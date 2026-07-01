NoirUI

NoirUI is a modern, feature-rich GUI library for Roblox exploits. It's a rebranded and enhanced version of Compkiller, designed with a sleek purple theme and optimized for both desktop and mobile devices.

---

✨ Features

· 🎨 Beautiful UI - Modern design with smooth animations
· 📱 Mobile Optimized - Touch-friendly interface with adaptive sizing
· 🎯 Rich Components - Toggles, Sliders, Dropdowns, Color Pickers, and more
· ⌨️ Advanced Keybind System - Right-click any element to assign keybinds
· 💾 Built-in Config System - Save/Load settings with ease
· 🖼️ Icon Library - Hundreds of icons (Lucide + FontAwesome)
· 🎭 Multiple Themes - 50+ beautiful color themes
· 🔒 Secure Mode - Cache assets locally for better performance
· 📢 Notifications - Built-in notification system
· 💧 Watermark - Customizable on-screen watermark

---

📋 Table of Contents

· Installation
· Quick Start
· Window Configuration
· Components
· Themes
· Config System
· Mobile Optimization
· API Reference
· Examples
· License

---

🚀 Installation

```lua
-- Load NoirUI
local Noir = loadstring(game:HttpGet("https://raw.githubusercontent.com/NoirStillHere/NUI-Lib/refs/heads/main/src/NoirCK.lua"))()
```

Note: You need to host the modified NoirUI code on your own server or paste it directly into your script.

---

🏃 Quick Start

```lua
local Noir = loadstring(game:HttpGet("https://raw.githubusercontent.com/NoirStillHere/NUI-Lib/refs/heads/main/src/NoirCK.lua"))()

-- Create window
local Window = Noir.new({
    Name = "My Script",
    Keybind = "Insert",
    Scale = UDim2.new(0.35, 0, 0.50, 0)  -- 35% width, 50% height
})

-- Update user info
Window:Update({
    Username = game.Players.LocalPlayer.DisplayName,
    ExpireDate = "Never"
})

-- Create tab
local Tab = Window:DrawTab({
    Name = "Main",
    Icon = "home",
    Type = "Single"
})

-- Create section
local Section = Tab:DrawSection({
    Name = "Settings"
})

-- Add toggle
Section:AddToggle({
    Name = "Enable Feature",
    Default = false,
    Flag = "Feature_Enable",
    Callback = function(Value)
        print("Feature:", Value)
    end
})

-- Add slider
Section:AddSlider({
    Name = "Value",
    Min = 0,
    Max = 100,
    Default = 50,
    Type = "%",
    Flag = "Value",
    Callback = function(Value)
        print("Value:", Value)
    end
})
```

---

📱 Mobile Optimization

Recommended Sizes for 6.5" Screen

Device Width Height Scale
5.5" (iPhone SE) 30-35% 45-50% UDim2.new(0.33, 0, 0.48, 0)
6.1" (iPhone 14) 35-38% 50-55% UDim2.new(0.35, 0, 0.50, 0)
6.5" (iPhone 14 Plus) 35-40% 50-55% UDim2.new(0.38, 0, 0.52, 0)
6.7" (iPhone Pro Max) 35-40% 50-55% UDim2.new(0.38, 0, 0.55, 0)
Tablet 40-45% 55-60% UDim2.new(0.42, 0, 0.58, 0)

Mobile Auto-Detect

```lua
local UserInputService = game:GetService("UserInputService")
local IsMobile = UserInputService.TouchEnabled and not UserInputService.MouseEnabled

local Window = Noir.new({
    Name = "My Script",
    Keybind = "Insert",
    Scale = IsMobile and UDim2.new(0.35, 0, 0.50, 0) or UDim2.new(0.45, 0, 0.65, 0),
    TextSize = IsMobile and 14 or 15
})
```

---

🎨 Components

Toggle

```lua
Section:AddToggle({
    Name = "Toggle Name",
    Default = false,      -- Default state
    Flag = "toggle_flag", -- For config system
    Risky = false,        -- Yellow warning color
    Callback = function(Value)
        -- Your code here
    end
})
```

Slider

```lua
Section:AddSlider({
    Name = "Slider Name",
    Min = 0,
    Max = 100,
    Default = 50,
    Type = "%",           -- Unit display
    Round = 0,            -- Decimal places
    Flag = "slider_flag",
    Callback = function(Value)
        -- Your code here
    end
})
```

Dropdown

