-- ========================================
-- GRANNY ESP - PROFESSIONAL EDITION
-- Made by E0k
-- ig: Foxzie.leak
-- ========================================

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local Workspace = game:GetService("Workspace")
local TweenService = game:GetService("TweenService")
local LocalPlayer = Players.LocalPlayer

-- ========================================
-- LOADING SCREEN
-- ========================================
local loadingGui = Instance.new("ScreenGui")
loadingGui.Parent = LocalPlayer:WaitForChild("PlayerGui")
loadingGui.ResetOnSpawn = false
loadingGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

local loadingFrame = Instance.new("Frame")
loadingFrame.Size = UDim2.new(1, 0, 1, 0)
loadingFrame.BackgroundColor3 = Color3.fromRGB(8, 0, 8)
loadingFrame.BackgroundTransparency = 0
loadingFrame.Parent = loadingGui

local bloodGradient = Instance.new("UIGradient")
bloodGradient.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0, Color3.fromRGB(20, 0, 5)),
    ColorSequenceKeypoint.new(0.3, Color3.fromRGB(40, 0, 10)),
    ColorSequenceKeypoint.new(0.6, Color3.fromRGB(60, 5, 5)),
    ColorSequenceKeypoint.new(0.8, Color3.fromRGB(30, 0, 8)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(15, 0, 5))
})
bloodGradient.Parent = loadingFrame

local bloodGlow = Instance.new("Frame")
bloodGlow.Size = UDim2.new(0.5, 0, 0.35, 0)
bloodGlow.Position = UDim2.new(0.25, 0, 0.3, 0)
bloodGlow.BackgroundColor3 = Color3.fromRGB(180, 0, 0)
bloodGlow.BackgroundTransparency = 0.85
bloodGlow.BorderSizePixel = 0
bloodGlow.Parent = loadingFrame

local glowGrad = Instance.new("UIGradient")
glowGrad.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0, Color3.fromRGB(180, 0, 0)),
    ColorSequenceKeypoint.new(0.4, Color3.fromRGB(255, 20, 0)),
    ColorSequenceKeypoint.new(0.7, Color3.fromRGB(200, 0, 0)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(150, 0, 0))
})
glowGrad.Parent = bloodGlow

local glowCorner = Instance.new("UICorner")
glowCorner.CornerRadius = UDim.new(1, 0)
glowCorner.Parent = bloodGlow

-- Blood drops
for i = 1, 8 do
    local drop = Instance.new("Frame")
    drop.Size = UDim2.new(0, math.random(15, 35), 0, math.random(15, 35))
    drop.Position = UDim2.new(math.random(5, 95) / 100, 0, math.random(5, 95) / 100, 0)
    drop.BackgroundColor3 = Color3.fromRGB(120, 0, 0)
    drop.BackgroundTransparency = 0.7 + math.random(0, 20) / 100
    drop.BorderSizePixel = 0
    drop.Parent = loadingFrame
    
    local dropCorner = Instance.new("UICorner")
    dropCorner.CornerRadius = UDim.new(0.5, 0)
    dropCorner.Parent = drop
    drop.Rotation = math.random(0, 360)
end

local mainText = Instance.new("TextLabel")
mainText.Size = UDim2.new(0.8, 0, 0.2, 0)
mainText.Position = UDim2.new(0.1, 0, 0.32, 0)
mainText.BackgroundTransparency = 1
mainText.Text = "Made by E0k"
mainText.TextColor3 = Color3.fromRGB(255, 60, 60)
mainText.TextSize = 45
mainText.Font = Enum.Font.GothamBold
mainText.TextScaled = true
mainText.TextStrokeColor3 = Color3.fromRGB(100, 0, 0)
mainText.TextStrokeTransparency = 0.3
mainText.Parent = loadingFrame

local subText = Instance.new("TextLabel")
subText.Size = UDim2.new(0.8, 0, 0.12, 0)
subText.Position = UDim2.new(0.1, 0, 0.52, 0)
subText.BackgroundTransparency = 1
subText.Text = "ig: Foxzie.leak"
subText.TextColor3 = Color3.fromRGB(200, 100, 150)
subText.TextSize = 25
subText.Font = Enum.Font.Gotham
subText.TextScaled = true
subText.TextTransparency = 0.4
subText.Parent = loadingFrame

