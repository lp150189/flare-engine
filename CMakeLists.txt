Project (Flare)
cmake_minimum_required (VERSION 2.6)

Set (PACKAGE "FLARE")
Set (VERSION "0.14.1")

# Detect missing dependencies

Find_Package (SDL REQUIRED)
If (NOT SDL_FOUND)
  Message (FATAL_ERROR "Couldn't find SDL development files. On Debian-based systems (such as Ubuntu) you should install the 'libsdl1.2-dev' package.")
Else (NOT SDL_FOUND)
  Include_Directories (${SDL_INCLUDE_DIR})
EndIf (NOT SDL_FOUND)

Find_Package (SDL_mixer REQUIRED)
If (NOT SDLMIXER_FOUND)
  Message (FATAL_ERROR "Couldn't find SDL-mixer development files. On Debian-based systems (such as Ubuntu) you should install the 'libsdl-mixer1.2-dev' package.")
Else (NOT SDLMIXER_FOUND)
  Include_Directories (${SDLMIXER_INCLUDE_DIR})
EndIf (NOT SDLMIXER_FOUND)

Find_Package (SDL_image REQUIRED)
If (NOT SDLIMAGE_FOUND)
  Message (FATAL_ERROR "Couldn't find SDL-image development files. On Debian-based systems (such as Ubuntu) you should install the 'libsdl-image1.2-dev' package.")
Else (NOT SDLIMAGE_FOUND)
  Include_Directories (${SDLIMAGE_INCLUDE_DIR})
EndIf (NOT SDLIMAGE_FOUND)

Find_Package (SDL_ttf REQUIRED)
If (NOT SDLTTF_FOUND)
  Message (FATAL_ERROR "Couldn't find SDL-ttf development files. On Debian-based systems (such as Ubuntu) you should install the 'libsdl-ttf1.2-dev' package.")
Else (NOT SDLTTF_FOUND)
  Include_Directories (${SDLTTF_INCLUDE_DIR})
EndIf (NOT SDLTTF_FOUND)


# Sources

Set (FLARE_SOURCES 
	../src/Entity.cpp
	../src/Animation.cpp
	../src/Avatar.cpp
	../src/CampaignManager.cpp
	../src/Enemy.cpp
	../src/EnemyGroupManager.cpp
	../src/EnemyManager.cpp
	../src/FileParser.cpp
	../src/FontEngine.cpp
	../src/GameState.cpp
	../src/GameStateTitle.cpp
	../src/GameStateLoad.cpp
	../src/GameStatePlay.cpp
	../src/GameStateNew.cpp
	../src/GameSwitcher.cpp
	../src/Hazard.cpp
	../src/HazardManager.cpp
	../src/InputState.cpp
	../src/ItemDatabase.cpp
	../src/ItemStorage.cpp
	../src/LootManager.cpp
	../src/MapCollision.cpp
	../src/MapIso.cpp
	../src/Menu.cpp
	../src/MenuActionBar.cpp
	../src/MenuCharacter.cpp
	../src/MenuConfirm.cpp
	../src/MenuEnemy.cpp
	../src/MenuExit.cpp
	../src/MenuExperience.cpp
	../src/MenuHPMP.cpp
	../src/MenuHUDLog.cpp
	../src/MenuInventory.cpp
	../src/MenuItemStorage.cpp
	../src/MenuLog.cpp
	../src/MenuManager.cpp
	../src/MenuMiniMap.cpp
	../src/MenuPowers.cpp
	../src/MenuTalker.cpp
	../src/MenuTooltip.cpp
	../src/MenuVendor.cpp
	../src/MessageEngine.cpp
	../src/NPC.cpp
	../src/NPCManager.cpp
	../src/PowerManager.cpp
	../src/QuestLog.cpp
	../src/SaveLoad.cpp
	../src/Settings.cpp
	../src/StatBlock.cpp
	../src/TileSet.cpp
	../src/Utils.cpp
	../src/UtilsFileSystem.cpp
	../src/UtilsParsing.cpp
	../src/WidgetButton.cpp
	../src/WidgetInput.cpp
	../src/WidgetLabel.cpp
	../src/main.cpp
)

Add_Executable (flare ${FLARE_SOURCES})

# libSDLMain comes with libSDL if needed on certain platforms
If (NOT SDLMAIN_LIBRARY)
  Set (SDLMAIN_LIBRARY "")
EndIf (NOT SDLMAIN_LIBRARY)

Target_Link_Libraries (flare ${SDL_LIBRARY} ${SDLMIXER_LIBRARY} ${SDLIMAGE_LIBRARY} ${SDLTTF_LIBRARY} ${SDLMAIN_LIBRARY})


# installing to the proper places
install(PROGRAMS ${CMAKE_CURRENT_BINARY_DIR}/flare
  DESTINATION games)
install(DIRECTORY
  "${CMAKE_CURRENT_SOURCE_DIR}/animations"
  "${CMAKE_CURRENT_SOURCE_DIR}/enemies"
  "${CMAKE_CURRENT_SOURCE_DIR}/engine"
  "${CMAKE_CURRENT_SOURCE_DIR}/fonts"
  "${CMAKE_CURRENT_SOURCE_DIR}/images"
  "${CMAKE_CURRENT_SOURCE_DIR}/items"
  "${CMAKE_CURRENT_SOURCE_DIR}/maps"
  "${CMAKE_CURRENT_SOURCE_DIR}/music"
  "${CMAKE_CURRENT_SOURCE_DIR}/npcs"
  "${CMAKE_CURRENT_SOURCE_DIR}/powers"
  "${CMAKE_CURRENT_SOURCE_DIR}/quests"
  "${CMAKE_CURRENT_SOURCE_DIR}/soundfx"
  "${CMAKE_CURRENT_SOURCE_DIR}/tilesetdefs"
  DESTINATION share/games/flare)