```lua
-- Single selection
Section:AddDropdown({
    Name = "Dropdown",
    Default = "Option 1",
    Values = {"Option 1", "Option 2", "Option 3"},
    Multi = false,
    Flag = "dropdown_flag",
    Callback = function(Value)
        print(Value)  -- Returns string
    end
})

-- Multiple selection
Section:AddDropdown({
    Name = "Multi Dropdown",
    Default = {"Option 1"},
    Values = {"Option 1", "Option 2", "Option 3"},
    Multi = true,
    Flag = "multi_flag",
    Callback = function(Value)
        -- Value is table: {["Option 1"] = true, ["Option 2"] = false}
        print(Value)
    end
})
```

Color Picker

```lua
Section:AddColorPicker({
    Name = "Color Picker",
    Default = Color3.fromRGB(139, 92, 246),
    Transparency = 0.5,
    Flag = "color_flag",
    Callback = function(Color, Transparency)
        print(Color, Transparency)
    end
})
```

Text Box

```lua
-- Text input
Section:AddTextBox({
    Name = "Text Input",
    Default = "",
    Placeholder = "Enter text...",
    Numeric = false,
    Flag = "text_flag",
    Callback = function(Text)
        print(Text)
    end
})

-- Numeric input
Section:AddTextBox({
    Name = "Number Input",
    Default = "100",
    Placeholder = "Enter number...",
    Numeric = true,
    Flag = "number_flag",
    Callback = function(Value)
        print(tonumber(Value))
    end
})
```

Button

```lua
Section:AddButton({
    Name = "Button Name",
    Callback = function()
        -- Your code here
    end
})
```

Helper

```lua
Section:AddHelper({
    Text = "Tooltip text\nCan be multi-line"
})
```

Paragraph

```lua
Section:AddParagraph({
    Title = "Title",
    Content = "Content text\nCan be multi-line"
})
```

Keybind

```lua
-- Keybinds are automatically available for Toggles and Sliders
-- Users right-click the element to open keybind settings

-- For manual keybind:
Section:AddKeybind({
    Name = "Keybind Name",
    Default = Enum.KeyCode.F,
    Callback = function(Key)
        print("Key:", Key)
    end,
    Blacklist = {Enum.KeyCode.Insert, "MouseLeft"}
})
```

---

🎭 Themes

Available Themes

```lua
-- Default themes
Noir:SetTheme("Default")
Noir:SetTheme("Noir")
Noir:SetTheme("Nebula")
Noir:SetTheme("Eclipse")
Noir:SetTheme("Aurora")
Noir:SetTheme("Galaxy")
Noir:SetTheme("Velvet")
Noir:SetTheme("Mystic")
Noir:SetTheme("Cyber")
Noir:SetTheme("Phantom")
Noir:SetTheme("Lunar")

-- And 50+ more themes...
```

Custom Theme

```lua
Noir.Colors = {
    Highlight = Color3.fromRGB(139, 92, 246),
    Toggle = Color3.fromRGB(124, 58, 237),
    Risky = Color3.fromRGB(255, 200, 50),
    BGDBColor = Color3.fromRGB(8, 8, 8),
    BlockColor = Color3.fromRGB(15, 15, 15),
    StrokeColor = Color3.fromRGB(25, 25, 25),
    SwitchColor = Color3.fromRGB(255, 255, 255),
    DropColor = Color3.fromRGB(20, 20, 20),
    MouseEnter = Color3.fromRGB(40, 40, 40),
    BlockBackground = Color3.fromRGB(30, 30, 30),
    LineColor = Color3.fromRGB(35, 35, 35),
    HighStrokeColor = Color3.fromRGB(45, 45, 45),
}
Noir:RefreshCurrentColor()
```

---

💾 Config System

Setup Config Manager

```lua
local Config = Noir:ConfigManager({
    Directory = "MyScript",   -- Folder name
    Config = "Settings"       -- Subfolder name
})

-- Create config tab
local ConfigTab = Window:DrawConfig({
    Name = "Configs",
    Icon = "folder",
    Config = Config
})
```

Manual Config Operations

```lua
-- Save config
Config:WriteConfig({
    Name = "MyConfig",
    Author = "Username"
})

-- Load config
Config:LoadConfig("MyConfig")

-- Delete config
Config:DeleteConfig("MyConfig")

-- Get all configs
local Configs = Config:GetFullConfigs()
for _, ConfigData in ipairs(Configs) do
    print(ConfigData.Name, ConfigData.Info.Author)
end
```

---

📢 Notifications

