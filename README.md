local remote = game:GetService("ReplicatedStorage"):WaitForChild("Events")
local cd = 0.01

getgenv().zniv_Click = true
getgenv().zniv_Exp = true
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

ToggleTrain:OnChanged(function(Value)
  getgenv().zniv_Damage = Value
  tap()
  end)

local selectedDummies

local option = {
  "Forest Dummies 1",
  "Forest Dummies 2",
  "Forest Dummies 3",
  "Magical Forest Dummies 1",
  "Magical Forest Dummies 2",
  "Magical Forest Dummies 3",
  "Dessert Dummies 1", 
  "Dessert Dummies 2",
  "Dessert Dummies 3",
  "Underworld Dummies 1",
  "Underworld Dummies 2",
  "Underworld Dummies 3"
}

local dummies = {
  ["Forest Dummies 1"] = {"1", "1"},
  ["Forest Dummies 2"] = {"1", "2"},
  ["Forest Dummies 3"] = {"1", "3"},
  ["Magical Forest Dummies 1"] = {"2", "1"},
  ["Magical Forest Dummies 2"] = {"2", "2"},
  ["Magical Forest Dummies 3"] = {"2", "3"},
  ["Dessert Dummies 1"] = {"3", "1"},
  ["Dessert Dummies 2"] = {"3", "2"},
  ["Dessert Dummies 3"] = {"3", "3"},
  ["Underworld Dummies 1"] = {"4", "1"},
  ["Underworld Dummies 2"] = {"4", "2"},
  ["Underworld Dummies 3"] = {"4", "3"}
}

local DropdownExp = Tabs.Misc:AddDropdown("DropdownExp:", {
    Title = "Choose Dummies",
    Values = option,
    Multi = false,
    Default = 1
})

DropdownExp:OnChanged(function(Value)
    selectedDummies = dummies[Value]
end)

local ToggleExp = Tabs.Misc:AddToggle("ToggleExp", { Title = "Select Pet Trainer", Default = false })

ToggleExp:OnChanged(function(Value)
  getgenv().zniv_Exp = Value
  xp(selectedDummies)
end)

local ToggleExp = Tabs.Main:AddToggle("ToggleExp", {Title = "Train Dummies", Default = false })

ToggleExp:OnChanged(function(Value)
  getgenv().zniv_Exp = Value
  xp()
  end)

local ToggleWin = Tabs.Main:AddToggle("ToggleWin", {Title = "Instant Win", Default = false })

ToggleWin:OnChanged(function(Value)
  getgenv().zniv_Win = Value
  win()
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
