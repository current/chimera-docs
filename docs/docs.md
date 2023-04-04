
---


<a name="-1"></a>

|Index|
|--------|
|[Penetration](#0)| 
|[Trace](#1)| 
|[Engine](#2)| 
|[DebugOverlay](#3)| 
|[ClientState](#4)| 
|[Event](#5)| 
|[Netvars](#6)| 
|[GlobalVariables](#7)| 
|[InputSystem](#8)| 
|[Memory](#9)| 
|[Cvar](#10)| 
|[AntiAim](#11)| 
|[Client](#12)| 
|[Fakelag](#13)| 
|[HTTP](#14)|
|[HTTPS](#15)|
|[Menu](#16)|
|[Doubletap](#17)|
|[EntityList](#18)|
|[Paint](#19)|
|[Bits](#20)|
|[Entity](#21)|
|[Surface](#22)|
|[World](#23)|
|[Console](#24)|
|[Sound](#25)|
|[CreateMove](#26)|
|[FrameStageNotify](#27)|
|[PostScreenEffects](#28)|
|[OverrideView](#29)|
|[Animations](#30)|
|[Vector](#31)|
|[Vector2D](#32)|
|[Color](#33)|
|[CGameTrace](#34)|
|[PlayerInfo_t](#35)|
|[ResolveData](#36)|
|[PaintStringRenderFlags](#37)|
|[SurfaceStringRenderFlags](#38)|
|[PaintFontCreationFlags](#39)|
|[Stages](#41)|
|[CBasePlayer](#42)|
|[Virtual Key](#43)|
|[ConVar](#43)|
|[CFont](#44)|
|[IFont](#45)|
|[BoneID](#46)|
|[Print](#47)|
|[ITexture](#48)|
|[Lua](#49)|
|[Rage](#50)|
|[PacketManager](#51)|

---

## <a name="0"></a>Penetration
---

#### Penetration.CanPenetrate


##### Parameters:

| Name | Type |
| :--- | :--- | 
| start | Vector | 
| end | Vector |

##### Returns:

| Name | Type | 
| :--- | :--- |
| penetration | bool | 


```lua
Penetration.CanPenetrate(Entity.GetEyePosition(EntityList.GetLocalPlayer()), Entity.GetBonePosition(Enemy, 0)) 
--true if we can penetrate false if we can't
```


#### Penetration.PredictDamage


##### Parameters:

| Name | Type | 
| :--- | :--- |
| start | Vector | 
| end | Vector | 
| target | CBasePlayer |

##### Returns:

| Name | Type | 
| :--- | :--- | 
| damage | int |


```lua
Penetration.PredictDamage(Entity.GetEyePosition(EntityList.GetLocalPlayer()), Entity.GetBonePosition(Enemy, 0), Enemy) 
--will be -1 if invalid parameters or (0 - max damage) if valid
```





[back to Contents](#-1)

---


## <a name="1"></a>Trace
---


#### Trace.GetPointContents


##### Parameters:

| Name | Type | 
| :--- | :--- | 
| point | Vector |

##### Returns:

| Name | Type | 
| :--- | :--- | 
| contents | int | 


```lua
Trace.GetPointContents(Entity.GetEyePosition(EntityList.GetLocalPlayer())) 
--will get point contents of local eye position 
```

#### Trace.GetPointContentsWorld



**Only returns world contents**


##### Parameters:

| Name | Type |
| :--- | :--- | 
| point | Vector | 

##### Returns:

| Name | Type | 
| :--- | :--- | 
| contents | int | 


```lua
Trace.GetPointContentsWorld(Entity.GetEyePosition(EntityList.GetLocalPlayer())) 
--will get point contents of local eye position
```


#### Trace.Line


##### Parameters:

| Name | Type | Description |
| :--- | :--- | :--- |
| start | Vector | 
| end | Vector | 
| skip [-1 if no player] | CBasePlayer | 
| mask | int | 

##### Returns:

| Name | Type |
| :--- | :--- |
| result | CGameTrace | 


```lua
Trace.Line(Entity.GetEyePosition(EntityList.GetLocalPlayer()), Entity.GetBonePosition(Enemy, 0), -1, 0x1).fraction == 1.0
--1.0 means our line did not hit anything
```

#### Trace.Ray


##### Parameters:

| Name | Type | Description |
| :--- | :--- | :--- |
| start | Vector | start position |
| end | Vector | end position |
| mins | Vector | bounding box min |
| max | Vector | bounding box max |
| skip | CBasePlayer | player skipped [-1 if no player] |
| mask | int | Trace Mask |

##### Returns:

| Name | Type | Description |
| :--- | :--- | :--- |
| Trace | CGameTrace | trace result |


```lua
Trace.Ray(Entity.GetEyePosition(EntityList.GetLocalPlayer()), Entity.GetBonePosition(Enemy, 0), Vector.Get(-2,-2,-2), Vector.Get(2,2,2), -1, 0x1).fraction == 1.0
--1.0 means our line did not hit anything
```




[back to Contents](#-1)

---

## <a name="2"></a>Engine
---


#### Engine.ExecuteClientCommand


##### Parameters:

| Name | Type | 
| :--- | :--- |
| command | string |

##### Returns:

| Name | Type | 
| :--- | :--- |
| | |

```lua
Engine.ExecuteClientCommand("say hello from oak!")
--will say hello in chat
```

#### Engine.GetGameDirectory


##### Parameters:

| Name | Type |
| :--- | :--- |
| | |

##### Returns:

| Name | Type |
| :--- | :--- | 
| game directory | string |


```lua
local gamedirectory = Engine.GetGameDirectory()
--this will be your game directory
```

#### Engine.GetLevelName


##### Parameters:

| Name | Type |
| :--- | :--- |
| | |

##### Returns:

| Name | Type |
| :--- | :--- | 
| level name [includes .bsp] | string |


```lua
local levelname = Engine.GetLevelName()
--your level name
```

#### Engine.GetLevelNameShort


##### Parameters:

| Name | Type |
| :--- | :--- |
| | |

##### Returns:

| Name | Type |
| :--- | :--- | 
| level name [example: de_mirage instead of de_mirage.bsp] | string |


```lua
local levelname = Engine.GetLevelNameShort()
--your level name
```

#### Engine.GetLocalPlayer


##### Parameters:

| Name | Type |
| :--- | :--- |
| | |

##### Returns:

| Name | Type |
| :--- | :--- | 
| local player | CBasePlayer |


```lua
local localplayer = Engine.GetLocalPlayer()
--this gets local player but you can also use EntityList.GetLocalPlayer()
```

#### Engine.GetMapGroupName


##### Parameters:

| Name | Type |
| :--- | :--- |
| | |

##### Returns:

| Name | Type |
| :--- | :--- | 
| map group name | string |


```lua
local groupname = Engine.GetMapGroupName()
--map group name
```

#### Engine.GetMaxClients


##### Parameters:

| Name | Type |
| :--- | :--- |
| | |

##### Returns:

| Name | Type |
| :--- | :--- | 
| total number of players | int |


```lua
local numclients = Engine.GetMaxClients()
--total clients, you can also use EntityList.NumberOfPlayers() or GlobalVariables.TotalClients()
```

#### Engine.GetViewAngles


##### Parameters:

| Name | Type |
| :--- | :--- |
| | |

##### Returns:

| Name | Type |
| :--- | :--- | 
| viewangle | Vector |


```lua
local viewangle = Engine.GetViewAngles()
--this gets the local viewangle
```

#### Engine.SetViewAngles


##### Parameters:

| Name | Type |
| :--- | :--- |
| Viewangle | Vector |

##### Returns:

| Name | Type |
| :--- | :--- | 
|  |  |


```lua
Engine.SetViewAngles(Vector.Get(0,89,0))
--this will make you look down
```



[back to Contents](#-1)

---

## <a name="3"></a>DebugOverlay
---

#### DebugOverlay.AddBox


##### Parameters:

| Name | Type |
| :--- | :--- | 
| origin | Vector | 
| mins | Vector |
| maxs | Vector |
| orientation | Vector |
| color | Color |
| duration | float |

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
DebugOverlay.AddBox(Vector.Get(0,0,0), Vector.Get(-5,-5,-5), Vector.Get(5,5,5), Vector.Get(0,0,0), Color.Get(255,255,255,255), 3.0)
```

#### DebugOverlay.AddCapsule


##### Parameters:

| Name | Type |
| :--- | :--- | 
| mins | Vector |
| maxs | Vector |
| radius | float |
| color | Color |
| duration | float |

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
DebugOverlay.AddCapsule(Vector.Get(-5,-5,-5), Vector.Get(5,5,5), 10.0, Color.Get(255,255,255,255), 3.0)
```

#### DebugOverlay.AddLine


##### Parameters:

| Name | Type |
| :--- | :--- | 
| start | Vector |
| end | Vector |
| color | Color |
| duration | float |
| disabledepth [optional] | bool |

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
DebugOverlay.AddLine(Vector.Get(-5,-5,-5), Vector.Get(5,5,5), Color.Get(255,255,255,255), 3.0)
```

#### DebugOverlay.AddSphere


##### Parameters:

| Name | Type |
| :--- | :--- | 
| center | Vector |
| theta | int |
| phi | int |
| radius | float |
| color | Color |
| duration | float |

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
--preview unavailable
```

#### DebugOverlay.AddTriangle


##### Parameters:

| Name | Type |
| :--- | :--- | 
| point 1 | Vector |
| point 2 | Vector |
| point 3 | Vector |
| color | Color |
| duration | float |
| disabledepth [optional] | bool |

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
DebugOverlay.AddLine(Vector.Get(-5,-5,-5), Vector.Get(5,5,5), Color.Get(255,255,255,255), 3.0)
```


[back to Contents](#-1)

---

## <a name="4"></a>ClientState
---

#### ClientState.GetChokedCommands


##### Parameters:

| Name | Type |
| :--- | :--- | 
| | |

##### Returns:

| Name | Type | 
| :--- | :--- |
| Choked commands | int |


```lua
ClientState.GetChokedCommands()
-- can range from 0 to sv_maxusercmdprocessticks depending on how much ticks we choked
```

#### ClientState.GetCommandAck


##### Parameters:

| Name | Type |
| :--- | :--- | 
| | |

##### Returns:

| Name | Type | 
| :--- | :--- |
| command ack | int |


```lua
ClientState.GetCommandAck()
```

#### ClientState.GetLastOutgoingAck


##### Parameters:

| Name | Type |
| :--- | :--- | 
| | |

##### Returns:

| Name | Type | 
| :--- | :--- |
| command last outgoing ack | int |


```lua
ClientState.GetLastOutgoingAck()
```

#### ClientState.GetLastOutgoingCommand


##### Parameters:

| Name | Type |
| :--- | :--- | 
| | |

##### Returns:

| Name | Type | 
| :--- | :--- |
| command last outgoing command | int |


```lua
ClientState.GetLastOutgoingCommand()
```


[back to Contents](#-1)

---

## <a name="5"></a>Event
---

#### Event.RegisterListener


##### Parameters:

| Name | Type |
| :--- | :--- | 
| listener | function | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| | | 


```lua
function OnEventFired() 

end

Event.RegisterListener(OnEventFired)

--or

Event.RegisterListener(function()

end)
```


#### Event.GetName


##### Parameters:

| Name | Type |
| :--- | :--- | 
| | | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| Event name | string | 


```lua
Event.RegisterListener(function()
  if Event.IsServerEvent() then
    return
  end
  
  local EventName = Event.GetName() --event name
end)
```

#### Event.IsServerEvent


##### Parameters:

| Name | Type |
| :--- | :--- | 
| | | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| is server event | bool | 


```lua
Event.RegisterListener(function()
  if Event.IsServerEvent() then -- true if its a server event
    return
  end
  
  local EventName = Event.GetName() 
end)
```

#### Event.GetBool


##### Parameters:

| Name | Type |
| :--- | :--- | 
| key | string | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| value | bool | 


```lua
Event.RegisterListener(function()
  if Event.IsServerEvent() then
    return
  end
  
  if Event.GetName() ~= "player_death" then
    return
  end
  
  if Event.GetBool("assistedflash") then --get bool usage
    Print("Someone Assisted this kill with a flash!")
  end
  
end)
```

#### Event.GetFloat


##### Parameters:

| Name | Type |
| :--- | :--- | 
| key | string | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| value | float | 


```lua
Event.RegisterListener(function()
  if Event.IsServerEvent() then
    return
  end
  
  if Event.GetName() ~= "player_death" then
    return
  end
  
  
  Print(Event.GetFloat("distance")) -- distance from localplayer to the player whom died
  
  
end)
```

#### Event.GetInt


##### Parameters:

| Name | Type |
| :--- | :--- | 
| key | string | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| value | float | 


```lua
Event.RegisterListener(function()
  if Event.IsServerEvent() then
    return
  end
  
  if Event.GetName() ~= "player_death" then
    return
  end
  
  
  Print(Event.GetInt("distance")) -- distance from localplayer to the player whom died in integer form
  
  
end)
```


#### Event.GetString


##### Parameters:

| Name | Type |
| :--- | :--- | 
| key | string | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| value | float | 


```lua
Event.RegisterListener(function()
  if Event.IsServerEvent() then
    return
  end
  
  if Event.GetName() ~= "player_death" then
    return
  end
  
  
  Print(Event.GetString("weapon")) -- the weapon name that the killer used to kill the dead player
  
  
end)
```




[back to Contents](#-1)

---

## <a name="6"></a>Netvars
---

#### Netvars.GetOffset


##### Parameters:

| Name | Type |
| :--- | :--- | 
| table | string | 
| name | string |

##### Returns:

| Name | Type | 
| :--- | :--- |
| netvar offset | int | 


```lua
local m_flDuckAmountOffset = Netvars.GetOffset("DT_CSPlayer", "m_flDuckAmount")
```




[back to Contents](#-1)

---

## <a name="7"></a>GlobalVariables
---

#### GlobalVariables.Realtime


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 
|  |  |

##### Returns:

| Name | Type | 
| :--- | :--- |
| realtime | float | 


```lua
GlobalVariables.Realtime()
--time since csgo started
```

#### GlobalVariables.Framecount


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 
|  |  |

##### Returns:

| Name | Type | 
| :--- | :--- |
| Framecount | int | 


```lua
GlobalVariables.Framecount()
--total frames rendered
```

#### GlobalVariables.AbsoluteFrametime


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 
|  |  |

##### Returns:

| Name | Type | 
| :--- | :--- |
| frame time | float | 


```lua
GlobalVariables.AbsoluteFrametime()
--very accurate frametime
```

#### GlobalVariables.Frametime


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 
|  |  |

##### Returns:

| Name | Type | 
| :--- | :--- |
| frame time | float | 


```lua
GlobalVariables.Frametime()
--less accurate frametime
```

#### GlobalVariables.Curtime


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 
|  |  |

##### Returns:

| Name | Type | 
| :--- | :--- |
| current time | float | 


```lua
GlobalVariables.Curtime()
--current server time
```

#### GlobalVariables.TotalClients


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 
|  |  |

##### Returns:

| Name | Type | 
| :--- | :--- |
| total clients | int | 


```lua
GlobalVariables.TotalClients()
--number of clients or players
```


#### GlobalVariables.Tickcount


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 
|  |  |

##### Returns:

| Name | Type | 
| :--- | :--- |
| tickcount | int | 


```lua
GlobalVariables.Tickcount()
--client tickcount
```

#### GlobalVariables.IntervalPerTick


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 
|  |  |

##### Returns:

| Name | Type | 
| :--- | :--- |
| interval in time per tick | int | 


```lua
GlobalVariables.IntervalPerTick()
--the interval of time for a tick to increment
```


#### GlobalVariables.InterpolationAmmount


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 
|  |  |

##### Returns:

| Name | Type | 
| :--- | :--- |
| ammount | float | 


```lua
GlobalVariables.InterpolationAmmount()
--how much players are interpolated
```



#### GlobalVariables.NetworkProtocol


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 
|  |  |

##### Returns:

| Name | Type | 
| :--- | :--- |
| network protocol | int | 


```lua
GlobalVariables.NetworkProtocol()
--current network protocol
```


#### GlobalVariables.Client


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 
|  |  |

##### Returns:

| Name | Type | 
| :--- | :--- |
| are we client or stream | bool | 


```lua
GlobalVariables.Client()
```




[back to Contents](#-1)

---

## <a name="8"></a>InputSystem
---

#### InputSystem.IsKeyPressed


##### Parameters:

| Name | Type |
| :--- | :--- | 
| virtual key | int | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| is pressed | bool | 


```lua
InputSystem.IsKeyPressed(0x09) --vk_tab or tab key
--true if we are holding the tab key
```

#### InputSystem.IsKeyToggled


##### Parameters:

| Name | Type |
| :--- | :--- | 
| virtual key | int | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| did the key toggle | bool | 


```lua
InputSystem.IsKeyPressed(0x09) --vk_tab or tab key
--true if we are toggle the key [once]
```

#### InputSystem.GetCursorPosition


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| cursor position | Vector2D | 


```lua
InputSystem.GetCursorPosition() 
--mouse cursor position
```

#### InputSystem.MouseLeftState


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| mouse left state | float | 


```lua
InputSystem.MouseLeftState()
--value is 0 if clicked once or above 0 if being held down or -1 if not used
```

#### InputSystem.MouseRightState


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| mouse left state | float | 


```lua
InputSystem.MouseRightState()
--value is 0 if clicked once or above 0 if being held down or -1 if not used
```


[back to Contents](#-1)

---

## <a name="9"></a>Memory
---

#### Memory.FindSignature


##### Parameters:

| Name | Type |
| :--- | :--- | 
| module name | string | 
| signature | string |

##### Returns:

| Name | Type | 
| :--- | :--- |
| pointer | int | 


```lua
Memory.FindSignature("engine.dll", "53 56 57 8B DA 8B F9 FF 15")
--setclantag pointer
```

#### Memory.ReadPointerAsBool


##### Parameters:

| Name | Type |
| :--- | :--- | 
| pointer | unsigned int | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| value | bool | 


```lua
Memory.ReadPointerAsBool(pointer) --returns true or false
```

#### Memory.ReadPointerAsFloat


##### Parameters:

| Name | Type |
| :--- | :--- | 
| pointer | unsigned int | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| value | float | 


```lua
Memory.ReadPointerAsFloat(pointer) --returns a floating pointer number
```

#### Memory.ReadPointerAsInt


##### Parameters:

| Name | Type |
| :--- | :--- | 
| pointer | unsigned int | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| value | int | 


```lua
Memory.ReadPointerAsInt(pointer) --returns a integer
```


#### Memory.WritePointerAsBool


##### Parameters:

| Name | Type |
| :--- | :--- | 
| pointer | unsigned int | 
| new value | bool | 

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Memory.WritePointerAsBool(pointer, true)
```

#### Memory.WritePointerAsInt


##### Parameters:

| Name | Type |
| :--- | :--- | 
| pointer | unsigned int | 
| new value | int | 

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Memory.WritePointerAsInt(pointer, 5)
```

#### Memory.WritePointerAsFloat


##### Parameters:

| Name | Type |
| :--- | :--- | 
| pointer | unsigned int | 
| new value | float | 

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Memory.WritePointerAsFloat(pointer, 5.0)
```

#### Memory.GetModuleHandle


##### Parameters:

| Name | Type |
| :--- | :--- | 
| module name | string | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| handle | int | 


```lua
Memory.GetModuleHandle("engine.dll")
--handle or base address of engine.dll
```

#### Memory.GetProcessAddress


##### Parameters:

| Name | Type |
| :--- | :--- | 
| module name | string | 
| process name | string | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| process pointer | int | 


```lua
Memory.GetProcessAddress("vstdlib.dll", "RandomSeed")
--process address of RandomSeed
```


#### Memory.GetInterfaceAddress


##### Parameters:

| Name | Type |
| :--- | :--- | 
| module name | string | 
| interface version | string | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| interface pointer | int | 


```lua
Memory.GetInterfaceAddress("client.dll", "GameMovement001")
--gets the interface pointer of GameMovement001
```



[back to Contents](#-1)

---

## <a name="10"></a>Cvar
---

#### Cvar.FindCvar


##### Parameters:

| Name | Type |
| :--- | :--- | 
| cvar name | string | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| cvar | ConVar | 


```lua
local svcheats = Cvar.FindCvar("sv_cheats")
```

#### Cvar.IsValid


##### Parameters:

| Name | Type |
| :--- | :--- | 
| cvar | ConVar | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| isvalid | bool | 


```lua
local invalid = Cvar.FindCvar("invalidcvar")
Cvar.IsValid(invalid) --this will be false because the cvar doesnt exist
```

#### Cvar.InvalidCvar


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| invalid cvar value | ConVar | 


```lua
local invalid = Cvar.FindCvar("invalidcvar")
invalid == Cvar.InvalidCvar() --this will be true because the cvar doesnt exist
```

#### Cvar.GetString


##### Parameters:

| Name | Type |
| :--- | :--- | 
| cvar | ConVar | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| value | string | 


```lua
local svcheats = Cvar.FindCvar("sv_cheats")
Cvar.GetString(svcheats) --this will be "0" or "1"
```

#### Cvar.GetInt


##### Parameters:

| Name | Type |
| :--- | :--- | 
| cvar | ConVar | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| value | int | 


```lua
local svcheats = Cvar.FindCvar("sv_cheats")
Cvar.GetInt(svcheats) --this will be 0 or 1
```

#### Cvar.GetFloat


##### Parameters:

| Name | Type |
| :--- | :--- | 
| cvar | ConVar | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| value | float | 


```lua
local svcheats = Cvar.FindCvar("sv_cheats")
Cvar.GetFloat(svcheats) --this will be 0.0 or 1.0
```

#### Cvar.GetBool


##### Parameters:

| Name | Type |
| :--- | :--- | 
| cvar | ConVar | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| value | bool | 


```lua
local svcheats = Cvar.FindCvar("sv_cheats")
Cvar.GetBool(svcheats) --this will be true or false
```



[back to Contents](#-1)

---

## <a name="11"></a>AntiAim
---

#### AntiAim.IsInverted


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| inverter state | bool | 


```lua
AntiAim.IsInverted()
--true if inverted
```

#### AntiAim.GetRange


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| range | float | 


```lua
AntiAim.GetRange()
--between 0.0-120.0 depending on current desync range
```

#### AntiAim.SetAtTarget


##### Parameters:

| Name | Type |
| :--- | :--- | 
| | | 

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
AntiAim.SetAtTarget() --will set out base yaw at target if we use also use AntiAim.SetYaw
```

#### AntiAim.SetYaw


##### Parameters:

| Name | Type |
| :--- | :--- | 
| new yaw | double | 

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
AntiAim.SetYaw() --will set our yaw
```


#### AntiAim.SetLBY


##### Parameters:

| Name | Type |
| :--- | :--- | 
| new lower body target | int | 

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
AntiAim.SetLBY() --will set our lby target
-- 0 = "Offset"
-- 1 = "Extend"
-- 2 = "Preserve"
-- 3 = "Tank"
-- 4 = "Fake"
```

#### AntiAim.OnRun


##### Parameters:

| Name | Type |
| :--- | :--- | 
| callback | function | 

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
AntiAim.OnRun(function()
  --new antiaim overrides

end)
```

#### AntiAim.SetRange


##### Parameters:

| Name | Type |
| :--- | :--- | 
| overriden range | float | 

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
AntiAim.SetRange(90) --will set our desync range to 90/2 or 45
```

#### AntiAim.SetInverterState


##### Parameters:

| Name | Type |
| :--- | :--- | 
| new state | bool | 

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
AntiAim.SetInverterState(true) --will set our inverter to right instead of left
```


#### AntiAim.IsPeeking


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| is peeking | bool | 


```lua
AntiAim.IsPeeking()
--true if peeking
```



[back to Contents](#-1)

---

## <a name="12"></a>Client
---

#### Client.OnRender


##### Parameters:

| Name | Type |
| :--- | :--- | 
| function | function | 

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Client.OnRender(function()
   --render code
end)
```

#### Client.OnUnload


##### Parameters:

| Name | Type |
| :--- | :--- | 
| function | function | 

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Client.OnUnload(function()
   --on unload
end)
```


#### Client.ResetRender


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Client.OnRender(function()
  Client.ResetRender() --make sure to reset render!
   --render code
end)
```

#### Client.GetDelay


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| delay | float | 


```lua
Client.GetDelay()
--returns ping
```

#### Client.GetTime


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| time | string | 


```lua
Client.GetTime()
--returns time in string with format H:M:S
```


#### Client.GetUsername


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| username | string | 


```lua
Client.GetUsername()
--gives client username
```

#### Client.GetConnectedAddress


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| ip address | string | 


```lua
Client.GetConnectedAddress()
--gives currently connected IP address
```


#### Client.IsConnected


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| is connected to server | bool | 


```lua
Client.IsConnected()
--if true we are connected to a server
```

#### Client.IsInGame


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| is connected to server | bool | 


```lua
Client.IsInGame()
--if true we are in a game or match
```

#### Client.SetClantag


##### Parameters:

| Name | Type |
| :--- | :--- | 
| clantag | string | 
| clanname | string | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| | | 


```lua
Client.SetClantag("chimera", "chimera.uno")
--sets clantag
```

#### Client.TimeToTicks


##### Parameters:

| Name | Type |
| :--- | :--- | 
| time | float | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| ticks | int | 


```lua
Client.TimeToTicks(1.0)
--1 second to ticks
```

#### Client.TicksToTime


##### Parameters:

| Name | Type | 
| :--- | :--- |
| ticks | int |

##### Returns:

| Name | Type |
| :--- | :--- | 
| time | float | 


```lua
Client.TicksToTime(16)
--16 ticks to seconds
```

#### Client.GetBinds


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| active binds | table of strings | 


```lua
Client.GetBinds()
```

#### Client.GetBindsAnimation


##### Parameters:

| Name | Type |
| :--- | :--- | 
| index | int | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| modifier [0 - 255] | float 


```lua
Client.GetBindsAnimation(#Client.GetBinds() - 1)
```

#### Client.GetBindsType


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| active binds type | table of ints | 


```lua
Client.GetBindsType()
```


[back to Contents](#-1)

---

## <a name="13"></a>Fakelag
---

#### Fakelag.OverridePacket


##### Parameters:

| Name | Type |
| :--- | :--- | 
| new state | bool | 


##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Fakelag.OverridePacket(true)
--if true we will send packet if false we will not send packet
```

#### Fakelag.GetChokedPackets


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 


##### Returns:

| Name | Type | 
| :--- | :--- |
| Choked Packets | int | 


```lua
Fakelag.GetChokedPackets()
--ammount of choked packets
```

#### Fakelag.SendPacket


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 


##### Returns:

| Name | Type | 
| :--- | :--- |
| will send packet | bool | 


```lua
Fakelag.SendPacket() -- returns true if we will send a packet and will return false if we wont send a packet
--value depends on CreateMove call section (prediction, preprediction)
```


[back to Contents](#-1)

---

## <a name="14"></a>HTTP
---

#### HTTP.Post


##### Parameters:

| Name | Type |
| :--- | :--- | 
| URL | string | 
| Body | string | 
| Headers | table of strings |  

##### Returns:

| Name | Type | 
| :--- | :--- |
| response body | string | 


```lua
HTTP.Post("http://unknownwebsite.com/api/test", "test", {""})
```


#### HTTP.Get


##### Parameters:

| Name | Type |
| :--- | :--- | 
| URL | string | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| response body | string | 


```lua
HTTP.Get("http://unknownwebsite.com/get")
```

#### HTTP.IsConnected


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| is connected to internet | bool | 


```lua
HTTP.IsConnected()
--true if connected to the internet
```



[back to Contents](#-1)

---

## <a name="15"></a>HTTPS
---

#### HTTPS.Get


##### Parameters:

| Name | Type |
| :--- | :--- | 
| URL | string | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| response body | string | 



```lua
HTTPS.Get("http://unknownwebsite.com/get")
```

#### HTTPS.Post


##### Parameters:

| Name | Type |
| :--- | :--- | 
| URL | string | 
| Path | string | 
| Body | string | 
| Headers | string | 

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 



```lua
HTTPS.Post("https://unknownwebsite.com", "/Post","Body","Header: Header")
```

#### HTTPS.DownloadURLToFile


##### Parameters:

| Name | Type |
| :--- | :--- | 
| URL | string | 
| File | string | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| Successful | bool | 



```lua
HTTPS.Post("https://unknownwebsite.com", "/Post","Body","Header: Header")
```

#### HTTPS.IsConnected


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| is connected to internet | bool | 


```lua
HTTPS.IsConnected()
--true if connected to the internet
```


[back to Contents](#-1)

---

## <a name="16"></a>Menu
---

#### Menu.GetMainMenu


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| Main Menu Name | string | 


```lua
local MainMenuHandle = Menu.OpenMenu(Menu.GetMainMenu()) --Menu.GetMainMenu() returns the main menu name
```

#### Menu.InvalidHandle


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| invalid handle | int | 


```lua
Menu.InvalidHandle() -- it is equal to -5 or invalid handle
```


#### Menu.CreateMenu


##### Parameters:

| Name | Type |
| :--- | :--- | 
| Position | Vector2D | 
| Size | Vector2D | 
| Name | string | 
| Closable | bool | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| created menu handle | int | 


```lua
local NewHandle = Menu.CreateMenu(Vector2D.Get(40,40 + 170),Vector2D.Get(365,100),"New Menu", true) --example
```

#### Menu.OpenMenu


##### Parameters:

| Name | Type |
| :--- | :--- | 
| menu name | string | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| menu handle | int | 


```lua
local MainMenu = Menu.OpenMenu(Menu.GetMainMenu()) --open menu used to open main menu
```


#### Menu.OpenElement


##### Parameters:

| Name | Type |
| :--- | :--- | 
| tab | string | 
| child | string | 
| element | string | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| element handle | string | 


```lua
local FakelagMode = Menu.OpenElement( "AntiAim","Main", "Fakelag") --opens fakelag dropdown
```


#### Menu.CloseHandle


##### Parameters:

| Name | Type |
| :--- | :--- | 
| menu handle | int | 


##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Menu.CloseHandle(somemenu) --only use when closing menus
```


#### Menu.CreateSwitch


##### Parameters:

| Name | Type |
| :--- | :--- | 
| menu handle | int | 
| label | string | 
| default value | bool | 


##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Menu.CreateSwitch(SomeMenu,"SomeSwitch", false)
```


#### Menu.CreateSlider


##### Parameters:

| Name | Type |
| :--- | :--- | 
| menu handle | int | 
| label | string | 
| min | int |
| max | int |
| default value | int | 


##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Menu.CreateSlider(SomeMenu,"SomeSlider", 0,10,5)
```



#### Menu.CreateDropdown


##### Parameters:

| Name | Type |
| :--- | :--- | 
| menu handle | int | 
| label | string | 
| elements | table of strings |
| default value | int | 


##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Menu.CreateDropdown(SomeMenu,"SomeDropdown", { "1","2", "3","4"}, 0)
```


#### Menu.CreateMultidropdown


##### Parameters:

| Name | Type |
| :--- | :--- | 
| menu handle | int | 
| label | string | 
| elements | table of strings |
| default value | int | 


##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Menu.CreateMultidropdown(SomeMenu,"SomeDropdown", { "1","2", "3","4"}, 0)
```



[back to Contents](#-1)

---

## <a name="17"></a>Doubletap
---

#### Doubletap.GetSpeed


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| current speed | int | 


```lua
Doubletap.GetSpeed()
--doubletap speed
```

#### Doubletap.GetMode


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| current mode | int | 


```lua
Doubletap.GetMode()
--doubletap mode
```

#### Doubletap.GetTolerance


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| current tolerance | int | 


```lua
Doubletap.GetTolerance()
--returns overiden tolerance or 0 if not overiden
```


#### Doubletap.IsCharged


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| charge state | bool | 


```lua
Doubletap.IsCharged()
--true if doubletap is charged
```


#### Doubletap.SetMode

**Overrides for 1 tick**

##### Parameters:

| Name | Type |
| :--- | :--- | 
| new mode | int | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| | |


```lua
Doubletap.SetMode(0)
--sets doubletap mode to shift
```


#### Doubletap.SetSpeed

**Overrides for 1 tick**

##### Parameters:

| Name | Type |
| :--- | :--- | 
| new speed | int | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| | |


```lua
Doubletap.SetSpeed(15)
--doubletap speed will now be 15
```


#### Doubletap.SetTolerance

**Overrides for 1 tick**

##### Parameters:

| Name | Type |
| :--- | :--- | 
| new tolerance | int | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| | |


```lua
Doubletap.SetTolerance(3)
--doubletap tolerance will now be 3
```




[back to Contents](#-1)

---

## <a name="18"></a>EntityList
---

#### EntityList.NumberOfPlayers


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| number of players | int | 


```lua
EntityList.NumberOfPlayers()
```

#### EntityList.NumberOfEntities


##### Parameters:

| Name | Type |
| :--- | :--- | 
| include non networkable | bool | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| number of entities | int | 


```lua
EntityList.NumberOfEntities()
```


#### EntityList.GetHighestEntityIndex


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| highest entity index | int | 


```lua
EntityList.GetHighestEntityIndex()
```


#### EntityList.GetEntityFromHandle


##### Parameters:

| Name | Type |
| :--- | :--- | 
| handle | int | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| entity | CBasePlayer | 


```lua
EntityList.GetEntityFromHandle(somehandle)
```



#### EntityList.GetLocalPlayer


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| local player | CBasePlayer | 


```lua
EntityList.GetLocalPlayer()
```


#### EntityList.GetEntityFromUserID


##### Parameters:

| Name | Type |
| :--- | :--- | 
| user id | int | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| entity | CBasePlayer | 


```lua
EntityList.GetEntityFromUserID(SomeUserID)
```



#### EntityList.GetEntitiesByClassName


##### Parameters:

| Name | Type |
| :--- | :--- | 
| class name | string | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| entities | table of CBasePlayer | 


```lua
EntityList.GetEntitiesByClassName("CBasePlayer")
```


#### EntityList.GetEntitiesByClassID


##### Parameters:

| Name | Type |
| :--- | :--- | 
| class id | int | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| entities | table of CBasePlayer | 


```lua
EntityList.GetEntitiesByClassID(157) --smoke
```


#### EntityList.GetEntities


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| entities | table of CBasePlayer | 


```lua
EntityList.GetEntities()
```


#### EntityList.GetValidPlayers


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| entities | table of CBasePlayer | 


```lua
EntityList.GetValidPlayers()
```


#### EntityList.GetOpponents


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| entities | table of CBasePlayer | 


```lua
EntityList.GetOpponents()
```


#### EntityList.GetPlayers


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| entities | table of CBasePlayer | 


```lua
EntityList.GetPlayers()
```





[back to Contents](#-1)

---

## <a name="19"></a>Paint
---

#### Paint.OnRender


##### Parameters:

| Name | Type |
| :--- | :--- | 
| function | function | 

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Paint.OnRender(function()
   --render code
end)
```


#### **Only call on PaintTranverse**

#### Paint.Line


##### Parameters:

| Name | Type |
| :--- | :--- | 
| start | Vector2D | 
| end | Vector2D |
| color | Color |

##### Returns:

| Name | Type | 
| :--- | :--- |
| | | 


```lua
Paint.Line(Vector2D.Get(40,40), Vector2D.Get(60,40), Color.Default())
```


#### Paint.FilledRectangle


##### Parameters:

| Name | Type |
| :--- | :--- | 
| position | Vector2D | 
| size | Vector2D |
| color | Color |

##### Returns:

| Name | Type | 
| :--- | :--- |
| | | 


```lua
Paint.FilledRectangle(Vector2D.Get(40,40), Vector2D.Get(60,40), Color.Default())
```


#### Paint.Rectangle


##### Parameters:

| Name | Type |
| :--- | :--- | 
| position | Vector2D | 
| size | Vector2D |
| thickness | float |
| color | Color |

##### Returns:

| Name | Type | 
| :--- | :--- |
| | | 


```lua
Paint.Rectangle(Vector2D.Get(40,40), Vector2D.Get(60,40),1.5, Color.Default())
```


#### Paint.String


##### Parameters:

| Name | Type |
| :--- | :--- | 
| position | Vector2D | 
| text | string |
| color | Color |
| flags | PaintStringRenderFlags |
| font | CFont |

##### Returns:

| Name | Type | 
| :--- | :--- |
| | | 


```lua
Paint.String(Vector2D.Get(40,40), "test", Color.Default(),PaintStringRenderFlags.LEFT, 0)
```


#### Paint.AddFont


##### Parameters:

| Name | Type |
| :--- | :--- | 
| name | string |
| size | int |
| weight | int |
| flags | PaintFontCreationFlags |


##### Returns:

| Name | Type | 
| :--- | :--- |
| font | CFont | 


```lua
Paint.AddFont("Verdana", 30,400,PaintFontCreationFlags.Shadow)
```


#### Paint.ClearFonts


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  |
|  |  |
|  |  |
|  |  |


##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Paint.ClearFonts()
--clears fonts
```





[back to Contents](#-1)

---

## <a name="20"></a>Bits
---

#### Bits.has


##### Parameters:

| Name | Type |
| :--- | :--- | 
| bit | int | 
| bit | int |

##### Returns:

| Name | Type | 
| :--- | :--- |
| has | bool | 


```lua
local mustbetrue = Bits.has(48,16) --will be true
--this is the same as mustbetrue = 48 & 16 (C)
```


#### Bits.or


##### Parameters:

| Name | Type |
| :--- | :--- | 
| bit | int | 
| bit | int |

##### Returns:

| Name | Type | 
| :--- | :--- |
| newbit | int | 


```lua
local val = Bits.has(16,32) --will be 48
--this is the same as val = 16 | 32 (C)
```


#### Bits.remove


##### Parameters:

| Name | Type |
| :--- | :--- | 
| bit | int | 
| bit | int |

##### Returns:

| Name | Type | 
| :--- | :--- |
| removedbit | int | 


```lua
local val = Bits.remove(48,16) --will be 32
--this is the same as val = 48 & ~16 (C)
```



#### Bits.add


##### Parameters:

| Name | Type |
| :--- | :--- | 
| bit | int | 
| bit | int |

##### Returns:

| Name | Type | 
| :--- | :--- |
| added bit | int | 


```lua
local val = Bits.add(32,16) --will be 48
--this is the same as val = 32 | 16 (C)
```





[back to Contents](#-1)

---

## <a name="21"></a>Entity
---

#### Entity.GetPlayerInfo


##### Parameters:

| Name | Type |
| :--- | :--- | 
| Player | CBasePlayer | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| player info | PlayerInfo_t | 


```lua
Entity.GetPlayerInfo(EntityList.GetLocalPlayer())
--returns local player info
```

#### Entity.GetHandle


##### Parameters:

| Name | Type |
| :--- | :--- | 
| Player | CBasePlayer | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| handle | unsigned int | 


```lua
Entity.GetHandle(EntityList.GetLocalPlayer())
--returns local player handle
```


#### Entity.GetClassID


##### Parameters:

| Name | Type |
| :--- | :--- | 
| Player | CBasePlayer | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| classid | unsigned int | 


```lua
Entity.GetClassID(EntityList.GetLocalPlayer())
--returns local player class id [MUST BE CBASEPLAYER]
```


#### Entity.IsAlive


##### Parameters:

| Name | Type |
| :--- | :--- | 
| Player | CBasePlayer | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| alive | bool | 


```lua
Entity.IsAlive(EntityList.GetLocalPlayer())
--true if local player is alive
```

#### Entity.IsValidOpponent


**Checks for Dormancy and LifeState as well**

##### Parameters:

| Name | Type |
| :--- | :--- | 
| Player | CBasePlayer | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| valid opponent | bool | 


```lua
Entity.IsValidOpponent(EntityList.GetLocalPlayer())
--will be true because local player is not a valid opponent
```

#### Entity.IsDormant


##### Parameters:

| Name | Type |
| :--- | :--- | 
| Player | CBasePlayer | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| dormancy state | bool | 


```lua
Entity.IsDormant(EntityList.GetLocalPlayer())
--true if local player is dormant
```


#### Entity.GetRenderOrigin


##### Parameters:

| Name | Type |
| :--- | :--- | 
| Player | CBasePlayer | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| render origin | Vector | 


```lua
Entity.GetRenderOrigin(EntityList.GetLocalPlayer())
--if player is dormant it will return the last known origin
```


#### Entity.GetEyePosition


##### Parameters:

| Name | Type |
| :--- | :--- | 
| Player | CBasePlayer | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| eye position | Vector | 


```lua
Entity.GetEyePosition(EntityList.GetLocalPlayer())
--get local player eye position
```



#### Entity.GetBonePosition


##### Parameters:

| Name | Type |
| :--- | :--- | 
| Player | CBasePlayer | 
| bone | BoneID | 


##### Returns:

| Name | Type | 
| :--- | :--- |
| bone position | Vector | 


```lua
Entity.GetBonePosition(EntityList.GetLocalPlayer(), 0)
--get local player head position
```


#### Entity.GetEyeAngles


##### Parameters:

| Name | Type |
| :--- | :--- | 
| Player | CBasePlayer | 


##### Returns:

| Name | Type | 
| :--- | :--- |
| eye angles | Vector | 


```lua
Entity.GetEyeAngles(EntityList.GetLocalPlayer())
--get local player eye angles
```


#### Entity.GetVelocity


##### Parameters:

| Name | Type |
| :--- | :--- | 
| Player | CBasePlayer | 


##### Returns:

| Name | Type | 
| :--- | :--- |
| velocity | Vector | 


```lua
Entity.GetEyeAngles(EntityList.GetLocalPlayer())
--get local player velocity
```


#### Entity.GetEntityPointer


**Used for FFI**


##### Parameters:

| Name | Type |
| :--- | :--- | 
| Player | CBasePlayer | 


##### Returns:

| Name | Type | 
| :--- | :--- |
| Entity Pointer | int | 


```lua
Entity.GetEntityPointer(EntityList.GetLocalPlayer())
--get local player pointer
```

#### Entity.GetClassName


##### Parameters:

| Name | Type |
| :--- | :--- | 
| Player | CBasePlayer | 


##### Returns:

| Name | Type | 
| :--- | :--- |
| class name or networked name | string | 


```lua
Entity.GetClassName(EntityList.GetLocalPlayer())
--gets local player class name which will be CBasePlayer
```


#### Entity.GetPropAsBool


##### Parameters:

| Name | Type |
| :--- | :--- | 
| Player | CBasePlayer | 
| table | string |
| prop | string |


##### Returns:

| Name | Type | 
| :--- | :--- |
| property | bool | 


```lua
--usage
Entity.GetPropAsBool(someEntity, "DT_SomeTable", "m_bSomeBool")
```

#### Entity.GetPropAsVector


##### Parameters:

| Name | Type |
| :--- | :--- | 
| Player | CBasePlayer | 
| table | string |
| prop | string |


##### Returns:

| Name | Type | 
| :--- | :--- |
| propery | Vector | 


```lua
--usage
Entity.GetPropAsVector(someEntity, "DT_SomeTable", "m_vecSomeVector")
```


#### Entity.GetPropAsInt


##### Parameters:

| Name | Type |
| :--- | :--- | 
| Player | CBasePlayer | 
| table | string |
| prop | string |


##### Returns:

| Name | Type | 
| :--- | :--- |
| propery | int | 


```lua
--usage
Entity.GetPropAsInt(someEntity, "DT_SomeTable", "m_iSomeInt")
```


#### Entity.GetPropAsFloat


##### Parameters:

| Name | Type |
| :--- | :--- | 
| Player | CBasePlayer | 
| table | string |
| prop | string |


##### Returns:

| Name | Type | 
| :--- | :--- |
| propery | float | 


```lua
--usage
Entity.GetPropAsFloat(someEntity, "DT_SomeTable", "m_flSomeFloat")
```

#### Entity.SetPropAsFloat


##### Parameters:

| Name | Type |
| :--- | :--- | 
| Player | CBasePlayer | 
| table | string |
| prop | string |
| newvalue | float |


##### Returns:

| Name | Type | 
| :--- | :--- |
| successful | bool | 


```lua
--usage
Entity.SetPropAsFloat(someEntity, "DT_SomeTable", "m_flSomeFloat", 0.0)
```

#### Entity.SetPropAsInt


##### Parameters:

| Name | Type |
| :--- | :--- | 
| Player | CBasePlayer | 
| table | string |
| prop | string |
| newvalue | int |


##### Returns:

| Name | Type | 
| :--- | :--- |
| successful | bool | 


```lua
--usage
Entity.SetPropAsInt(someEntity, "DT_SomeTable", "m_iSomeInt", 0)
```

#### Entity.SetPropAsBool


##### Parameters:

| Name | Type |
| :--- | :--- | 
| Player | CBasePlayer | 
| table | string |
| prop | string |
| newvalue | bool |


##### Returns:

| Name | Type | 
| :--- | :--- |
| successful | bool | 


```lua
--usage
Entity.SetPropAsBool(someEntity, "DT_SomeTable", "m_bSomeBool", false)
```


#### Entity.SetPropAsVector


##### Parameters:

| Name | Type |
| :--- | :--- | 
| Player | CBasePlayer | 
| table | string |
| prop | string |
| newvalue | Vector |


##### Returns:

| Name | Type | 
| :--- | :--- |
| successful | bool | 


```lua
--usage
Entity.SetPropAsVector(someEntity, "DT_SomeTable", "m_vecSomeVector", Vector.Get(0,0,0))
```



[back to Contents](#-1)

---

## <a name="22"></a>Surface
---


#### Surface.OnRender


##### Parameters:

| Name | Type |
| :--- | :--- | 
| function | function | 

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Surface.OnRender(function()
   --render code
end)
```
### You may call on any callback

#### Surface.Triangle


##### Parameters:

| Name | Type |
| :--- | :--- | 
| point 1 | Vector2D | 
| point 2 | Vector2D |
| point 3 | Vector2D |
| color | Color |
| thickness | float |


##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Surface.Triangle(Vector2D.Get(30,30),Vector2D.Get(50,30), Vector2D.Get(50,50), Color.Get(255,255,255,255), 1.0)
```


#### Surface.FilledTriangle


##### Parameters:

| Name | Type |
| :--- | :--- | 
| point 1 | Vector2D | 
| point 2 | Vector2D |
| point 3 | Vector2D |
| color | Color |


##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Surface.FilledTriangle(Vector2D.Get(30,30),Vector2D.Get(50,30), Vector2D.Get(50,50), Color.Get(255,255,255,255))
```


#### Surface.Line


##### Parameters:

| Name | Type |
| :--- | :--- | 
| point 1 | Vector2D | 
| point 2 | Vector2D |
| color | Color |
| thickness | float |


##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Surface.Line(Vector2D.Get(30,30),Vector2D.Get(50,30), Color.Get(255,255,255,255), 1.0)
```


#### Surface.Rectangle


##### Parameters:

| Name | Type |
| :--- | :--- | 
| position | Vector2D | 
| size | Vector2D |
| color | Color |
| thickness | float |


##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Surface.Rectangle(Vector2D.Get(30,30),Vector2D.Get(50,30), Color.Get(255,255,255,255), 1.0)
```


#### Surface.FilledRectangle


##### Parameters:

| Name | Type |
| :--- | :--- | 
| position | Vector2D | 
| size | Vector2D |
| color | Color |



##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Surface.FilledRectangle(Vector2D.Get(30,30),Vector2D.Get(50,30), Color.Get(255,255,255,255))
```


#### Surface.GradientRectangle


##### Parameters:

| Name | Type |
| :--- | :--- | 
| position | Vector2D | 
| size | Vector2D |
| top left | Color |
| top right | Color |
| bottom left | Color |
| bottom right | Color |



##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Surface.GradientRectangle(Vector2D.Get(30,30),Vector2D.Get(50,30), Color.Get(255,255,255,0), Color.Get(255,255,255,255), Color.Get(255,255,255,0), Color.Get(255,255,255,255))
```


#### Surface.CircleFilled


##### Parameters:

| Name | Type |
| :--- | :--- | 
| position | Vector2D | 
| radius | float |
| color | Color |
| segments | int |


##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Surface.CircleFilled(Vector2D.Get(200,200),30.0,Color.Default(),20)
```

#### Surface.Texture


##### Parameters:

| Name | Type |
| :--- | :--- | 
| position | Vector2D | 
| size | Vector2D |
| color | Color |
| texture | ITexture |


##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
local texture = ITexture.SetTextureFromFile("C:\\texture.png")
Surface.Texture(Vector2D.Get(20,20), Vector2D.Get(200,200), Color.Default(), texture)
```


#### Surface.Circle


##### Parameters:

| Name | Type |
| :--- | :--- | 
| position | Vector2D | 
| radius | float |
| color | Color |
| thickness | float |


##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Surface.Circle(Vector2D.Get(200,200),30.0,Color.Default(),1.0)
```


#### Surface.CalculateText


##### Parameters:

| Name | Type |
| :--- | :--- | 
| text | string | 
| font | int |
| on get | function |


##### Returns:

| Name | Type | 
| :--- | :--- |
| Size of text | Vector2D | 


```lua
local sizex = 0
local sizey = 0

RegisterCallback(PaintTranverse(), function()
  Surface.CalculateText("text", function(x, y)
    sizex = x
    sizey = y
  end)
end)
```



#### Surface.Arc


##### Parameters:

| Name | Type |
| :--- | :--- | 
| position | Vector2D | 
| radius | float |
| color | Color |
| thickness | float |
| start angle [radian] | float |
| end angle [radian] | float |


##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Surface.Arc(Vector2D.Get(200,200),30.0,Color.Default(),1.0, 0, 3.14) --3.14 * 2 for a full circle
```


#### Surface.GradientCircle


##### Parameters:

| Name | Type |
| :--- | :--- | 
| position | Vector2D | 
| radius | float |
| inner | Color |
| outer | Color |


##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Surface.GradientCircle(Vector2D.Get(200,200),30.0,Color.Default(),Color.Get(255,255,255,0))
```


#### Surface.String


##### Parameters:

| Name | Type |
| :--- | :--- | 
| position | Vector2D | 
| color | Color |
| flags | SurfaceStringRenderFlags |
| text | string |
| font | IFont |


##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Surface.String(Vector2D.Get(200,200), Color.Get(255,255,255,255), SurfaceStringRenderFlags.NONE, "text", 0)
```



[back to Contents](#-1)

---

## <a name="23"></a>World
---

#### World.OnRender


##### Parameters:

| Name | Type |
| :--- | :--- | 
| function | function | 

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
World.OnRender(function()
   --render code
end)
```


### You may call on any Callback

#### World.Line

##### Parameters:

| Name | Type |
| :--- | :--- | 
| start | Vector | 
| end | Vector |
| color | Color |
| thickness | float |

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
World.Line(Vector.Get(100,0,0), Vector.Get(200,0,0), Color.Default(), 1.0)
```


#### World.GradientCircle


##### Parameters:

| Name | Type |
| :--- | :--- | 
| Origin | Vector | 
| Radius | float |
| Inner | Color |
| Outer | Color |


##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
World.GradientCircle(Vector.Get(100,0,0), 30.0, Color.Default(), Color.Default())
```


#### World.FilledCircle


##### Parameters:

| Name | Type |
| :--- | :--- | 
| Origin | Vector | 
| Radius | float |
| Color | Color |

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
World.FilledCircle(Vector.Get(100,0,0), 30.0, Color.Default())
```

#### World.FilledPyramid


##### Parameters:

| Name | Type |
| :--- | :--- | 
| Origin | Vector | 
| Radius | float |
| Height | float |
| Color | Color |

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
World.FilledPyramid(Vector.Get(100,0,0), 30.0, 20.0, Color.Default())
```

#### World.GradientPyramid


##### Parameters:

| Name | Type |
| :--- | :--- | 
| Origin | Vector | 
| Radius | float |
| Height | float |
| Inner | Color |
| Outer | Color |

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
World.GradientPyramid(Vector.Get(100,0,0), 30.0, 20.0, Color.Default(), Color.Default())
```

#### World.ToScreen


##### Parameters:

| Name | Type |
| :--- | :--- | 
| World | Vector | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| Screen | Vector2D | 


```lua
World.ToScreen(Vector.Get(100,0,0))
```

#### World.GlowLine


##### Parameters:

| Name | Type |
| :--- | :--- | 
| start | Vector | 
| end | Vector |
| color | Color |
| time | float |


##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
World.Line(Vector.Get(100,0,0), Vector.Get(200,0,0), Color.Default(), 1.0)
```


[back to Contents](#-1)

---

## <a name="24"></a>Console
---

#### Console.Print


##### Parameters:

| Name | Type |
| :--- | :--- | 
| text | string | 
| color | Color |

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Console.Print("text", Color.Default())
```


#### Console.Newline


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 
|  |  |

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Console.Newline()
--next line or new line
```



[back to Contents](#-1)

---

## <a name="25"></a>Sound
---

#### Sound.PlaySoundFromFile


##### Parameters:

| Name | Type |
| :--- | :--- | 
| path or file | string | 

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Sound.PlaySoundFromFile("C:\\Sounds\\AnimeUWU.wav")
```

#### Sound.PlaySoundFromFileInMemory


##### Parameters:

| Name | Type |
| :--- | :--- | 
| file in memory | table of bytes [unsigned char or unsigned int] | 

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Sound.PlaySoundFromFileInMemory(SomeFileInMemory)
```

#### Sound.Stop


##### Parameters:

| Name | Type |
| :--- | :--- | 
| |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Sound.Stop()
```


[back to Contents](#-1)

---

## <a name="26"></a>CreateMove
---


#### CreateMove.OnPrePrediction



##### Parameters:

| Name | Type |
| :--- | :--- | 
| Callback | function | 


##### Returns:

| Name | Type | 
| :--- | :--- |
| | | 


```lua
CreateMove.OnPrePrediction(function()


end)
```


#### CreateMove.OnPostPrediction



##### Parameters:

| Name | Type |
| :--- | :--- | 
| Callback | function | 


##### Returns:

| Name | Type | 
| :--- | :--- |
| | | 


```lua
CreateMove.OnPostPrediction(function()


end)
```


#### CreateMove.OnFinishPrediction



##### Parameters:

| Name | Type |
| :--- | :--- | 
| Callback | function | 


##### Returns:

| Name | Type | 
| :--- | :--- |
| | | 


```lua
CreateMove.OnFinishPrediction(function()


end)
```

#### CreateMove.OnRunCommand



##### Parameters:

| Name | Type |
| :--- | :--- | 
| Callback | function | 


##### Returns:

| Name | Type | 
| :--- | :--- |
| | | 


```lua
CreateMove.OnRunCommand(function()


end)
```

#### CreateMove.GetTickcount



##### Parameters:

| Name | Type |
| :--- | :--- | 
| | | 


##### Returns:

| Name | Type | 
| :--- | :--- |
| tickcount | int | 


```lua
CreateMove.GetTickcount()
```

#### CreateMove.GetViewAngles




##### Parameters:

| Name | Type |
| :--- | :--- | 
| | | 


##### Returns:

| Name | Type | 
| :--- | :--- |
| viewangles | Vector | 


```lua
CreateMove.GetViewAngles()
```


#### CreateMove.GetMovement



##### Parameters:

| Name | Type |
| :--- | :--- | 
| | | 


##### Returns:

| Name | Type | 
| :--- | :--- |
| movement | Vector | 


```lua
CreateMove.GetMovement()
```


#### CreateMove.GetAimDirection


##### Parameters:

| Name | Type |
| :--- | :--- | 
| | | 


##### Returns:

| Name | Type | 
| :--- | :--- |
| Aim Direction | Vector | 


```lua
CreateMove.GetAimDirection()
```


#### CreateMove.GetButtons



##### Parameters:

| Name | Type |
| :--- | :--- | 
| | | 


##### Returns:

| Name | Type | 
| :--- | :--- |
| Buttons | unsigned int | 


```lua
CreateMove.GetButtons()
```


#### CreateMove.GetCommandNumber



##### Parameters:

| Name | Type |
| :--- | :--- | 
| | | 


##### Returns:

| Name | Type | 
| :--- | :--- |
| Command Number | unsigned int | 


```lua
CreateMove.GetCommandNumber()
```

#### CreateMove.SetCommandNumber


##### Parameters:

| Name | Type |
| :--- | :--- | 
| new value | int | 


##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
CreateMove.SetCommandNumber(50)
```


#### CreateMove.SetButtons


##### Parameters:

| Name | Type |
| :--- | :--- | 
| new value | int | 


##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
CreateMove.SetButtons(0)
```


#### CreateMove.SetTickcount


##### Parameters:

| Name | Type |
| :--- | :--- | 
| new value | int | 


##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
CreateMove.SetTickcount(9999999)
```



#### CreateMove.SetViewAngles


##### Parameters:

| Name | Type |
| :--- | :--- | 
| new value | Vector | 


##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
CreateMove.SetViewAngles(Vector.Get(0,0,0))
```

#### CreateMove.SetMovement


##### Parameters:

| Name | Type |
| :--- | :--- | 
| new value | Vector | 


##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
CreateMove.SetMovement(Vector.Get(0,0,0))
```

#### CreateMove.SetAimDirection


##### Parameters:

| Name | Type |
| :--- | :--- | 
| new value | Vector | 


##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
CreateMove.SetAimDirection(Vector.Get(0,0,0))
```

#### CreateMove.IsPredicted



##### Parameters:

| Name | Type |
| :--- | :--- | 
| |  | 


##### Returns:

| Name | Type | 
| :--- | :--- |
| is predicted | bool | 


```lua
CreateMove.IsPredicted() 
```

#### CreateMove.SetPredicted



##### Parameters:

| Name | Type |
| :--- | :--- | 
| new value | bool | 


##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
CreateMove.SetPredicted(true)
```


[back to Contents](#-1)

---
## <a name="27"></a>FrameStageNotify
---

#### FrameStageNotify.Stage


##### **For FrameStageNotify**


##### Parameters:

| Name | Type |
| :--- | :--- | 
| | | 


##### Returns:

| Name | Type | 
| :--- | :--- |
| Frame Stage Notify Stage | Stages | 


```lua
FrameStageNotify.GetStage()
```

#### FrameStageNotify.On



##### Parameters:

| Name | Type |
| :--- | :--- | 
| Callback | function | 


##### Returns:

| Name | Type | 
| :--- | :--- |
| | | 


```lua
FrameStageNotify.On(function()


end)
```

[back to Contents](#-1)

---
## <a name="28"></a>PostScreenEffects
---


#### PostScreenEffects.On



##### Parameters:

| Name | Type |
| :--- | :--- | 
| Callback | function | 


##### Returns:

| Name | Type | 
| :--- | :--- |
| | | 


```lua
PostScreenEffects.On(function()


end)
```

[back to Contents](#-1)

---
## <a name="29"></a>OverrideView
---


#### OverrideView.On



##### Parameters:

| Name | Type |
| :--- | :--- | 
| Callback | function | 


##### Returns:

| Name | Type | 
| :--- | :--- |
| | | 


```lua
OverrideView.On(function()


end)
```

[back to Contents](#-1)

---
## <a name="30"></a>Animations
---


#### Animations.OnAnimationUpdate



##### Parameters:

| Name | Type |
| :--- | :--- | 
| Callback | function | 


##### Returns:

| Name | Type | 
| :--- | :--- |
| | | 


```lua
Animations.OnAnimationUpdate(function()


end)
```


#### Animations.OnResolve



##### Parameters:

| Name | Type |
| :--- | :--- | 
| Callback | function | 


##### Returns:

| Name | Type | 
| :--- | :--- |
| | | 


```lua
Animations.OnResolve(function()


end)
```

#### Animations.GetCurrentAnimationUpdatePlayer



##### Parameters:

| Name | Type |
| :--- | :--- | 
| | | 


##### Returns:

| Name | Type | 
| :--- | :--- |
| Entity | CBasePlayer | 


```lua
Animations.OnAnimationUpdate(function()
    local CurrentPlayer = Animations.GetCurrentAnimationUpdatePlayer()

end)
```

#### Animations.GetCurrentResolveUpdatePlayer



##### Parameters:

| Name | Type |
| :--- | :--- | 
| | | 


##### Returns:

| Name | Type | 
| :--- | :--- |
| Entity | CBasePlayer | 


```lua
Animations.OnResolve(function()
    local CurrentPlayer = Animations.GetCurrentResolveUpdatePlayer()

end)
```

#### Animations.SetGoalFeetYaw



##### Parameters:

| Name | Type |
| :--- | :--- | 
| GoalFeetYaw | float | 


##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Animations.OnResolve(function()
    local CurrentPlayer = Animations.GetCurrentResolveUpdatePlayer()

    Animations.SetGoalFeetYaw(math.random(-180, 180))
end)
```

#### Animations.SetYaw



##### Parameters:

| Name | Type |
| :--- | :--- | 
| Yaw | float | 


##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Animations.OnResolve(function()
    local CurrentPlayer = Animations.GetCurrentResolveUpdatePlayer()

    Animations.SetYaw(math.random(-180, 180))
end)
```

#### Animations.GetResolveData



##### Parameters:

| Name | Type |
| :--- | :--- | 
| | | 


##### Returns:

| Name | Type | 
| :--- | :--- |
| Resolve Data | ResolveData | 


```lua
Animations.OnResolve(function()
    local CurrentPlayer = Animations.GetCurrentResolveUpdatePlayer()
    local ResolveData = Animations.GetResolveData()
    Animations.SetYaw(ResolveData.Yaw + math.random(-60, 60))
end)
```

[back to Contents](#-1)

---

## <a name="31"></a>Vector
---

#### Members:

| Name | Type |
| :--- | :--- | 
| X | float | 
| Y | float |
| Z | float |

#### Vector.new

##### **Not recommended - Requires more memory then Vector.Get**

##### Parameters:

| Name | Type |
| :--- | :--- | 
| X | float | 
| Y | float |
| Z | float |

##### Returns:

| Name | Type | 
| :--- | :--- |
| Vector | Vector | 


```lua
local Vec = Vector.new(50,50,50)
```

#### Vector.Get

##### Parameters:

| Name | Type |
| :--- | :--- | 
| X | float | 
| Y | float |
| Z | float |

##### Returns:

| Name | Type | 
| :--- | :--- |
| Vector | Vector | 


```lua
local Vec = Vector.Get(50,50,50)
```

#### Vector.Default

##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 


##### Returns:

| Name | Type | 
| :--- | :--- |
| default | Vector | 


```lua
local Vec = Vector.Default()
```



#### Vector.Length

##### Parameters:

| Name | Type |
| :--- | :--- | 
| vector | Vector | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| Length | float | 


```lua
local Vec = Vector.Get(50,50,50)
local Length = Vector.Length(Vec)
```

#### Vector.Add

##### Parameters:

| Name | Type |
| :--- | :--- | 
| vector 1 | Vector | 
| vector 2 | Vector | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| Added | Vector | 


```lua
local Vec = Vector.Add(Vector.Get(0,0,50), Vector.Get(50,50,0))
```


#### Vector.Subtract

##### Parameters:

| Name | Type |
| :--- | :--- | 
| vector 1 | Vector | 
| vector 2 | Vector | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| Subtracted | Vector | 


```lua
local Vec = Vector.Subtract(Vector.Get(50,50,50), Vector.Get(50,50,50))
```


#### Vector.Multiply

##### Parameters:

| Name | Type |
| :--- | :--- | 
| vector 1 | Vector | 
| vector 2 | Vector | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| Multiplied | Vector | 


```lua
local Vec = Vector.Multiply(Vector.Get(5,5,5), Vector.Get(10,10,10))
```

#### Vector.Divide

##### Parameters:

| Name | Type |
| :--- | :--- | 
| vector 1 | Vector | 
| vector 2 | Vector | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| Divided | Vector | 


```lua
local Vec = Vector.Divide(Vector.Get(50,50,50), Vector.Get(10,10,10))
```




[back to Contents](#-1)

---

## <a name="32"></a>Vector2D
---

#### Members:

| Name | Type |
| :--- | :--- | 
| X | float | 
| Y | float |


#### Vector2D.new

##### **Not recommended - Requires more memory then Vector2D.Get**

##### Parameters:

| Name | Type |
| :--- | :--- | 
| X | float | 
| Y | float |

##### Returns:

| Name | Type | 
| :--- | :--- |
| val | Vector2D | 

```lua
local vec2 = Vector2D.new(20,20)
```

#### Vector2D.Get


##### Parameters:

| Name | Type |
| :--- | :--- | 
| X | float | 
| Y | float |

##### Returns:

| Name | Type | 
| :--- | :--- |
| val | Vector2D | 

```lua
local vec2 = Vector2D.Get(20,20)
```

#### Vector2D.Default()


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| default | Vector2D | 

```lua
local default = Vector2D.Default()
```


#### Vector2D.Add


##### Parameters:

| Name | Type |
| :--- | :--- | 
| first | Vector2D | 
| second | Vector2D | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| Added | Vector2D | 

```lua
local vec2 = Vector2D.Add(Vector2D.Get(20,20), Vector2D.Get(40,0))
```


#### Vector2D.Subtract


##### Parameters:

| Name | Type |
| :--- | :--- | 
| first | Vector2D | 
| second | Vector2D | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| Subtracted | Vector2D | 

```lua
local vec2 = Vector2D.Subtract(Vector2D.Get(20,20), Vector2D.Get(10,10))
```



[back to Contents](#-1)

---

## <a name="33"></a>Color
---

#### Color.Default


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| default | Color | 


```lua
Color.Default()
```

#### Color.new

##### **Not recommended - Requires more memory then Color.Get**

##### Parameters:

| Name | Type |
| :--- | :--- | 
| R | float | 
| G | float | 
| B | float | 
| A [Optional] | float | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| color | Color | 


```lua
Color.new(255,255,100) 
Color.new(255,255,100,255)
```

#### Color.Get


##### Parameters:

| Name | Type |
| :--- | :--- | 
| R | float | 
| G | float | 
| B | float | 
| A | float | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| color | Color | 


```lua
Color.Get(255,255,100,255)
```


[back to Contents](#-1)

---

## <a name="34"></a>CGameTrace
---

#### Members:

| Name | Type |
| :--- | :--- | 
| fraction | float | 
| fractionleftsolid | float |
| hitbox | int |
| hitgroup | int |
| physicsbone | short |
| worldsurfaceindex | short |
| startpos | Vector |
| endpos | Vector |
| contents | int |
| dispflags | short |
| allsolid | bool |
| startsolid | bool |
| hitentity | CBasePlayer |


##### hitentity is -1 if it did not hit a entity


[back to Contents](#-1)

---

## <a name="35"></a>PlayerInfo_t
---

#### Members:

| Name | Type |
| :--- | :--- | 
| IsBot | bool | 
| IsHLTV | bool |
| Name | string |
| SteamID | int |
| UserID | int |

[back to Contents](#-1)

---

## <a name="36"></a>ResolveData
---

#### Members:

| Name | Type |
| :--- | :--- | 
| Yaw | float | 
| GoalFeetYaw | float |
| CurrentPlayer | CBasePlayer |


[back to Contents](#-1)

---

## <a name="37"></a>PaintStringRenderFlags
---

#### Type definition int PaintStringRenderFlags

#### Enumeration:

| Name | Value |
| :--- | :--- | 
| LEFT | 0 | 
| RIGHT | 1 |
| CENTER | 2 |


[back to Contents](#-1)

---

## <a name="38"></a>SurfaceStringRenderFlags
---

#### Type definition int SurfaceStringRenderFlags

#### Enumeration:

| Name | Value |
| :--- | :--- | 
| NONE | 0 | 
| OUTLINE | 1 |
| CENTEREDX | 2 |
| CENTEREDY | 4 |


[back to Contents](#-1)

---

## <a name="39"></a>PaintFontCreationFlags
---

#### Type definition int PaintFontCreationFlags

#### Enumeration:

| Name | Value |
| :--- | :--- | 
| NONE | 0 | 
| ITALIC | 1 |
| UNDERLINE | 2 |
| STRIKEOUT | 4 |
| SYMBOL | 8 |
| ANTIALIAS | 16 |
| BLUR | 32 |
| ROTARY | 64 |
| SHADOW | 128 |
| ADDITIVE | 256 |
| OUTLINE | 512 |
| CUSTOM | 1024 |
| BITMAP | 2048 |


[back to Contents](#-1)

---

## <a name="40"></a>Stages
---

#### Type definition int Stages

#### Enumeration:

| Name | Value |
| :--- | :--- | 
| FRAME_UNDEFINED | -1 |
| FRAME_START | 0 | 
| FRAME_NET_UPDATE_START | 1 |
| FRAME_NET_UPDATE_POSTDATAUPDATE_START | 2 |
| FRAME_NET_UPDATE_POSTDATAUPDATE_END | 3 |
| FRAME_NET_UPDATE_END | 4 |
| FRAME_RENDER_START | 5 |
| FRAME_RENDER_END | 6 |



[back to Contents](#-1)

---

## <a name="41"></a>CBasePlayer
---

#### Type definition int CBasePlayer

[back to Contents](#-1)

---

## <a name="42"></a>Virtual Key
---

#### Type definition int Virtual Key

[back to Contents](#-1)

---

## <a name="43"></a>ConVar
---

#### Type definition int ConVar

[back to Contents](#-1)

---

## <a name="44"></a>CFont
---

#### Type definition int CFont

[back to Contents](#-1)

---

## <a name="45"></a>IFont
---

#### Type definition int IFont

[back to Contents](#-1)

---

## <a name="46"></a>BoneID
---

#### Type definition int BoneID


```cpp
[NOT ENUMERATION]
Values:
0 = head 
1 = neck 
2 = pelvis 
3 = body 
4 = thorax
5 = chest
6 = upper chest
7 = left thigh
8 = right thigh
9 = left calf
10 = right calf
11 = left foot
12 = right foot
```

[back to Contents](#-1)

---

## <a name="47"></a>Print
---

#### Print


##### Parameters:

| Name | Type |
| :--- | :--- | 
| text | string | 

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Print("text")
```



[back to Contents](#-1)

---
## <a name="48"></a>ITexture
---

#### ITexture.new


##### Parameters:

| Name | Type |
| :--- | :--- | 
| | | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| texture | ITexture | 


```lua
local texture = ITexture.new()
```


#### ITexture.Get


##### Parameters:

| Name | Type |
| :--- | :--- | 
| | | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| texture | ITexture | 


```lua
local texture = ITexture.Get()
```


#### ITexture.SetTextureFromFile


##### Parameters:

| Name | Type |
| :--- | :--- | 
| file path | string | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| texture | ITexture | 


```lua
local texture = ITexture.SetTextureFromFile("C:\\Texture.png")
```



[back to Contents](#-1)

---

## <a name="49"></a>Lua
---

#### Lua.Run


##### Parameters:

| Name | Type |
| :--- | :--- | 
| script | string | 

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Lua.Run("Print("test")")
```

#### Lua.File


##### Parameters:

| Name | Type |
| :--- | :--- | 
| script path | string | 

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Lua.File("C:\\CustomScripts\\Test.lua")
```



#### Lua.Error


##### Parameters:

| Name | Type |
| :--- | :--- | 
| error | string | 

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Lua.Error("threw script error [this will unload script]")
```


#### Lua.Unload


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Lua.Unload() --unloads ourself 
```


[back to Contents](#-1)

---
## <a name="50"></a>Rage
---


#### Rage.OnScan


##### Parameters:

| Name | Type |
| :--- | :--- | 
| Callback | function | 

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
Rage.OnScan(function()
--inside callback
  Rage.ForceBaim()
end)
```

#### Rage.Target


##### Parameters:

| Name | Type |
| :--- | :--- | 
| | | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| Target | CBasePlayer | 


```lua
Rage.OnScan(function()
  Print(Rage.Target()) --will print the current ragebot target
end)
```

#### Rage.ForceBaim


##### Parameters:

| Name | Type |
| :--- | :--- | 
| | | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| | | 


```lua
Rage.OnScan(function()
  Rage.ForceBaim() --force baim on target
end)
```

#### Rage.SetScannedHitboxes


##### Parameters:

| Name | Type |
| :--- | :--- | 
| overriden hitbox | unsigned int | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| | | 


```lua
Rage.OnScan(function()
  Rage.SetScannedHitboxes(1) --forces head hitbox
  --16 - stomach
  --32 - pelvis
  --8 - chest
  --4 - upper chest
  --2 - neck
  --1 - head
  --128 - thighs
  --256 - foot
	--NOTE: use bit library
end)
```

#### Rage.SetScannedDamage


##### Parameters:

| Name | Type |
| :--- | :--- | 
| new minimum damage | int | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| | | 


```lua
Rage.OnScan(function()
  Rage.SetScannedDamage(10)
end)
```



[back to Contents](#-1)

---

---
## <a name="51"></a>PacketManager
---



#### PacketManager.SetRealPackets


##### Parameters:

| Name | Type |
| :--- | :--- | 
| New Real Packets | int | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| | | 


```lua
--NOTE MUST ALWAYS BE POSITIVE
PacketManager.SetRealPackets(16) --sets our sent real packets to 16
```

#### PacketManager.GetRealPackets


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| New Real Packets | int | 


```lua
PacketManager.GetRealPackets() --returns our sent real packets as int
```

#### PacketManager.SetFakePackets


##### Parameters:

| Name | Type |
| :--- | :--- | 
| New Fake Packets | int | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| | | 


```lua
--NOTE: MUST ALWAYS BE POSITIVE
PacketManager.SetFakePackets(16) --sets our sent fake packets to 16
```

#### PacketManager.GetFakePackets


##### Parameters:

| Name | Type |
| :--- | :--- | 
|  |  | 

##### Returns:

| Name | Type | 
| :--- | :--- |
| New Fake Packets | int | 


```lua
PacketManager.GetFakePackets() --returns our sent fake packets as int
```

#### PacketManager.ShiftTickbase


##### Parameters:

| Name | Type |
| :--- | :--- | 
| Shifted Ticks | int | 

##### Returns:

| Name | Type | 
| :--- | :--- |
|  |  | 


```lua
--MAY BE POSITIVE OR NEGATIVE DEPENDING ON CONTEXT
--NEGATIVE: SKIP TICKSBASE
--POSITIVE: SHIFT TICKBASE
PacketManager.ShiftTickbase(-16) --Skips our tickbase by 16
PacketManager.ShiftTickbase(16) --Shifts our tickbase by 16
```



[back to Contents](#-1)

---