```lua
local Notify = Noir.newNotify()

-- Simple notification
Notify.new({
    Title = "Title",
    Icon = "check",
    Content = "Message content",
    Duration = 3  -- Seconds (math.huge for infinite)
})

-- Progress notification
local Progress = Notify.new({
    Title = "Loading...",
    Icon = "loader",
    Content = "0%",
    Duration = math.huge
})

-- Update progress
task.spawn(function()
    for i = 0, 100 do
        task.wait(0.05)
        Progress:SetProgress(i / 100)
        Progress:Content(tostring(i) .. "%")
    end
    task.wait(0.5)
    Progress:Close()
end)
```

---

💧 Watermark

```lua
local Watermark = Window:Watermark()

-- Add text to watermark
local UserText = Watermark:AddText({
    Icon = "user",
    Text = "Username"
})

local TimeText = Watermark:AddText({
    Icon = "clock",
    Text = os.date("%H:%M:%S")
})

-- Update text
UserText:SetText("New Text")

-- Hide/Show
UserText:Visible(false)
UserText:Visible(true)
```

---

🔧 API Reference

Window

Method Description
Noir.new(Config) Create new window
Window:Update(Config) Update window info
Window:DrawTab(Config) Create new tab
Window:DrawConfig(Config) Create config tab
Window:Watermark() Create watermark
Window:Toggle(boolean) Open/close window
Window:SetMenuKey(key) Change menu keybind
Window:SetVisible(boolean) Show/hide window

Tab

Method Description
Tab:DrawSection(Config) Create section
Tab:DrawTab(Config) Create sub-tab (ContainerTab)

Section

Method Description
Section:AddToggle(Config) Add toggle
Section:AddSlider(Config) Add slider
Section:AddDropdown(Config) Add dropdown
Section:AddColorPicker(Config) Add color picker
Section:AddTextBox(Config) Add text box
Section:AddButton(Config) Add button
Section:AddKeybind(Config) Add keybind
Section:AddHelper(Config) Add helper tooltip
Section:AddParagraph(Config) Add paragraph

---

📝 Full Example

```lua
local Noir = loadstring(game:HttpGet("https://raw.githubusercontent.com/NoirStillHere/NUI-Lib/refs/heads/main/src/NoirCK.lua"))()

-- Detect mobile
local UserInputService = game:GetService("UserInputService")
local IsMobile = UserInputService.TouchEnabled and not UserInputService.MouseEnabled

-- Create window
local Window = Noir.new({
    Name = "My Script v1.0",
    Keybind = "Insert",
    Logo = Noir.Logo,
    Scale = IsMobile and UDim2.new(0.35, 0, 0.50, 0) or UDim2.new(0.45, 0, 0.65, 0),
    TextSize = IsMobile and 14 or 15
})

-- Update info
Window:Update({
    Username = game.Players.LocalPlayer.DisplayName,
    ExpireDate = "Never"
})

-- Setup config
local Config = Noir:ConfigManager({
    Directory = "MyScript",
    Config = "Settings"
})

-- Create tabs
local MainTab = Window:DrawTab({
    Name = "Main",
    Icon = "home",
    Type = IsMobile and "Single" or "Double"
})

local ConfigTab = Window:DrawConfig({
    Name = "Configs",
    Icon = "folder",
    Config = Config
})

-- Add sections
local Combat = MainTab:DrawSection({
    Name = " Combat",
    Position = IsMobile and "Left" or "Left"
})

local Visual = MainTab:DrawSection({
    Name = " Visual",
    Position = IsMobile and "Left" or "Right"
})

-- Add components
Combat:AddToggle({
    Name = "Enable Aimbot",
    Default = false,
    Flag = "Aimbot_Enable",
    Callback = function(Value)
        print("Aimbot:", Value)
    end
})

Combat:AddSlider({
    Name = "FOV",
    Min = 0,
    Max = 360,
    Default = 120,
    Type = "°",
    Flag = "Aimbot_FOV",
    Callback = function(Value)
        print("FOV:", Value)
    end
})

Visual:AddColorPicker({
    Name = "ESP Color",
    Default = Color3.fromRGB(139, 92, 246),
    Flag = "ESP_Color",
    Callback = function(Color, Trans)
        print("Color changed")
    end
})

-- Add watermark
local Watermark = Window:Watermark()
Watermark:AddText({
    Icon = "user",
    Text = game.Players.LocalPlayer.DisplayName
})

-- Notification
local Notify = Noir.newNotify()
Notify.new({
    Title = "NoirUI",
    Icon = "check",
    Content = "Script loaded!",
    Duration = 3
})

print("NoirUI loaded successfully!")
```
