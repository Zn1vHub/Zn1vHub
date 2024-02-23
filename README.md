local remote = game:GetService("ReplicatedStorage"):WaitForChild("Events")
local rmt = game:GetService("ReplicatedStorage").Events
local cd = 0.01

getgenv().zniv_Click = true
getgenv().zniv_Win = true
getgenv().zniv_Hatch = true
getgenv().zniv_Equipment = true

function tap()
  spawn(function()
    while getgenv().zniv_Click do
      remote:WaitForChild("DamageIncreaseOnClickEvent"):FireServer()
      task.wait(cd)
    end
  end)
end

function xp()
  spawn(function()
    while getgenv().zniv_Exp do
      remote:WaitForChild("PlayerDefeatedTrainingDummy"):FireServer(selectedDummies)
      task.wait(cd)
    end
  end)
end

function win()
  spawn(function()
    while getgenv().zniv_Win do
      remote:WaitForChild("EndBattle"):FireServer(game:GetService("Players").LocalPlayer)
      task.wait(cd)
    end
  end)
end

function hatch(selectedEgg)
  spawn(function()
    while wait() do
      if not getgenv().zniv_Egg then break end
      remote:WaitForChild("PlayerPressedKeyOnEgg"):FireServer(selectedEgg)
      task.wait(cd)
    end
  end)
end

function craft(selectedEquipment)
  spawn(function()
    while getgenv().zniv_Craft do
      rmt.CraftingEvent:FireServer(selectedEquipment)
      task.wait(cd)
    end
  end)
end

local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
local SaveManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/SaveManager.lua"))()
local InterfaceManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/InterfaceManager.lua"))()

local Window = Fluent:CreateWindow({
    Title = "Pet Adventure",
    SubTitle = "Zniv Hub",
    TabWidth = 160,
    Size = UDim2.fromOffset(580, 460),
    Acrylic = true,
    Theme = "Dark",
    MinimizeKey = Enum.KeyCode.LeftControl
})

local Tabs = {
    Main = Window:AddTab({ Title = "Main", Icon = "gamepad-2" }),
    Pets = Window:AddTab({ Title = "Eggs", Icon = "egg" }),
    Misc = Window:AddTab({ Title = "Misc", Icon = "coins" }),
    Settings = Window:AddTab({ Title = "Settings", Icon = "settings" })
}

Fluent:Notify({
    Title = "Script Loaded!",
    Content = "Logged in as " .. game.Players.LocalPlayer.Name,
    Duration = 7
})

Tabs.Main:AddSection("Auto Farm")

local ToggleTap = Tabs.Main:AddToggle("ToggleTap", {Title = "Auto Click", Default = false })

ToggleTap:OnChanged(function(Value)
  getgenv().zniv_Click = Value
  tap()
  end)

local ToggleWin = Tabs.Main:AddToggle("ToggleWin", {Title = "Instant Win", Default = false })

ToggleWin:OnChanged(function(Value)
  getgenv().zniv_Win = Value
  win()
end)

Tabs.Pets:AddSection("Pets")

Tabs.Pets:AddButton({
        Title = "Remove Egg Animation",
        Description = "Click to Remove Egg Animation",
        Callback = function()
            Window:Dialog({
                Title = "Are you sure?",
                Content = "Remove Egg Animation",
                Buttons = {
                    {
                        Title = "Yes",
                        Callback = function()
                          game:GetService("ReplicatedStorage"):WaitForChild("EggOpenMap"):Destroy()
                        end
                    },
                    {
                        Title = "No",
                        Callback = function()
                        end
                    }
                }
            })
        end
    })

local selectedEgg

local option = {
  "Forest 1 Egg",
  "Forest 2 Egg",
  "Magical Forest Egg",
  "Dessert Egg",
  "Volcano Egg"
}

local egg = {
  ["Forest 1 Egg"] = "1",
  ["Forest 2 Egg"] = "Forest2",
  ["Magical Forest Egg"] = "2",
  ["Dessert Egg"] = "3",
  ["Volcano Egg"] = "4"
}

local DropdownEgg = Tabs.Pets:AddDropdown("DropdownEgg:", {
    Title = "Select Egg",
    Values = option,
    Multi = false,
    Default = 1
})

DropdownEgg:OnChanged(function(Value)
    selectedEgg = egg[Value]
end)

local ToggleEgg = Tabs.Pets:AddToggle("ToggleEgg", { Title = "Hatch Egg", Default = false })

ToggleEgg:OnChanged(function(Value)
  getgenv().zniv_Egg = Value
  hatch(selectedEgg)
end)

Tabs.Misc:AddSection("BLACKSMITH")

local selectedEquipment

local option = {
  "Xp Booster",
  "Clover",
  "Magnet",
  "Boots of Swiftness",
  "Lucky Tooth"
}

local item = {
  ["Xp Booster"] = "XPBooster",
  ["Clover"] = "Clover",
  ["Magnet"] = "CoinMagnet",
  ["Boots of Swiftness"] = "BootsOfSwiftness",
  ["Lucky Tooth"] = "LuckyTooth"
}
  
local DropdownCraft = Tabs.Misc:AddDropdown("DropdownCraft:", {
  Title = "Select Equipment",
  Values = option,
  Multi = false,
  Default = 1
})

DropdownCraft:OnChanged(function(Value)
    selectedEquipment = item[Value]
end)

local ToggleCrafts = Tabs.Misc:AddToggle("ToggleCrafts", { Title = "Craft Selected Equipment", Default = false })

ToggleCrafts:OnChanged(function(Value)
  getgenv().zniv_Craft = Value
  craft(selectedEquipment)
end)

SaveManager:SetLibrary(Fluent)
InterfaceManager:SetLibrary(Fluent)

SaveManager:IgnoreThemeSettings()

SaveManager:SetIgnoreIndexes({})

InterfaceManager:SetFolder("FluentScriptHub")
SaveManager:SetFolder("FluentScriptHub/specific-game")

InterfaceManager:BuildInterfaceSection(Tabs.Settings)
SaveManager:BuildConfigSection(Tabs.Settings)

SaveManager:LoadAutoloadConfig()                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      






