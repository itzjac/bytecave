# UE4 new engine version without P4
Create a new engine version

Build.version is the entry point to change the engine version.

AutomationToolLauncher is invoked with the BatchFiles included with the engine distro,
verify listing all the command line options 
```
Binaries\DotNET>.. \ .. \Build\BatchFiles\RunUAT.bat -list 
```

Generally, to generate a new engine version, it must be P4 connected
```
Binaries\DotNET>.. \ .. \Build\BatchFiles\RunUAT.bat UpdateLocalVersion
```

AutomationToolLauncher includes a NoP4 option, not implemented by Epic
```
UpdateLocalVersion -Verbose -NoP4
```

We provide two methods to avoid using P4 and support the -NoP4 command line option.


## First method (debugging hack)
* Automation.cs if (CommandUtils.P4Enabled) to false change it during runtime
* One line comment in UE4Build.cs 
```
CommandUtils.P4.Sync(String.Format("-f \"{0}@{1}\"", BuildVersionFile, ChangelistNumber), false, false);
```


## Second method (completing code)
1. Automation.cs implements NoP4 support
```
// Enable or disable P4 support
if (!GlobalCommandLine.NoP4)
{
	CommandUtils.InitP4Support(CommandsToExecute, ScriptCompiler.Commands);
	if (CommandUtils.P4Enabled)
	{
		Log.TraceLog("Setting up Perforce environment.");
		CommandUtils.InitP4Environment();
		CommandUtils.InitDefaultP4Connection();
	}
}
```		
2. UE4Build.cs implements NoP4 support
```
public List<FileReference> UpdateVersionFiles(bool ActuallyUpdateVersionFiles = true, int? ChangelistNumberOverride = null, int? CompatibleChangelistNumberOverride = null, string Build = null, bool? IsPromotedOverride = null)
{
	bool bIsLicenseeVersion = ParseParam("Licensee") || !FileReference.Exists(FileReference.Combine(CommandUtils.EngineDirectory, "Build", "NotForLicensees", "EpicInternal.txt"));
	bool bIsPromotedBuild = IsPromotedOverride.HasValue? IsPromotedOverride.Value : (ParseParamInt("Promoted", 1) != 0);
	bool bDoUpdateVersionFiles = ParseParam("NoP4") ? true : CommandUtils.P4Enabled && ActuallyUpdateVersionFiles;		
	int ChangelistNumber = 0;
	if (bDoUpdateVersionFiles)
	{
		ChangelistNumber = ChangelistNumberOverride.HasValue? ChangelistNumberOverride.Value : CommandUtils.P4Env.Changelist;
	}
	int CompatibleChangelistNumber = 0;
	if(bDoUpdateVersionFiles && CompatibleChangelistNumberOverride.HasValue)
	{
		CompatibleChangelistNumber = CompatibleChangelistNumberOverride.Value;
	}
	string Branch = OwnerCommand.ParseParamValue("Branch");
	if (String.IsNullOrEmpty(Branch))
	{
		Branch = ParseParam("NoP4") ? ParseParamValue("Branch") : (CommandUtils.P4Enabled ? CommandUtils.EscapePath(CommandUtils.P4Env.Branch) : "");
	}
	return StaticUpdateVersionFiles(ChangelistNumber, CompatibleChangelistNumber, Branch, Build, bIsLicenseeVersion, bIsPromotedBuild, bDoUpdateVersionFiles, ParseParam("NoP4"));
}
```		
		
3. Implement NoP4 validation for all the occurrencies in UE4Build.cs
```
if(!NoP4 && CommandUtils.P4Enabled && ChangelistNumber > 0)
{
CommandUtils.P4.Sync(String.Format("-f \"{0}@{1}\"", BuildVersionFile, ChangelistNumber), false, false);
}
```	
4. Command line must include cl, compatiblecl, Build, and Branch options to exit success
```
.\..\Build\BatchFiles\RunUAT.bat UpdateLocalVersion -Verbose -NoP4 -cl=666 -compatiblecl=666 -Build=ByteCave666
```

5. Both methods Engine\Source\Programs\DotNETCommon\MetaData.cs should reflect the version changes

# Common pitfall when generating a new engine version
* mcrolib.dll , a .NET file, apparently related to the -compile option 
 * https://answers.unrealengine.com/questions/873535/automationtool-error-failed-to-delete-automationut.html
 * https://stackoverflow.com/questions/37960616/exception-thrown-system-exception-in-mscorlib-ni-dll-on-uwp-app-start 
 
# Launching UE4 with newer Build.version file

>Creating makefile for UE4Editor (Build.version is newer)

Splash window 
to get full patch version
const FText Version = FText::FromString( FEngineVersion::Current().ToString()); 

# UE4 binary distro
Deploy a custom engine version for artists or machine without VStudio

## Requirements
* PDBCOPY.EXE https://developer.microsoft.com/en-us/windows/downloads/windows-10-sdk/
* Must have installed exactly .NET 4.5.0 (from VStudio)
* https://developer.microsoft.com/en-us/windows/downloads/windows-10-sdk/
 
## Pipeline
* AutomationTool BuildGraph -target="Make Installed Build Win64" -script=Engine/Build/BARBBuildDistro.xml -clean
* UnrealVersionSelector.exe /fileassociations

# UE4 Commands
* Netprofile enable
* Netprofile disable
* Stat startfile
* Stat stopfile
* Stat Obj
* Slomo [float value]
* showflag.toggleparticles 0/1
* showflag.wireframe 0/1
* memreport -full
* stat D3D1RHI
* stat scenerendering
* stat engine
* toggleUI 1/0
* showdebug bones
* Net PktLoss=1
* Net PktOrder=0
* Net PktDup=0
*Net PktLag=75
* Net PktLagVariance=0
* p.netshowcorrections 1
* t.Max FPS 30

# UE4 Build system
https://docs.unrealengine.com/latest/INT/Programming/UnrealBuildSystem/Configuration/index.html Unreal Build System


Disable IncrediBuild here!!!
UnrealEngine-4.16\Engine\Saved\UnrealBuildTool\BuildConfiguration.xml
     ```<BuildConfiguration>
         <bAllowXGE>false</bAllowXGE>
     </BuildConfiguration>```
Command line -noxge


# Uncooked builds execution
@ECHO OFF
* client
start "MyGameClient" /D "UE4\Engine\Binaries\Win64" /MAX UE4Editor.exe  "full_path\MyGame\MyGame.uproject" -game 127.0.0.1 -log -messaging
* editor
start "MyGameEditor" /D "UE4\Engine\Binaries\Win64" /MAX UE4Editor.exe  "full_path\MyGame\MyGame.uproject" Example_Map -log -messaging
* server
@echo off
start "MyGameserver" /D "UE4\Engine\Binaries\Win64" /MAX UE4Editor.exe  "full_path\MyGame\MyGame.uproject" Example_Map -log -messaging Example_Map -server -log -messaging

auto test
@echo off
SET IPServer=127.0.0.1

SET Server=TestSystemMap016?
REM MAP_PVPSetdressTest_005

* start "MyGameServer" /D "UE4\Engine\Binaries\Win64" /MAX UE4Editor.exe  "full_path\MyGame\MyGame.uproject" Example_Map?port=36004 -server -log -messaging -NOSTEAM -PORT=7810

## echo giving server some time to start

* ping /n 16 localhost >nul

## echo starting test client

* ping /n 7 localhost >nul


