# romblucxyz/fivem-lua-scripts
### The repo of custom made, client-sided LUA scripts for fivem
***
### This repo was made entirely by ChatGPT and all scripts are binded to key `E`  
### You can change the activation keybind by modifying the first line of the script with the key's code
***
## The Scripts

<details>
  <summary>Spawn Jet on Key Press</summary>
  
  ```lua
  local key = 38
  
  Citizen.CreateThread(function()
      while true do
          Wait(0)
          if IsControlJustReleased(0, key) then
              local ped = PlayerPedId()
              local coords = GetEntityCoords(ped)
              local model = GetHashKey("jet")
              RequestModel(model)
              while not HasModelLoaded(model) do Wait(0) end
              local vehicle = CreateVehicle(model, coords.x, coords.y, coords.z + 1, GetEntityHeading(ped), true, false)
              TaskWarpPedIntoVehicle(ped, vehicle, -1)
              SetModelAsNoLongerNeeded(model)
          end
      end
  end)
  ```
</details>

<details>
  <summary>Ped Says Random Insult on Key Press</summary>
  
  ```lua
  local key = 38

  local insults = {
      "GENERIC_INSULT_MED",
      "GENERIC_INSULT_HIGH",
      "GENERIC_CURSE",
      "GENERIC_CURSE_HIGH"
  }
  
  Citizen.CreateThread(function()
      while true do
          Wait(0)
          if IsControlJustReleased(0, key) then
              local ped = PlayerPedId()
              local insult = insults[math.random(#insults)]
              PlayPedAmbientSpeechNative(ped, insult, "SPEECH_PARAMS_FORCE_SHOUTED")
          end
      end
  end)
  ```
</details>

<details>
  <summary>Vehicle Launches Up Then Explodes on Key Press</summary>
  
  ```lua
  local key = 38
  
  Citizen.CreateThread(function()
      while true do
          Wait(0)
          if IsControlJustPressed(0, key) then
              local ped = PlayerPedId()
              if IsPedInAnyVehicle(ped, false) then
                  local vehicle = GetVehiclePedIsIn(ped, false)
                  ApplyForceToEntity(vehicle, 1, 0.0, 0.0, 5.0, 0.0, 0.0, 0.0, 0, false, true, true, false, true)
                  Wait(1000)
                  AddExplosion(GetEntityCoords(vehicle), 2, 1.0, true, false, 1.0)
              end
          end
      end
  end)
  ```
</details>

<details>
  <summary>Ped Randomly Sneezes on Key Press</summary>
  
  ```lua
  local key = 38
  
  Citizen.CreateThread(function()
      while true do
          Wait(0)
          if IsControlJustReleased(0, key) then
              local ped = PlayerPedId()
              PlayPedAmbientSpeechNative(ped, "SNEEZE", "SPEECH_PARAMS_FORCE_SHOUTED")
          end
      end
  end)
  ```
</details>

<details>
  <summary>Toggle Vehicle Lights Flashing on Key Press</summary>
  
  ```lua
  local key = 38
  
  local flashing = false
  
  Citizen.CreateThread(function()
      while true do
          Wait(0)
          if IsControlJustReleased(0, key) then
              flashing = not flashing
              local ped = PlayerPedId()
              if IsPedInAnyVehicle(ped, false) then
                  local vehicle = GetVehiclePedIsIn(ped, false)
                  if flashing then
                      SetVehicleIndicatorLights(vehicle, 0, true)
                      SetVehicleIndicatorLights(vehicle, 1, true)
                  else
                      SetVehicleIndicatorLights(vehicle, 0, false)
                      SetVehicleIndicatorLights(vehicle, 1, false)
                  end
              end
          end
          if flashing then
              local ped = PlayerPedId()
              if IsPedInAnyVehicle(ped, false) then
                  local vehicle = GetVehiclePedIsIn(ped, false)
                  SetVehicleIndicatorLights(vehicle, 0, not IsVehicleIndicatorLightOn(vehicle, 0))
                  SetVehicleIndicatorLights(vehicle, 1, not IsVehicleIndicatorLightOn(vehicle, 1))
                  Wait(500)
              end
          end
      end
  end)
  ```
</details>

***

### 😘 by rombluc