local loadingBarBg = Instance.new("Frame")
loadingBarBg.Size = UDim2.new(0.4, 0, 0.025, 0)
loadingBarBg.Position = UDim2.new(0.3, 0, 0.72, 0)
loadingBarBg.BackgroundColor3 = Color3.fromRGB(40, 10, 10)
loadingBarBg.BackgroundTransparency = 0.5
loadingBarBg.BorderSizePixel = 1
loadingBarBg.BorderColor3 = Color3.fromRGB(180, 0, 0)
loadingBarBg.Parent = loadingFrame

local barCorner = Instance.new("UICorner")
barCorner.CornerRadius = UDim.new(0.5, 0)
barCorner.Parent = loadingBarBg

local loadingBarFill = Instance.new("Frame")
loadingBarFill.Size = UDim2.new(0, 0, 1, 0)
loadingBarFill.BackgroundColor3 = Color3.fromRGB(200, 0, 0)
loadingBarFill.BorderSizePixel = 0
loadingBarFill.Parent = loadingBarBg

local fillCorner = Instance.new("UICorner")
fillCorner.CornerRadius = UDim.new(0.5, 0)
fillCorner.Parent = loadingBarFill

local percentText = Instance.new("TextLabel")
percentText.Size = UDim2.new(0.2, 0, 0.04, 0)
percentText.Position = UDim2.new(0.4, 0, 0.76, 0)
percentText.BackgroundTransparency = 1
percentText.Text = "0%"
percentText.TextColor3 = Color3.fromRGB(255, 150, 150)
percentText.TextSize = 18
percentText.Font = Enum.Font.Gotham
percentText.Parent = loadingFrame

local function animateLoading()
    local duration = 2.5
    local steps = 30
    local stepTime = duration / steps
    
    for i = 0, steps do
        local progress = i / steps
        loadingBarFill.Size = UDim2.new(progress, 0, 1, 0)
        percentText.Text = string.format("%.0f%%", progress * 100)
        wait(stepTime)
    end
end

-- ========================================
-- SETTINGS
-- ========================================
local settings = {
    players = true,
    bots = true,
    items = true,
    traps = true,
    house1 = true,
    house2 = true,
    mansion = true,
    minimap = true
}

local espObjects = {}
local minimized = false
local guiRef = nil

-- ========================================
-- CREATE ESP (LIGHTWEIGHT - NO HIGHLIGHT FOR ITEMS)
-- ========================================
local function createESP(target, color, text, textColor, noHighlight)
    if not target or not target.Parent then return end
    
    if espObjects[target] then
        for _, obj in pairs(espObjects[target]) do
            pcall(function() obj:Destroy() end)
        end
        espObjects[target] = nil
    end
    
    local objects = {}
    
    -- Only add highlight if not an item (to reduce lag)
    if not noHighlight then
        local highlight = Instance.new("Highlight")
        highlight.Adornee = target
        highlight.FillColor = color
        highlight.FillTransparency = 0.5
        highlight.OutlineColor = Color3.fromRGB(255, 255, 255)
        highlight.OutlineTransparency = 0.3
        highlight.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop
        highlight.Parent = target
        table.insert(objects, highlight)
    end
    
    local head = target:FindFirstChild("Head")
    if not head then
        head = target:FindFirstChild("HumanoidRootPart") or target:FindFirstChild("PrimaryPart")
    end
    
    if head then
        local billboard = Instance.new("BillboardGui")
        billboard.Size = UDim2.new(0, 200, 0, 30)
        billboard.Adornee = head
        billboard.AlwaysOnTop = true
        billboard.Parent = head
        
        local label = Instance.new("TextLabel")
        label.Size = UDim2.new(1, 0, 1, 0)
        label.BackgroundTransparency = 1
        label.Text = text or "???"
        label.TextColor3 = textColor or Color3.fromRGB(255, 255, 255)
        label.TextScaled = true
        label.Font = Enum.Font.GothamBold
        label.TextStrokeColor3 = Color3.fromRGB(0, 0, 0)
        label.TextStrokeTransparency = 0.3
        label.Parent = billboard
        
        table.insert(objects, billboard)
        table.insert(objects, label)
    end
    
    espObjects[target] = objects
end

local function removeESP(target)
    if espObjects[target] then
        for _, obj in pairs(espObjects[target]) do
            pcall(function() obj:Destroy() end)
        end
        espObjects[target] = nil
    end
end

