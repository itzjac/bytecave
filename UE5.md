# CheatSheet
* BOM in files
* UnrealEngine3/4 BSP brush tool
* Best Tips and practices [https://flassari.notion.site/UE-Tips-Best-Practices-3ff4c3297b414a66886c969ff741c5ba]

# Logging 
Build.h turn off file logiing NO_LOGGING (set per build target)
```
UE_BUILD_DEVELOPMENT
	#ifndef DO_GUARD_SLOW
		#define DO_GUARD_SLOW									0
	#endif
	#ifndef DO_CHECK
		#define DO_CHECK										1
	#endif
	#ifndef STATS
		#define STATS											((WITH_UNREAL_DEVELOPER_TOOLS || !WITH_EDITORONLY_DATA || USE_STATS_WITHOUT_ENGINE || USE_MALLOC_PROFILER || FORCE_USE_STATS) && !ENABLE_STATNAMEDEVENTS)
	#endif
	#ifndef ALLOW_DEBUG_FILES
		#define ALLOW_DEBUG_FILES								1
	#endif
	#ifndef ALLOW_CONSOLE
		#define ALLOW_CONSOLE									1
	#endif
	#ifndef NO_LOGGING
		#define NO_LOGGING										0
	#endif
```

# Blueprint
	// bytecave: when more than one ouput pin in blueprint is desired, use the *&
	UFUNCTION(BlueprintCallable, BlueprintNativeEvent)
	bool TraceForPhysicsBodies(AActor*& HitActor, UPrimitiveComponent*& HitComponent);


# UE4 binary distro
https://answers.unrealengine.com/questions/164423/where-to-inject-custom-engine-versioning.html
Work only with engine in the github repo
Pdbcopy.exe  dependency, install https://developer.microsoft.com/en-us/windows/downloads/windows-10-sdk/
https://forums.unrealengine.com/development-discussion/engine-source-github/113790-installed-build-fails-trying-to-run-pdbcopy-exe
Must have installed exactly .NET 4.5.0






# UnrealEngine3/UDK - Deprecated 

https://udn.epicgames.com/lists/showpost.php?id=62975&list=unprog3

https://udn.epicgames.com/lists/showpost.php?id=67441&list=unprog3

https://udn.epicgames.com/Three/UnSetup

https://udn.epicgames.com/Three/InstallationAndDistribution

https://udn.epicgames.com/Three/BuildAndReleaseHome

# UnrealEngine4

Install
https://www.unrealengine.com/en-US/ue4-on-github GitHub
https://github.com/EpicGames/UnrealEngine UnrealEngine
https://docs.unrealengine.com/latest/INT/GettingStarted/DownloadingUnrealEngine/index.html Step by step
https://docs.unrealengine.com/latest/INT/Programming/Development/BuildingUnrealEngine/index.html#compilingunrealengine Compile engine
https://docs.unrealengine.com/latest/INT/GettingStarted/Installation/index.html Installing Unreal Engine by Epic Launcher :(
https://github.com/EpicGames/UnrealTournament UnrealTournament
https://github.com/EpicGames All Epic Games 
http://www.hourences.com/tutorials-ue3-texture-optimization/ Hourences


https://docs.unrealengine.com/latest/INT/Programming/Development/CodingStandard/index.html Coding standard (enums)


https://docs.unrealengine.com/latest/INT/Programming/Introduction/index.html Introduction to C++ programming

https://docs.unrealengine.com/latest/INT/Engine/Blueprints/TechnicalGuide/Compiler/index.html Blueprint Compiling overview

https://docs.unrealengine.com/latest/INT/Programming/UnrealArchitecture/Reference/Properties/Specifiers/index.html Property Specifiers


https://docs.unrealengine.com/latest/INT/Programming/UnrealArchitecture/Actors/index.html Actors


https://www.unrealengine.com/en-US/blog/unreal-property-system-reflection Unreal property system reflection

https://docs.unrealengine.com/latest/INT/Programming/UnrealArchitecture/Reference/Classes/Specifiers/index.html Classes specifiers

https://docs.unrealengine.com/latest/INT/Programming/UnrealArchitecture/Reference/Functions/Specifiers/index.html Function specifiers

https://docs.unrealengine.com/latest/INT/Programming/UnrealArchitecture/Reference/Structs/Specifiers/index.html Struct specifiers

https://docs.unrealengine.com/latest/INT/Programming/UnrealArchitecture/StringHandling/index.html String handling

https://wiki.unrealengine.com/Forward_Declarations Forward declarations


https://www.dropbox.com/s/xcix3b93tn73zt1/%EC%96%B8%EB%A6%AC%EC%96%BC%20%EC%97%94%EC%A7%84%204%20%EC%97%90%EB%94%94%ED%84%B0%20%ED%99%95%EC%9E%A5%EB%B2%95_Keegan%20Gibson.pdf?dl=0 Plugins

https://www.dropbox.com/s/w04ng7w1o721kyj/GDC2015%20%EC%98%A4%ED%94%88%EC%9B%94%EB%93%9C%20%ED%85%8C%ED%81%AC%EB%8D%B0%EB%AA%A8%EC%9D%98%20%EB%B9%84%EB%B0%80_Jack%20Porter.pdf?dl=0 Open World Tech demo secrets

https://www.dropbox.com/s/slg51l0cr6pmc5e/ARM%20CPU%EC%99%80%20GPU%EB%A5%BC%20%ED%99%9C%EC%9A%A9%ED%95%9C%20%EB%AA%A8%EB%B0%94%EC%9D%BC%20%EA%B7%B8%EB%9E%98%ED%94%BD_ARM%ED%99%A9%EA%B4%91%EC%84%A0_%EC%B5%9C%EC%83%81%EC%9D%B5_%EC%97%90%ED%94%BD%EA%B2%8C%EC%9E%84%EC%8A%A4Niklas%20Smedberg.pdf?dl=0 Mali GPU Architecture


https://www.unrealengine.com/en-US/resources Third party resource / Tutorials

https://forums.unrealengine.com/unreal-engine/announcements-and-releases/2196-ue4-libraries-you-should-know-about?2064-UE4-Libraries-You-Should-Know-About!=&highlight=comment+overflow Libraries containers

https://forums.unrealengine.com/development-discussion/content-creation/33788-tga-vs-png-for-textures?62848-TGA-vs-PNG-(for-textures)= TGA or PNG for textures

# Memory management

https://wiki.unrealengine.com/Garbage_Collection_%26_Dynamic_Memory_Allocation#Overview Garbage Collection & Dynamic Memory Allocation

https://forums.unrealengine.com/development-discussion/c-gameplay-programming/33780-spawning-uobject-from-tsubclassof?62840-Spawning-UObject-from-TSubClassOf=&highlight=creating+uobject Spawning UObject from TSubClassOf

https://www.unrealengine.com/en-US/blog/optimizing-tarray-usage-for-performance Array performance

# Editor

https://wiki.unrealengine.com/Component_Visualizers Component Visualizers
https://wiki.unrealengine.com/Customizing_detail_panels Customizing details panels
https://answers.unrealengine.com/questions/164648/461-plugin-why-do-fleveleditormoduleregistertabspa.html Tab Spawner
https://wiki.unrealengine.com/UPARAM Expose parameter as output pin
https://vimeo.com/jasonchoi Fancy features

https://docs.unrealengine.com/latest/INT/Programming/Slate/DetailsCustomization/index.html Slate Details Panel Customization

https://answers.unrealengine.com/questions/226086/476-transient-uproperty-specifier-doesnt-work.html BP dependencies Transient properties

https://answers.unrealengine.com/questions/80010/cant-save-blueprint-referenced-in-enginetransient.html BP dependencies Can’t save BP error!!!!


https://www.youtube.com/watch?v=ITdXkenr6no&feature=youtu.be character & materials
https://www.youtube.com/watch?v=VTc91YolRTI
https://www.youtube.com/watch?v=jG0739vqV5U&feature=youtu.be

# Animation

https://docs.unrealengine.com/latest/INT/Engine/Animation/RootMotion/index.html Root motion

https://docs.unrealengine.com/latest/INT/Engine/Blueprints/UserGuide/EventDispatcher/index.html Event Dispatcher

https://answers.unrealengine.com/questions/73533/how-to-design-a-generic-animbp-with-variable-anima.html Play random animation from a list
# Destructibles

https://docs.unrealengine.com/latest/INT/Engine/Physics/Collision/Overview/index.html Collision Overview

https://www.unrealengine.com/en-US/blog/collision-filtering Collision Filtering

# Navigation Mesh

https://answers.unrealengine.com/questions/49563/how-to-have-a-static-mesh-be-ignored-by-a-navmesh.html Static mesh be ignored by navmesh

https://docs.unrealengine.com/latest/INT/Engine/Components/Navigation/ Navigation components


# Networking

* UE4 Cedric https://cedric-neukirchen.net/Downloads/Compendium/UE4_Network_Compendium_by_Cedric_eXi_Neukirchen.pdf
* UDP wrapper for UE4 https://github.com/getnamo/udp-ue4
* UE4 simulate network conditions https://answers.unrealengine.com/questions/46072/simulate-network-conditions-commands.html
* Traveling in Multiplayer https://dawnarc.com/2017/06/ue4networking-in-baisc-travelling-in-multiplayer/

https://answers.unrealengine.com/questions/891883/dedicated-server-performance-1.html Server performance and multithreading

https://answers.unrealengine.com/questions/43178/how-do-you-create-a-server-clients-in-code-not-in.html Command line

https://www.youtube.com/watch?v=ZsDRDAdtA9w Variable replication


https://udn.unrealengine.com/questions/6300/network-dormancy.html Dormancy


https://forums.unrealengine.com/unreal-engine/announcements-and-releases/1812-new-blog-post-network-tips-and-tricks?1690-New-blog-post-Network-Tips-and-Tricks=&highlight=two+server+calls Tips and tricks

https://docs.unrealengine.com/latest/INT/Gameplay/Networking/Actors/Components/index.html Component replication

https://udn.unrealengine.com/questions/256127/editor-crash-if-you-start-multiplayer-client-with.html Common crashes in editor with Dedicated Server 
The related code ----> https://github.com/EpicGames/UnrealEngine/blob/5fd57546cc721650026801021de0be733d48a3e9/Engine/Source/Editor/UnrealEd/Private/PlayLevel.cpp
https://answers.unrealengine.com/questions/89747/how-to-read-netprofile-and-stat-net-output.html how to read netprofile and stat net output


Epic Launcher ContentExamples /  Network_Features tutorials
# Performance

https://www.tomlooman.com/unrealengine-optimization-talk/ UE5 Optmization

https://unrealartoptimization.github.io/book/process/ Art Optimization

https://topic.alibabacloud.com/a/ui-optimization-tips-in-unreal-engine-4_8_8_10274886.html UI Optimization

https://www.unrealengine.com/en-US/blog/how-to-improve-game-thread-cpu-performance CPU performance

https://docs.unrealengine.com/latest/INT/Engine/Performance/CPU/index.html CPU profiling

https://docs.unrealengine.com/latest/INT/Engine/Performance/index.html Performance and profiling

https://docs.unrealengine.com/latest/INT/Engine/Performance/Profiler/index.html profiler tool reference

https://answers.unrealengine.com/questions/177892/game-hitches-gc-mark-time.html Game hitches (GC Mark Time)

https://docs.unrealengine.com/latest/INT/Gameplay/Tools/GameplayDebugger/ Gameplay Debugger runtime

https://indiebrothers.itch.io/ue4benchmark

https://www.orfeasel.com/implementing-multithreading-in-ue4/ Multithreading

# P4
https://www.perforce.com/blog/streams-tiny-tutorial streams

https://www.perforce.com/perforce/doc.current/manuals/p4v/Content/P4V/streams.task.html working with tasks streams


# Localization


https://docs.unrealengine.com/latest/INT/Gameplay/Localization/Setup/index.html Setup

https://docs.unrealengine.com/latest/INT/Gameplay/Localization/Overview/index.html#text System overview

https://forums.unrealengine.com/unreal-engine/announcements-and-releases/4087-creating-a-localization-ready-game-in-ue4-part-1-text?3924-CREATING-A-LOCALIZATION-READY-GAME-IN-UE4-Part-1-Text= Localization

https://forums.unrealengine.com/community/work-in-progress/995-arabic-version-of-unreal-editor?898-Arabic-version-of-Unreal-Editor=&viewfull=1 Arabic version

https://docs.unrealengine.com/latest/INT/Engine/UMG/index.html UMG UI

http://coherent-labs.com/coherent-gt/ Coherent UI

http://coherent-labs.com/using-the-unreal-engine-4-localization-with-coherent-ui/ Coherent UI Coherent labs 



# AI

https://wiki.unrealengine.com/Blueprint_Behavior_Tree_Tutorial Behavior Tree

https://www.youtube.com/watch?v=PgxuaTSkyu4 AI workshop

https://www.youtube.com/watch?v=wMRxw6aM45k Basic cover system

https://www.youtube.com/watch?v=NZZtMNdJk5o Set up advanced AI

https://docs.unrealengine.com/latest/INT/Engine/AI/EnvironmentQuerySystem/UserGuide/ Environment system

http://www.gdcvault.com/play/1015665/Believable-Tactics-for-Squad Tactics Squad AI

Linux
https://wiki.unrealengine.com/Building_Linux_cross-toolchain Cross tool chain

https://wiki.unrealengine.com/Compiling_For_Linux Compiling for Linux

https://answers.unrealengine.com/questions/120642/how-to-setup-cross-compilation-toolchain-for-linux.html How to set up cross-compilation toolchain for linux packaging

# Cooking

https://docs.unrealengine.com/latest/INT/Engine/Deployment/Cooking/index.html Content cooking

https://wiki.unrealengine.com/How_to_package_your_game_with_commands Package with commands

https://answers.unrealengine.com/questions/333314/cookalltrue-but-no-cooking.html Cook all but not cooking

https://udn.unrealengine.com/questions/196897/shorten-pathnames-when-cooking.html Shorten pathnames when cooking


 https://udn.unrealengine.com/questions/276937/cooking-requires-source-files.html Cooking requires source files

https://udn.unrealengine.com/questions/267420/whenhow-can-we-guarantee-the-use-of-cooked-content.html# When can we guarantee the use of cooked content

# Collision
https://www.unrealengine.com/en-US/blog/collision-filtering?sessionInvalidated=true


# Visual Studio
// Intellisense cpp.hint file
//
https://msdn.microsoft.com/en-us/library/dd997977.aspx

# CPU usage and threads
https://gpuopen.com/learn/threadripper-for-gamedev-ue4/
