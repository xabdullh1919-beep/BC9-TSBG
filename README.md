local Players = game:GetService("Players")
local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-- Main GUI Setup
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "BC9_GUI"
screenGui.ResetOnSpawn = false
screenGui.IgnoreGuiInset = true
screenGui.Parent = playerGui

local menuButton = Instance.new("TextButton")
menuButton.Size = UDim2.new(0, 60, 0, 40)
menuButton.Position = UDim2.new(0, 10, 0, 50)
menuButton.Text = "BC9"
menuButton.BackgroundColor3 = Color3.fromRGB(0, 170, 255)
menuButton.TextColor3 = Color3.new(1, 1, 1)
menuButton.Font = Enum.Font.SourceSansBold
menuButton.TextSize = 20
menuButton.Parent = screenGui

local uicorner = Instance.new("UICorner")
uicorner.CornerRadius = UDim.new(0.3, 0)
uicorner.Parent = menuButton

local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 450, 0, 350)
mainFrame.Position = UDim2.new(0.5, -225, 0.5, -175)
mainFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
mainFrame.Visible = true
mainFrame.Parent = screenGui

local titleBar = Instance.new("TextLabel")
titleBar.Size = UDim2.new(1, 0, 0, 35)
titleBar.Text = "BC9 | THE STRONGEST BATTLEGROUND"
titleBar.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
titleBar.TextColor3 = Color3.new(1, 1, 1)
titleBar.Font = Enum.Font.SourceSansBold
titleBar.TextSize = 18
titleBar.Parent = mainFrame

local pageSelector = Instance.new("Frame")
pageSelector.Size = UDim2.new(1, 0, 0, 40)
pageSelector.Position = UDim2.new(0, 0, 0, 35)
pageSelector.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
pageSelector.Parent = mainFrame

local pages = {}
local function createPage(index)
    local page = Instance.new("ScrollingFrame")
    page.Size = UDim2.new(1, -10, 1, -85)
    page.Position = UDim2.new(0, 5, 0, 80)
    page.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
    page.BorderSizePixel = 0
    page.ScrollBarThickness = 6
    page.Visible = (index == 1)
    page.CanvasSize = UDim2.new(0, 0, 0, 0)
    page.Parent = mainFrame
    
    local layout = Instance.new("UIListLayout", page)
    layout.Padding = UDim.new(0, 5)
    layout.HorizontalAlignment = Enum.HorizontalAlignment.Center
    layout.SortOrder = Enum.SortOrder.LayoutOrder
    
    pages[index] = page
    return page
end

local function createTab(name, index)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(1/6, 0, 1, 0)
    btn.Position = UDim2.new((index-1)/6, 0, 0, 0)
    btn.Text = name
    btn.BackgroundColor3 = Color3.fromRGB(0, 120, 255)
    btn.TextColor3 = Color3.new(1, 1, 1)
    btn.Font = Enum.Font.SourceSansBold
    btn.TextSize = 14
    btn.Parent = pageSelector
    
    local page = createPage(index)
    
    btn.MouseButton1Click:Connect(function()
        for _, p in pairs(pages) do p.Visible = false end
        page.Visible = true
    end)
end

-- Create 6 Tabs
createTab("Misc", 1)
createTab("Tech", 2)
createTab("Esp", 3)
createTab("Aimbot", 4)
createTab("Admin", 5)
createTab("Server", 6)

-- Helper to add buttons and update canvas
local function addButton(page, name, code, isToggle, onCode, offCode)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(0.9, 0, 0, 40)
    btn.Text = name
    btn.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
    btn.TextColor3 = Color3.new(1, 1, 1)
    btn.Font = Enum.Font.SourceSans
    btn.TextSize = 18
    btn.Parent = page

    if isToggle then
        local toggled = false
        btn.MouseButton1Click:Connect(function()
            toggled = not toggled
            btn.Text = toggled and name .. " [ON]" or name
            pcall(function() loadstring(toggled and onCode or offCode)() end)
        end)
    else
        btn.MouseButton1Click:Connect(function()
            pcall(function() loadstring(code)() end)
        end)
    end
    page.CanvasSize = UDim2.new(0, 0, 0, page.UIListLayout.AbsoluteContentSize.Y + 10)
end

