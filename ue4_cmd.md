# UE4 binary distro
* AutomationTool BuildGraph -target="Make Installed Build Win64" -script=Engine/Build/BARBBuildDistro.xml -clean
* UnrealVersionSelector.exe /fileassociations


# UE4 new engine version
AutomationToolLauncher UpdateLocalVersion -Verbose -NoP4
Automation.cs if (CommandUtils.P4Enabled) to false change it during runtime, 


* Build\BatchFiles\RunUAT.bat -list 
* Binaries\DotNET>.. \ .. \Build\BatchFiles\RunUAT.bat UpdateLocalVersion (must be P4 connected)
* https://answers.unrealengine.com/questions/873535/automationtool-error-failed-to-delete-automationut.html
* Engine\Source\Programs\DotNETCommon\MetaData.cs
* UE4Build.cs line //CommandUtils.P4.Sync(String.Format("-f \"{0}@{1}\"", BuildVersionFile, ChangelistNumber), false, false);
// Copyright Epic Games, Inc. All Rights Reserved.

using System.Reflection;
using System.Runtime.InteropServices;
using System.Resources;

// These are the assembly properties for all tools
[assembly: AssemblyCompany( "Epic Games, Inc." )]
[assembly: AssemblyProduct( "UE4" )]
[assembly: AssemblyCopyright( "Copyright Epic Games, Inc. All Rights Reserved." )]
[assembly: AssemblyTrademark( "" )]

// Use a neutral culture to avoid some localisation issues
[assembly: AssemblyCulture( "" )]

[assembly: ComVisible( false )]
[assembly: NeutralResourcesLanguageAttribute( "" )]

#if !SPECIFIC_VERSION
// Automatically generate a version number based on the time of compilation
[assembly: AssemblyVersion( "4.0.0.0" )]
[assembly: AssemblyInformationalVersion("4.25.666-ByteCave")]
#endif


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


