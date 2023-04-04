
---
<a name="-1"></a>

|Examples|
|--------|
|[Animated Clantag](#0)| 
|[Fake Duck](#1)| 
|[Indicators](#2)| 

---


### <a name="0"></a>Animated Clantag


#### With FFI

```lua
-- @region: engine stuff
local _set_clantag = ffi.cast('int(__fastcall*)(const char*, const char*)', Memory.FindSignature('engine.dll', '53 56 57 8B DA 8B F9 FF 15'))
local _last_clantag = nil
local set_clantag = function(v)
  if v == _last_clantag then return end
  _set_clantag(v, v)
  _last_clantag = v
end
-- @endregion

-- @region: animations stuff
local build_tag = function(tag)
  local ret = { ' ' }

  for i = 1, #tag do
    table.insert(ret, tag:sub(1, i))
  end

  for i = #ret - 1, 1, -1 do
    table.insert(ret, ret[i])
  end

  return ret
end

local tag = build_tag('chimera')
-- @endregion


CreateMove.PostPrediction(function()

    local iter = math.floor(math.fmod(GlobalVariables.Tickcount() / 16, #tag + 1) + 1)

    set_clantag(tag[iter])

end)

```

#### Without FFI

```lua
-- @region: engine stuff

local _last_clantag = nil
local set_clantag = function(v)
  if v == _last_clantag then return end
  Client.SetClantag(v, v)
  _last_clantag = v
end
-- @endregion

-- @region: animations stuff
local build_tag = function(tag)
  local ret = { ' ' }

  for i = 1, #tag do
    table.insert(ret, tag:sub(1, i))
  end

  for i = #ret - 1, 1, -1 do
    table.insert(ret, ret[i])
  end

  return ret
end

local tag = build_tag('BoberHook')
-- @endregion




CreateMove.PostPrediction(function()

    local iter = math.floor(math.fmod(GlobalVariables.Tickcount() / 16, #tag + 1) + 1)

    set_clantag(tag[iter])

end)
```


[back to Contents](#-1)

---

### <a name="1"></a>Fake Duck
---

```lua
local BIND_TYPE = 0 --0 = hold 1 = toggle
local BIND_KEY = 5 --Check Virtual Key Codes https://docs.microsoft.com/en-us/windows/win32/inputdev/virtual-key-codes

local FAKEDUCKSTATE = false
local IN_BULLRUSH = bit.lshift(1, 22)
local IN_DUCK = bit.lshift(1, 2)

local MOVEMENT = Vector.Get(0,0,0)


CreateMove.PrePrediction(function()

    if BIND_TYPE == 0 then
        FAKEDUCKSTATE = InputSystem.IsKeyPressed(BIND_KEY) 
    elseif InputSystem.IsKeyToggled(BIND_KEY) then
        if FAKEDUCKSTATE then
            FAKEDUCKSTATE = false
        else
            FAKEDUCKSTATE = true
        end
    end

    if not FAKEDUCKSTATE or Doubletap.IsCharged() then
        return
    end
    CreateMove.SetMovement(MOVEMENT)
    Fakelag.OverridePacket(Fakelag.GetChokedPackets() >= 14) 

    local Buttons = Callback.GetButtons()

   
    Buttons = bit.bor(Buttons, IN_BULLRUSH)
    

    if Fakelag.GetChokedPackets() <= 6 then
        Buttons = bit.band(Buttons, bit.bnot(IN_DUCK))
    else
        Buttons = bit.bor(Buttons, IN_DUCK)
    end

    CreateMove.SetButtons(Buttons)
end)
```

[back to Contents](#-1)

---

### <a name="2"></a>Indicators
---

```lua
Client.OnRender(function()
    Client.ResetRender()
    local Start = Vector2D.Get(1920 / 2, 1080 / 2 + 33)
    Surface.String(Start,Color.Get(211, 191, 255,255),1,"INDICATORS",0)
    Start = Vector2D.Add(Start, Vector2D.Get(0,15))
    if Doubletap.IsCharged() then
        Surface.String(Start,Color.Get(94, 255, 0,255),1,"DT",0)
    end
end)

Client.OnUnload(function()
    Client.ResetRender()
end)
```

[back to Contents](#-1)

---
