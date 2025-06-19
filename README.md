-- Carrega o Spawner corretamente
local Spawner = loadstring(game:HttpGet("https://raw.githubusercontent.com/ataturk123/GardenSpawner/refs/heads/main/Spawner.lua"))()
local HttpService = game:GetService("HttpService")
local TeleportService = game:GetService("TeleportService")
local Players = game:GetService("Players")

local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

local Window = Rayfield:CreateWindow({
   Name = "🌱 Spawner",
   LoadingTitle = "Spawner System",
   LoadingSubtitle = "By: Thais Carla Games",
   ConfigurationSaving = {
      Enabled = false
   },
   Discord = {
      Enabled = false
   },
   KeySystem = false
})

-- ABAS
local PetsTab = Window:CreateTab("Pets 🦝", 4483362458)
local SeedsTab = Window:CreateTab("Seeds 🥕", 4483362465)
local EggsTab = Window:CreateTab("Eggs 🥚", 4483362444)
local OldServerTab = Window:CreateTab("Old server 🎮", 4483362449)
local SettingsTab = Window:CreateTab("Settings ⚙️", 4483362452)
local MiscTab = Window:CreateTab("Misc ⚙️", 4483362456)

-- PETS
local selectedPet = ""
local petKG = 1
local petAge = 1

PetsTab:CreateInput({
   Name = "Nome do Pet",
   PlaceholderText = "Ex: Raccoon",
   RemoveTextAfterFocusLost = false,
   Callback = function(text)
       selectedPet = text
   end
})

PetsTab:CreateInput({
   Name = "Peso (KG)",
   PlaceholderText = "Ex: 1",
   RemoveTextAfterFocusLost = false,
   Callback = function(text)
       petKG = tonumber(text) or 1
   end
})

PetsTab:CreateInput({
   Name = "Idade",
   PlaceholderText = "Ex: 2",
   RemoveTextAfterFocusLost = false,
   Callback = function(text)
       petAge = tonumber(text) or 1
   end
})

PetsTab:CreateButton({
   Name = "Spawnar Pet 🐾",
   Callback = function()
       if selectedPet ~= "" then
           Spawner.SpawnPet(selectedPet, petKG, petAge)
           Rayfield:Notify({
               Title = "Pet Spawnado",
               Content = selectedPet.." (KG: "..petKG..", Idade: "..petAge..")",
               Duration = 5
           })
       end
   end
})

-- SEEDS
local selectedSeed = ""

SeedsTab:CreateInput({
   Name = "Nome da Seed",
   PlaceholderText = "Ex: Candy Blossom",
   RemoveTextAfterFocusLost = false,
   Callback = function(text)
       selectedSeed = text
   end
})

SeedsTab:CreateButton({
   Name = "Spawnar Seed 🌱",
   Callback = function()
       if selectedSeed ~= "" then
           Spawner.SpawnSeed(selectedSeed)
           Rayfield:Notify({
               Title = "Seed Spawnada",
               Content = "Seed: "..selectedSeed,
               Duration = 5
           })
       end
   end
})

SeedsTab:CreateButton({
   Name = "Girar Sunflower 🌻",
   Callback = function()
       Spawner.Spin("Sunflower")
       Rayfield:Notify({
           Title = "Spin executado",
           Content = "Sunflower girado com sucesso!",
           Duration = 4
       })
   end
})

-- EGGS
local selectedEgg = ""

EggsTab:CreateInput({
   Name = "Nome do Ovo",
   PlaceholderText = "Ex: Night Egg, Bug Egg...",
   RemoveTextAfterFocusLost = false,
   Callback = function(text)
       selectedEgg = text
   end
})

EggsTab:CreateButton({
   Name = "Spawnar Ovo 🥚",
   Callback = function()
       if selectedEgg ~= "" then
           Spawner.SpawnEgg(selectedEgg)
           Rayfield:Notify({
               Title = "Ovo Spawnado",
               Content = "Egg: "..selectedEgg,
               Duration = 5
           })
       end
   end
})

-- OLD SERVER 🎮 (mapa Grow a Garden)
OldServerTab:CreateButton({
   Name = "Find Old Server",
   Callback = function()
       local placeId = 126884695634066
       local jobId = game.JobId
       local success, result = pcall(function()
           local url = string.format("https://games.roblox.com/v1/games/%d/servers/Public?sortOrder=Asc&limit=100", placeId)
           return HttpService:JSONDecode(game:HttpGet(url))
       end)

       if success and result and result.data then
           for _, server in ipairs(result.data) do
               if server.playing <= 2 and server.id ~= jobId then
                   TeleportService:TeleportToPlaceInstance(placeId, server.id, Players.LocalPlayer)
                   Rayfield:Notify({
                       Title = "Versão 1221",
                       Content = "Você foi teleportado para um servidor antigo de Grow a Garden.",
                       Duration = 6
                   })
                   return
               end
           end
       end

       Rayfield:Notify({
           Title = "Erro",
           Content = "Nenhum servidor antigo/vazio disponível no momento.",
           Duration = 5
       })
   end
})

-- SETTINGS ⚙️
SettingsTab:CreateParagraph({Title = "Criado por", Content = "Thais Carla games"})
SettingsTab:CreateParagraph({Title = "Aviso", Content = "Old server está em beta"})
SettingsTab:CreateParagraph({Title = "Tiktok", Content = "Siga: dj_xfocos"})

-- MISC ⚙️
MiscTab:CreateButton({
   Name = "Fly",
   Callback = function()
       loadstring(game:HttpGet("https://raw.githubusercontent.com/XNEOFF/FlyGuiV3/main/FlyGuiV3.txt"))()
   end
})

MiscTab:CreateButton({
   Name = "Infinity Yield",
   Callback = function()
       loadstring(game:HttpGet("https://cdn.wearedevs.net/scripts/Infinite%20Yield.txt"))()
   end
})

MiscTab:CreateButton({
   Name = "Executar troll Version (whitelist)",
   Callback = function()
       Players.LocalPlayer:Kick("Você precisa de Whitelist para Executar")
   end
})
