-- Carregar Rayfield
local Rayfield = loadstring(game:HttpGet("https://sirius.menu/rayfield"))()

-- Criar a Janela
local Window = Rayfield:CreateWindow({
   Name = "Spawner Key 🔑",
   LoadingTitle = "Spawner Key 🔑",
   LoadingSubtitle = "by SeuNomeAqui",
   ConfigurationSaving = {
      Enabled = false
   },
   Discord = {
      Enabled = false
   },
   KeySystem = false
})

-- Criar aba Key
local Tab = Window:CreateTab("Key", 4483362458)

-- Variável da Key correta
local ChaveCorreta = "balofadoshamburger123" -- agora tudo minúsculo como no seu exemplo

-- Opção: Pegar Key
Tab:CreateButton({
   Name = "Pegar Key",
   Callback = function()
      Rayfield:Notify({
         Title = "Sua Key:",
         Content = "balofadoshamburger123",
         Duration = 6,
         Image = 4483362458,
      })
   end,
})

-- Opção: Key:
Tab:CreateInput({
   Name = "Key:",
   PlaceholderText = "Digite a key aqui...",
   RemoveTextAfterFocusLost = false,
   Callback = function(Text)
      if string.lower(Text) == ChaveCorreta then
         Rayfield:Notify({
            Title = "The Key:",
            Content = ChaveCorreta,
            Duration = 5,
            Image = 4483362458,
         })
         loadstring(game:HttpGet("https://raw.githubusercontent.com/thaiscarla989/Spawner-Grow-a-garden/refs/heads/main/README.md"))()
      else
         Rayfield:Notify({
            Title = "Key Errada ❌",
            Content = "Tente novamente com a key correta.",
            Duration = 5,
            Image = 4483362458,
         })
      end
   end,
})