-- ========================================
-- FIND FUNCTIONS
-- ========================================

-- Players
local function findPlayers()
    local results = {}
    for _, player in ipairs(Players:GetPlayers()) do
        if player ~= LocalPlayer and player.Character then
            local name = player.Name:lower()
            if not string.find(name, "granny") and not string.find(name, "grandma") and not string.find(name, "grandpa") and not string.find(name, "slendrina") and not string.find(name, "faceless") then
                table.insert(results, player.Character)
            end
        end
    end
    return results
end

-- Bots (Granny, Grandpa, etc.)
local function findBots()
    local results = {}
    
    for _, player in ipairs(Players:GetPlayers()) do
        if player ~= LocalPlayer and player.Character then
            local name = player.Name:lower()
            if string.find(name, "granny") or string.find(name, "grandma") or string.find(name, "grandpa") or string.find(name, "slendrina") or string.find(name, "faceless") then
                table.insert(results, player.Character)
            end
        end
    end
    
    local botNames = {"Granny", "Grandma", "Grandpa", "Slendrina", "Faceless", "Enemy", "NPC", "Boss"}
    for _, name in ipairs(botNames) do
        local found = Workspace:FindFirstChild(name)
        if found and found:IsA("Model") then
            table.insert(results, found)
        end
    end
    
    return results
end

-- House I Items
local function findHouse1Items()
    local results = {}
    local itemNames = {
        "Master key", "Padlock key", "Car key", "Playhouse key", "Special key", "Weapon key",
        "Safe key", "Spider key", "Hammer", "Crowbar", "Screwdriver", "Wrench",
        "Cutting Pliers", "Chain Cutter", "Winch Handle", "Shovel", "Rope", "Hook",
        "Battery", "Car Battery", "Spark Plug", "Birdseed", "Meat", "Book", "Plank",
        "Padlock Code", "Remote Control", "Wooden Stick", "Wheel Crank"
    }
    
    local function search(folder)
        if not folder then return end
        for _, child in ipairs(folder:GetChildren()) do
            if child:IsA("Model") or child:IsA("Part") or child:IsA("Tool") or child:IsA("BasePart") then
                local name = child.Name
                for _, itemName in ipairs(itemNames) do
                    if name == itemName then
                        if not child:FindFirstChild("Humanoid") then
                            table.insert(results, child)
                        end
                        break
                    end
                end
            end
            if child:IsA("Folder") or child:IsA("Model") then
                search(child)
            end
        end
    end
    
    search(Workspace)
    return results
end

-- House II Items
local function findHouse2Items()
    local results = {}
    local itemNames = {
        "Hand wheel", "Door handle", "Security key", "Safe key", "Cutting pliers",
        "Boat key", "Boat steering wheel", "Gasoline can", "Crowbar", "Padlock key",
        "Spark plug"
    }
    
    local function search(folder)
        if not folder then return end
        for _, child in ipairs(folder:GetChildren()) do
            if child:IsA("Model") or child:IsA("Part") or child:IsA("Tool") or child:IsA("BasePart") then
                local name = child.Name
                for _, itemName in ipairs(itemNames) do
                    if name == itemName then
                        if not child:FindFirstChild("Humanoid") then
                            table.insert(results, child)
                        end
                        break
                    end
                end
            end
            if child:IsA("Folder") or child:IsA("Model") then
                search(child)
            end
        end
    end
    
    search(Workspace)
    return results
end

-- Mansion Items
local function findMansionItems()
    local results = {}
    local itemNames = {
        "Padlock key", "Shed key", "Generator cable", "Coin", "Ticket",
        "Stun gun", "Firewood", "Hand wheel", "Fuse", "Safe key"
    }
    
    local function search(folder)
        if not folder then return end
        for _, child in ipairs(folder:GetChildren()) do
            if child:IsA("Model") or child:IsA("Part") or child:IsA("Tool") or child:IsA("BasePart") then
                local name = child.Name
                for _, itemName in ipairs(itemNames) do
                    if name == itemName then
                        if not child:FindFirstChild("Humanoid") then
                            table.insert(results, child)
                        end
                        break
                    end
                end
            end
            if child:IsA("Folder") or child:IsA("Model") then
                search(child)
            end
        end
    end
    
    search(Workspace)
    return results
end