-- === MISC PAGE ===
addButton(pages[1], "Anti Lag", [[loadstring(game:HttpGet("https://raw.githubusercontent.com/Kietba/Kietba/refs/heads/main/Antilag%20script"))()]])
addButton(pages[1], "M1 Reach Rework", [[loadstring(game:HttpGet("https://raw.githubusercontent.com/Kietba/Kietba/refs/heads/main/M1%20Reach%20Rework"))()]])
addButton(pages[1], "Aura (Client)", [[loadstring(game:HttpGet("https://raw.githubusercontent.com/Kietba/Kietba/refs/heads/main/Aura"))()]])
addButton(pages[1], "Auto Block + Aimbot", [[loadstring(game:HttpGet("https://raw.githubusercontent.com/Cyborg883/TSB/refs/heads/main/CombatGui"))()]])
addButton(pages[1], "Orbit", [[loadstring(game:HttpGet("https://raw.githubusercontent.com/Kietba/Kietba/refs/heads/main/Orbit%20by%20YQANTG"))()]])
addButton(pages[1], "Standing Pose", [[loadstring(game:HttpGet("https://raw.githubusercontent.com/Kietba/Kietba/refs/heads/main/Idiea"))()]])
addButton(pages[1], "Keyboard", [[loadstring(game:HttpGet("https://raw.githubusercontent.com/AZYsGithub/Delta-Scripts/refs/heads/main/MobileKeyboard.txt"))()]])
addButton(pages[1], "Fake Dash Q", [[loadstring(game:HttpGet("https://raw.githubusercontent.com/Kietba/Kietba/refs/heads/main/Fake%20Dash%20Q"))()]])
addButton(pages[1], "No Slide Endlag", [[loadstring(game:HttpGet("https://raw.githubusercontent.com/Slaphello/No-endlag-side-dash/refs/heads/main/No%20endlag%20side%20dash"))()]])

-- === TECH PAGE ===
addButton(pages[2], "M1 Reset (YQANTG)", [[loadstring(game:HttpGet("https://raw.githubusercontent.com/Kietba/Kietba/refs/heads/main/m1%20reset%20by%20me"))()]])
addButton(pages[2], "Auto Kyoto", [[loadstring(game:HttpGet("https://raw.githubusercontent.com/Kietba/Kietba/refs/heads/main/Auto%20kyoto%20ma%20hoa"))()]])
addButton(pages[2], "Oreo Dash", [[loadstring(game:HttpGet("https://raw.githubusercontent.com/Kietba/Kietba/refs/heads/main/Oreo%20Dash"))()]])
addButton(pages[2], "Lethal Dash", [[loadstring(game:HttpGet("https://raw.githubusercontent.com/Kietba/Kietba/refs/heads/main/Lethal%20Dash%20Script"))()]])
addButton(pages[2], "Tornado Tech", [[loadstring(game:HttpGet("https://raw.githubusercontent.com/Kietba/Kietba/refs/heads/main/Idk%20lolololol"))()]])

-- === ESP PAGE (Restored full logic) ===
addButton(pages[3], "Esp Name", "", true, [[
    _G.EspName = true
    while _G.EspName do
        for _, v in pairs(game.Players:GetPlayers()) do
            if v ~= game.Players.LocalPlayer and v.Character and v.Character:FindFirstChild("Head") and not v.Character.Head:FindFirstChild("BC9_Name") then
                local b = Instance.new("BillboardGui", v.Character.Head)
                b.Name = "BC9_Name" b.Size = UDim2.new(0,100,0,30) b.AlwaysOnTop = true b.StudsOffset = Vector3.new(0,3,0)
                local l = Instance.new("TextLabel", b)
                l.Size = UDim2.new(1,0,1,0) l.BackgroundTransparency = 1 l.Text = v.Name l.TextColor3 = Color3.new(1,1,1) l.TextScaled = true
            end
        end
        task.wait(1)
    end
]], [[
    _G.EspName = false
    for _, v in pairs(game.Players:GetPlayers()) do
        if v.Character and v.Character:FindFirstChild("Head") and v.Character.Head:FindFirstChild("BC9_Name") then v.Character.Head.BC9_Name:Destroy() end
    end
]])

-- === AIMBOT PAGE ===
addButton(pages[4], "Aimbot", [[loadstring(game:HttpGet("https://raw.githubusercontent.com/Kietba/Kietba/refs/heads/main/Aimlock%20By%20YQANTG"))()]])
addButton(pages[4], "FaceLock", [[loadstring(game:HttpGet("https://raw.githubusercontent.com/Kietba/Kietba/refs/heads/Tsb/FACELOCK"))()]])

-- === ADMIN PAGE ===
addButton(pages[5], "Infinite Yield", [[loadstring(game:HttpGet('https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source'))()]])
addButton(pages[5], "Nameless Admin", [[loadstring(game:HttpGet("https://github.com/FilteringEnabled/NamelessAdmin/blob/main/Source?raw=true"))()]])

-- === SERVER PAGE ===
addButton(pages[6], "Rejoin", [[game:GetService("TeleportService"):TeleportToPlaceInstance(game.PlaceId, game.JobId, game.Players.LocalPlayer)]])
addButton(pages[6], "Server Hop", [[loadstring(game:HttpGet("https://raw.githubusercontent.com/xabdullh1919-beep/BC9-TSBG-2/main/serverhop.lua"))()]])

menuButton.MouseButton1Click:Connect(function()
    mainFrame.Visible = not mainFrame.Visible
end)
