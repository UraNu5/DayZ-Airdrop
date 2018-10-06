# Airdrop
DayZ 0.63 AirDrop mod by mov3ax / mov3ax.pro

## Credits

* @i_kolobov - Documentation and Code snippets
* @Arkensor - Code snippets
* @FIDOv - Documentation
* @Revelin - Code snippets

## Setup

Copy all code from 

```
/* DayZ 0.63 AirDrop plugin by mov3ax / mov3ax.pro */
/* ### ### ### ### ### ### ### ### */
```

Up to

```
/* ### ### ### ### ### ### ### ### */
```

And paste it into init.c of your server, into class of your mission, by default it is -

```
class CustomMission: MissionServer
```

After that copy OnUpdate method

```
float TimerSlice;
	override void OnUpdate( float timeslice )
	{
		super.OnUpdate( timeslice );

		// FPS Fix
		TimerSlice += timeslice;
		if (TimerSlice >= TimesliceMultiplyier)
		{
			CreateAirDrop();
			TimerSlice = 0;	
		}
	}
```

And put it to your, init.c file, if you already have OnUpdate method you just have to add "float TimerSlice;" above it and put following  code into your OnUpdate method

```
// FPS Fix
		TimerSlice += timeslice;
		if (TimerSlice >= TimesliceMultiplyier)
		{
			CreateAirDrop();
			TimerSlice = 0;	
		}
```

So now you have installed airdrop plugin

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
SpawnZombie - Spawn zombie near airdrop when landed
PrintInformationMessages - Show chat messages about -

* Airplane flew out
* Airdrop dropped
* Airdrop landed

DropOnStart - Use only for debug and test puproses, drop airdrop instantly after airplane flew out
TeleportDebug - Use only for debug and test puproses, teleport all players to airplane and airdrop

## Plans

* Add physics to falling container (Like physics on car)
* Add airdrop flare
* Fix plane sound radius
* ✅ Add zombie spawns around airdrop
