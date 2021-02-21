# UE4 new engine version without P4
Create a new engine version

Build.version is the entry point to change the engine version

AutomationToolLauncher UpdateLocalVersion -Verbose -NoP4
-NoP4 doesn't work out of the box

* First approach debugging hack, Automation.cs if (CommandUtils.P4Enabled) to false change it during runtime
* 
* Binaries\DotNET>.. \ .. \Build\BatchFiles\RunUAT.bat -list 
* Binaries\DotNET>.. \ .. \Build\BatchFiles\RunUAT.bat UpdateLocalVersion (must be P4 connected)
* https://answers.unrealengine.com/questions/873535/automationtool-error-failed-to-delete-automationut.html
* Engine\Source\Programs\DotNETCommon\MetaData.cs
* UE4Build.cs line //CommandUtils.P4.Sync(String.Format("-f \"{0}@{1}\"", BuildVersionFile, ChangelistNumber), false, false);
// Copyright Epic Games, Inc. All Rights Reserved.


* Second approach Automation.cs with NoP4 support

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
			
* UE4Build.cs with NoP4 support

```public List<FileReference> UpdateVersionFiles(bool ActuallyUpdateVersionFiles = true, int? ChangelistNumberOverride = null, int? CompatibleChangelistNumberOverride = null, string Build = null, bool? IsPromotedOverride = null)
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
		}```
	
		
		
	* All occurrencies
			if(!NoP4 && CommandUtils.P4Enabled && ChangelistNumber > 0)
						{
							CommandUtils.P4.Sync(String.Format("-f \"{0}@{1}\"", BuildVersionFile, ChangelistNumber), false, false);
						}

UE4Build.cs
bool bDoUpdateVersionFiles = /*CommandUtils.P4Enabled &&*/ ActuallyUpdateVersionFiles;		


.\..\Build\BatchFiles\RunUAT.bat UpdateLocalVersion -Verbose -NoP4 -cl=666 -compatiblecl=666 -Build=ByteCave666
MetaData.cs is now updated accordingly

When launching UE4

>Creating makefile for UE4Editor (Build.version is newer)

Splash window 
to get full patch version
const FText Version = FText::FromString( FEngineVersion::Current().ToString()); 

# UE4 binary distro
Deploy a custom engine version for artists or machine without VStudio
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


