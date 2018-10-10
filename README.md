# Airdrop
DayZ 0.63 AirDrop mod by mov3ax / mov3ax.pro

## Credits

* @i_kolobov - Documentation and Code snippets
* @Arkensor - Code snippets
* @FIDOv - Documentation
* @Revelin - Code snippets

## Setup

* Extract archive to your mission folder, (e.g default dayzOffline.chernarusplus)
* Open init.c file of your server using any notepad
* Include plugin to your init.c file

```
#include "$CurrentDir:\\mpmissions\\dayzOffline.chernarusplus\\plugins\\AirDrop.c"
```

* Find your custom mission class

```
class CustomMission : MissionServer
```

* Append this code inside class

```
ref AirDrop AirDropClass; // Class definition

void CustomMission()
{
	AirDropClass = new AirDrop;		
}

float TimerSlice; // Timeslice
override void OnUpdate( float timeslice )
{
	super.OnUpdate( timeslice );

	// FPS Fix
	TimerSlice += timeslice;
	if (TimerSlice >= AirDropClass.TimesliceMultiplyier)
	{
		AirDropClass.CreateAirDrop();
		TimerSlice = 0;	
	}
}
```

If you already have OnUpdate method you just have to add following code into it

```
// FPS Fix
TimerSlice += timeslice;
if (TimerSlice >= AirDropClass.TimesliceMultiplyier)
{
	AirDropClass.CreateAirDrop();
	TimerSlice = 0;	
}
```

Also don't forget to add following variable above OnUpdate

```
float TimerSlice; // Timeslice
```

Now you have installed airdrop plugin

## Configuration

Default code -

```
bool EnableAirdrops = true; // Main switch

float TimesliceMultiplyier = 0.01; // Timeslice multiplyier, default value is 0.01 (60 FPS)
float AirPlaneSpeed = 0.25; // Airplane fly speed 
float AirPlaneHeight = 500; // Airplane fly height 
float AirDropFallSpeed = 0.2; // Airdrop fall speed 
// 600 Seconds = 10 Minutes
float TicksTimerFromStart = 600 / TimesliceMultiplyier; // How much time will pass from the server start to first airdrop
bool PrintInformationMessages = true; // Show in chat when airplane flew out and when airdrop is landed
bool PrintInformationCoordinates = true; // Show in chat coordinates where airdrop is landed
// 36000 Seconds = 1 Hour
float RemoveTime = 36000 / TimesliceMultiplyier; // After how much time airplane and loot will be removed and new airplane will be spawned
bool SpawnZombie = true; // Spawn zombie near airdrop when landed
bool ShowSignal = true; // Show smoke signal when airdrop landed

float RandomBoundsMin = 95; // Airdrop drop bounds min
float RandomBoundsMax = 180; // Airdrop drop bounds max
	
bool PrintDebugMessages = false; // Show debug messages (Debug)
bool DropOnStart = false; // Drop airdrop instantly after airplane (Debug)
bool TeleportDebug = false; // Teleport to airplane and airdrop during flight (Debug)
```

EnableAirdrops - Enable or Disable airdrop switch
TimesliceMultiplyier - Value that responds for smooth processing time, default value is 1, so if you wan't to process time in 60 FPS you need divide 1 by 60 that as a result equals 0.01
AirPlaneSpeed - How fast airplane will move
AirPlaneHeight - How high will the plane fly
AirDropFallSpeed - How fast airdrop will fall
TicksTimerFromStart - How much time will pass from the server start to first airdrop
RandomBoundsMin - Airdrop drop bounds minimum
RandomBoundsMax - Airdrop drop bounds maximum
SpawnZombie - Spawn zombie near airdrop when landed
ShowSignal - Show smoke signal when airdrop landed
PrintInformationMessages - Show chat messages about -

* Airplane flew out
* Airdrop dropped
* Airdrop landed

DropOnStart - Use only for debug and test puproses, drop airdrop instantly after airplane flew out
TeleportDebug - Use only for debug and test puproses, teleport all players to airplane and airdrop

## Setup tutorial

<a href="http://www.youtube.com/watch?feature=player_embedded&v=kYgzQY_wy94
" target="_blank"><img src="http://img.youtube.com/vi/kYgzQY_wy94/0.jpg" 
alt="IMAGE ALT TEXT HERE" width="240" height="180" border="10" /></a>

## Plans

* ✅ Add physics to falling container
* ✅ Add airdrop flare
* ✅ Add zombie spawns around airdrop
* Fix particles on server, land and signal effect
* Fix plane sound radius
* Show information about airdrop only with equipped radio