-- Traps (no doors)
local function findTraps()
    local results = {}
    local trapNames = {"Trap", "Pułapka", "BearTrap", "Pendulum", "Spike", "Cola"}
    
    local function search(folder)
        if not folder then return end
        for _, child in ipairs(folder:GetChildren()) do
            if child:IsA("Model") or child:IsA("Part") then
                local name = child.Name:lower()
                for _, check in ipairs(trapNames) do
                    if string.find(name, check:lower()) then
                        table.insert(results, child)
                        break
                    end
                end
            end
            if child:IsA("Folder") or child:IsA("Model") then
                search(child)
            end
        end
    end
    
    search(Workspace)
    return results
end

-- ========================================
-- REFRESH ESP
-- ========================================
local function refreshESP()
    -- Cleanup
    for obj, _ in pairs(espObjects) do
        if not obj or not obj.Parent then
            removeESP(obj)
        end
    end
    
    -- Players (Blue) - with highlight
    if settings.players then
        for _, player in ipairs(findPlayers()) do
            local name = player.Parent and player.Parent.Name or "Player"
            createESP(player, Color3.fromRGB(0, 120, 255), name, Color3.fromRGB(150, 200, 255), false)
        end
    end
    
    -- Bots (Red) - with highlight
    if settings.bots then
        for _, bot in ipairs(findBots()) do
            local name = bot.Parent and bot.Parent.Name or "Bot"
            createESP(bot, Color3.fromRGB(255, 0, 0), name, Color3.fromRGB(255, 100, 100), false)
        end
    end
    
    -- House I Items (Green) - NO HIGHLIGHT, only text
    if settings.house1 then
        for _, item in ipairs(findHouse1Items()) do
            createESP(item, Color3.fromRGB(0, 255, 0), item.Name, Color3.fromRGB(0, 255, 100), true)
        end
    end
    
    -- House II Items (Yellow) - NO HIGHLIGHT, only text
    if settings.house2 then
        for _, item in ipairs(findHouse2Items()) do
            createESP(item, Color3.fromRGB(255, 200, 0), item.Name, Color3.fromRGB(255, 200, 0), true)
        end
    end
    
    -- Mansion Items (Purple) - NO HIGHLIGHT, only text
    if settings.mansion then
        for _, item in ipairs(findMansionItems()) do
            createESP(item, Color3.fromRGB(255, 100, 255), item.Name, Color3.fromRGB(255, 100, 255), true)
        end
    end
    
    -- Traps (Pink) - with highlight
    if settings.traps then
        for _, trap in ipairs(findTraps()) do
            createESP(trap, Color3.fromRGB(255, 0, 50), "Trap", Color3.fromRGB(255, 50, 100), false)
        end
    end
end

-- ========================================
-- CREATE MAIN GUI
-- ========================================
local function createMainGUI()
    -- Fade out loading
    local fadeTween = TweenService:Create(loadingFrame, TweenInfo.new(0.5, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {
        BackgroundTransparency = 1
    })
    fadeTween:Play()
    fadeTween.Completed:Wait()
    loadingGui:Destroy()
    
    local gui = Instance.new("ScreenGui")
    gui.Parent = LocalPlayer:WaitForChild("PlayerGui")
    gui.ResetOnSpawn = false
    gui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
    guiRef = gui
    
    local mainFrame = Instance.new("Frame")
    mainFrame.Size = UDim2.new(0, 260, 0, 390)
    mainFrame.Position = UDim2.new(0.02, 0, 0.05, 0)
    mainFrame.BackgroundColor3 = Color3.fromRGB(12, 0, 8)
    mainFrame.BackgroundTransparency = 0.08
    mainFrame.BorderSizePixel = 2
    mainFrame.BorderColor3 = Color3.fromRGB(180, 0, 0)
    mainFrame.Active = true
    mainFrame.Draggable = true
    mainFrame.Parent = gui
    
    local frameCorner = Instance.new("UICorner")
    frameCorner.CornerRadius = UDim.new(0, 10)
    frameCorner.Parent = mainFrame
    
    local mainGrad = Instance.new("UIGradient")
    mainGrad.Color = ColorSequence.new({
        ColorSequenceKeypoint.new(0, Color3.fromRGB(20, 0, 5)),
        ColorSequenceKeypoint.new(0.5, Color3.fromRGB(30, 0, 10)),
        ColorSequenceKeypoint.new(1, Color3.fromRGB(15, 0, 5))
    })
    mainGrad.Parent = mainFrame
    
    -- Top Bar
    local topBar = Instance.new("Frame")
    topBar.Size = UDim2.new(1, 0, 0.12, 0)
    topBar.Position = UDim2.new(0, 0, 0, 0)
    topBar.BackgroundColor3 = Color3.fromRGB(40, 0, 0)
    topBar.BackgroundTransparency = 0.5
    topBar.BorderSizePixel = 0
    topBar.Parent = mainFrame
    
    local topCorner = Instance.new("UICorner")
    topCorner.CornerRadius = UDim.new(0, 10)
    topCorner.Parent = topBar
    
    local titleLabel = Instance.new("TextLabel")
    titleLabel.Size = UDim2.new(0.55, 0, 0.55, 0)
    titleLabel.Position = UDim2.new(0.05, 0, 0, 0)
    titleLabel.BackgroundTransparency = 1
    titleLabel.Text = "Made by E0k"
    titleLabel.TextColor3 = Color3.fromRGB(255, 60, 60)
    titleLabel.TextSize = 14
    titleLabel.Font = Enum.Font.GothamBold
    titleLabel.TextXAlignment = Enum.TextXAlignment.Left
    titleLabel.Parent = topBar
    
    local subLabel = Instance.new("TextLabel")
    subLabel.Size = UDim2.new(0.5, 0, 0.45, 0)
    subLabel.Position = UDim2.new(0.05, 0, 0.55, 0)
    subLabel.BackgroundTransparency = 1
    subLabel.Text = "ig: Foxzie.leak"
    subLabel.TextColor3 = Color3.fromRGB(200, 100, 150)
    subLabel.TextSize = 10
    subLabel.Font = Enum.Font.Gotham
    subLabel.TextXAlignment = Enum.TextXAlignment.Left
    subLabel.Parent = topBar
    
    -- Minimize Button
    local minBtn = Instance.new("TextButton")
    minBtn.Size = UDim2.new(0.08, 0, 0.6, 0)
    minBtn.Position = UDim2.new(0.82, 0, 0.2, 0)
    minBtn.BackgroundColor3 = Color3.fromRGB(60, 0, 0)
    minBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
    minBtn.Text = "_"
    minBtn.TextSize = 20
    minBtn.Font = Enum.Font.GothamBold
    minBtn.BorderSizePixel = 1
    minBtn.BorderColor3 = Color3.fromRGB(150, 0, 0)
    minBtn.Parent = topBar
    
    local minCorner = Instance.new("UICorner")
    minCorner.CornerRadius = UDim.new(0, 4)
    minCorner.Parent = minBtn
    
    -- Auto-Destruct Button
    local killBtn = Instance.new("TextButton")
    killBtn.Size = UDim2.new(0.08, 0, 0.6, 0)
    killBtn.Position = UDim2.new(0.91, 0, 0.2, 0)
    killBtn.BackgroundColor3 = Color3.fromRGB(80, 0, 0)
    killBtn.TextColor3 = Color3.fromRGB(255, 100, 100)
    killBtn.Text = "✕"
    killBtn.TextSize = 18
    killBtn.Font = Enum.Font.GothamBold
    killBtn.BorderSizePixel = 1
    killBtn.BorderColor3 = Color3.fromRGB(200, 0, 0)
    killBtn.Parent = topBar
    
    local killCorner = Instance.new("UICorner")
    killCorner.CornerRadius = UDim.new(0, 4)
    killCorner.Parent = killBtn
    
    -- ========================================
    -- BUTTON CREATOR
    -- ========================================
    local function makeButton(text, yPos, bgColor, borderColor)
        local btn = Instance.new("TextButton")
        btn.Size = UDim2.new(0.85, 0, 0.10, 0)
        btn.Position = UDim2.new(0.075, 0, yPos, 0)
        btn.BackgroundColor3 = bgColor
        btn.TextColor3 = Color3.fromRGB(255, 255, 255)
        btn.Text = text
        btn.TextScaled = true
        btn.Font = Enum.Font.GothamBold
        btn.BorderSizePixel = 1
        btn.BorderColor3 = borderColor
        btn.Parent = mainFrame
        
        local corner = Instance.new("UICorner")
        corner.CornerRadius = UDim.new(0, 5)
        corner.Parent = btn
        
        return btn
    end
    
    -- ========================================
    -- BUTTONS
    -- ========================================
    local playersBtn = makeButton("[ON] Players", 0.14, Color3.fromRGB(0, 40, 80), Color3.fromRGB(0, 80, 150))
    local botsBtn = makeButton("[ON] Bots", 0.25, Color3.fromRGB(80, 0, 0), Color3.fromRGB(150, 0, 0))
    local house1Btn = makeButton("[ON] House I", 0.36, Color3.fromRGB(0, 60, 0), Color3.fromRGB(0, 150, 0))
    local house2Btn = makeButton("[ON] House II", 0.47, Color3.fromRGB(80, 60, 0), Color3.fromRGB(150, 100, 0))
    local mansionBtn = makeButton("[ON] Mansion", 0.58, Color3.fromRGB(80, 0, 60), Color3.fromRGB(150, 0, 100))
    local trapsBtn = makeButton("[ON] Traps", 0.69, Color3.fromRGB(80, 30, 0), Color3.fromRGB(150, 60, 0))
    local minimapBtn = makeButton("[ON] Minimap", 0.80, Color3.fromRGB(0, 40, 80), Color3.fromRGB(0, 80, 150))
    local clearBtn = makeButton("[OFF] Disable All", 0.91, Color3.fromRGB(40, 40, 40), Color3.fromRGB(80, 80, 80))
    
    -- ========================================
    -- MINIMAP
    -- ========================================
    local minimapGui = Instance.new("ScreenGui")
    minimapGui.Parent = LocalPlayer:WaitForChild("PlayerGui")
    minimapGui.ResetOnSpawn = false
    minimapGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
    
    local minimapFrame = Instance.new("Frame")
    minimapFrame.Size = UDim2.new(0, 180, 0, 180)
    minimapFrame.Position = UDim2.new(0.77, 0, 0.05, 0)
    minimapFrame.BackgroundColor3 = Color3.fromRGB(10, 0, 10)
    minimapFrame.BackgroundTransparency = 0.15
    minimapFrame.BorderSizePixel = 2
    minimapFrame.BorderColor3 = Color3.fromRGB(180, 0, 0)
    minimapFrame.Parent = minimapGui
    
    local mmCorner = Instance.new("UICorner")
    mmCorner.CornerRadius = UDim.new(0, 10)
    mmCorner.Parent = minimapFrame
    
    local mmGrad = Instance.new("UIGradient")
    mmGrad.Color = ColorSequence.new({
        ColorSequenceKeypoint.new(0, Color3.fromRGB(20, 0, 5)),
        ColorSequenceKeypoint.new(0.5, Color3.fromRGB(30, 0, 10)),
        ColorSequenceKeypoint.new(1, Color3.fromRGB(15, 0, 5))
    })
    mmGrad.Parent = minimapFrame
    
    local mmTitle = Instance.new("TextLabel")
    mmTitle.Size = UDim2.new(1, 0, 0.12, 0)
    mmTitle.Position = UDim2.new(0, 0, 0, 0)
    mmTitle.BackgroundColor3 = Color3.fromRGB(40, 0, 0)
    mmTitle.BackgroundTransparency = 0.5
    mmTitle.Text = "Minimap"
    mmTitle.TextColor3 = Color3.fromRGB(255, 150, 150)
    mmTitle.TextScaled = true
    mmTitle.Font = Enum.Font.GothamBold
    mmTitle.Parent = minimapFrame
    
    local mmClose = Instance.new("TextButton")
    mmClose.Size = UDim2.new(0.12, 0, 0.08, 0)
    mmClose.Position = UDim2.new(0.86, 0, 0.02, 0)
    mmClose.BackgroundColor3 = Color3.fromRGB(80, 0, 0)
    mmClose.TextColor3 = Color3.fromRGB(255, 100, 100)
    mmClose.Text = "X"
    mmClose.TextSize = 14
    mmClose.Font = Enum.Font.GothamBold
    mmClose.BorderSizePixel = 1
    mmClose.BorderColor3 = Color3.fromRGB(200, 0, 0)
    mmClose.Parent = minimapFrame
    
    mmClose.MouseButton1Click:Connect(function()
        minimapFrame.Visible = not minimapFrame.Visible
    end)
    
    local dotContainer = {}
    local minimapEnabled = true
    local mmLoop = nil
    
    -- Update Minimap
    local function updateMinimap()
        for _, dot in pairs(dotContainer) do
            pcall(function() dot:Destroy() end)
        end
        dotContainer = {}
        
        local cam = workspace.CurrentCamera
        local char = LocalPlayer.Character
        local root = char and char:FindFirstChild("HumanoidRootPart")
        if not root then return end
        
        local myPos = root.Position
        local scale = 1 / 30
        
        local function addDot(pos, color, size)
            local dx = (pos.X - myPos.X) * scale
            local dz = (pos.Z - myPos.Z) * scale
            if math.abs(dx) > 0.5 or math.abs(dz) > 0.5 then return end
            
            local dot = Instance.new("Frame")
            dot.Size = UDim2.new(0, size or 8, 0, size or 8)
            dot.Position = UDim2.new(0.5 + dx - 0.02, 0, 0.5 + dz - 0.02, 0)
            dot.BackgroundColor3 = color
            dot.BackgroundTransparency = 0
            dot.BorderSizePixel = 0
            dot.Parent = minimapFrame
            
            local dc = Instance.new("UICorner")
            dc.CornerRadius = UDim.new(1, 0)
            dc.Parent = dot
            
            table.insert(dotContainer, dot)
        end
        
        -- Player (You)
        addDot(myPos, Color3.fromRGB(0, 100, 255), 10)
        
        -- Other players
        for _, player in ipairs(Players:GetPlayers()) do
            if player ~= LocalPlayer and player.Character then
                local rootPart = player.Character:FindFirstChild("HumanoidRootPart")
                if rootPart then
                    local name = player.Name:lower()
                    if string.find(name, "granny") or string.find(name, "grandma") or string.find(name, "grandpa") or string.find(name, "slendrina") then
                        addDot(rootPart.Position, Color3.fromRGB(255, 0, 0), 10)
                    else
                        addDot(rootPart.Position, Color3.fromRGB(0, 255, 0), 8)
                    end
                end
            end
        end
    end
    
    mmLoop = RunService.Heartbeat:Connect(function()
        if minimapFrame and minimapFrame.Visible then
            updateMinimap()
        end
    end)
    
    -- ========================================
    -- BUTTON FUNCTIONS
    -- ========================================
    
    -- Minimap Toggle
    minimapBtn.MouseButton1Click:Connect(function()
        minimapEnabled = not minimapEnabled
        minimapBtn.Text = minimapEnabled and "[ON] Minimap" or "[OFF] Minimap"
        if minimapFrame then
            minimapFrame.Visible = minimapEnabled
        end
    end)
    
    -- Auto-Destruct
    killBtn.MouseButton1Click:Connect(function()
        for obj, _ in pairs(espObjects) do
            if espObjects[obj] then
                for _, espObj in pairs(espObjects[obj]) do
                    pcall(function() espObj:Destroy() end)
                end
                espObjects[obj] = nil
            end
        end
        pcall(function() gui:Destroy() end)
        pcall(function() minimapGui:Destroy() end)
        if mmLoop then pcall(function() mmLoop:Disconnect() end) end
        print("GRANNY ESP - DESTROYED")
    end)
    
    -- Minimize
    local function toggleMinimize()
        minimized = not minimized
        if minimized then
            mainFrame.Size = UDim2.new(0, 260, 0, 45)
            minBtn.Text = "+"
            playersBtn.Visible = false
            botsBtn.Visible = false
            house1Btn.Visible = false
            house2Btn.Visible = false
            mansionBtn.Visible = false
            trapsBtn.Visible = false
            minimapBtn.Visible = false
            clearBtn.Visible = false
        else
            mainFrame.Size = UDim2.new(0, 260, 0, 390)
            minBtn.Text = "_"
            playersBtn.Visible = true
            botsBtn.Visible = true
            house1Btn.Visible = true
            house2Btn.Visible = true
            mansionBtn.Visible = true
            trapsBtn.Visible = true
            minimapBtn.Visible = true
            clearBtn.Visible = true
        end
    end
    
    minBtn.MouseButton1Click:Connect(toggleMinimize)
    
    -- Players Toggle
    playersBtn.MouseButton1Click:Connect(function()
        settings.players = not settings.players
        playersBtn.Text = settings.players and "[ON] Players" or "[OFF] Players"
        playersBtn.BackgroundColor3 = settings.players and Color3.fromRGB(0, 40, 80) or Color3.fromRGB(30, 30, 30)
        if not settings.players then
            for obj, _ in pairs
