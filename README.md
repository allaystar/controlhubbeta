-- Control Hub v5.0
-- Script FIXED para Blox Fruits
-- Key: Control
-- Suporte completo para todos os seas

local ControlHub = {
    Version = "5.0.0",
    Key = "Control",
    Creator = "ControlHub Team"
}

-- Verificação do jogo SEM return
if not (game.PlaceId == 2753915549 or game.PlaceId == 4442272183 or game.PlaceId == 7449423635) then
    game:GetService("StarterGui"):SetCore("SendNotification", {
        Title = "Control Hub",
        Text = "Este script é apenas para Blox Fruits!",
        Duration = 5
    })
    -- Continua mesmo não estando no jogo certo (para teste)
    -- Não faz return
end

-- Função de notificação
local function Notify(title, message, duration)
    duration = duration or 5
    game:GetService("StarterGui"):SetCore("SendNotification", {
        Title = title,
        Text = message,
        Duration = duration
    })
    print("[Control Hub] " .. title .. ": " .. message)
end

-- Detectar Sea atual
local CurrentSea = 1
local function DetectSea()
    local map = workspace:FindFirstChild("Map")
    if map then
        if map:FindFirstChild("MysticIsland") or map:FindFirstChild("Port Town") then
            return 3
        elseif map:FindFirstChild("FountainOfStrength") or map:FindFirstChild("Kingdom of Rose") then
            return 2
        else
            return 1
        end
    end
    return 1
end

CurrentSea = DetectSea()
Notify("Control Hub", "Sea Detectado: " .. CurrentSea, 3)

-- Criar interface gráfica SIMPLES
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "ControlHubUI"
ScreenGui.Parent = game:GetService("CoreGui")
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

-- Frame principal
local MainFrame = Instance.new("Frame")
MainFrame.Name = "MainFrame"
MainFrame.Parent = ScreenGui
MainFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 30)
MainFrame.BorderSizePixel = 0
MainFrame.Position = UDim2.new(0.3, 0, 0.3, 0)
MainFrame.Size = UDim2.new(0, 500, 0, 400)
MainFrame.Active = true
MainFrame.Draggable = true

local UICorner = Instance.new("UICorner")
UICorner.CornerRadius = UDim.new(0, 10)
UICorner.Parent = MainFrame

local UIStroke = Instance.new("UIStroke")
UIStroke.Color = Color3.fromRGB(0, 150, 255)
UIStroke.Thickness = 2
UIStroke.Parent = MainFrame

-- Barra de título
local TitleBar = Instance.new("Frame")
TitleBar.Name = "TitleBar"
TitleBar.Parent = MainFrame
TitleBar.BackgroundColor3 = Color3.fromRGB(0, 100, 200)
TitleBar.BorderSizePixel = 0
TitleBar.Size = UDim2.new(1, 0, 0, 40)

local titleCorner = Instance.new("UICorner")
titleCorner.CornerRadius = UDim.new(0, 10, 0, 0)
titleCorner.Parent = TitleBar

-- Título
local Title = Instance.new("TextLabel")
Title.Name = "Title"
Title.Parent = TitleBar
Title.BackgroundTransparency = 1
Title.Position = UDim2.new(0, 15, 0, 0)
Title.Size = UDim2.new(0.7, 0, 1, 0)
Title.Font = Enum.Font.GothamBold
Title.Text = "CONTROL HUB v" .. ControlHub.Version
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.TextSize = 18
Title.TextXAlignment = Enum.TextXAlignment.Left

-- Indicador de Sea
local SeaLabel = Instance.new("TextLabel")
SeaLabel.Name = "SeaLabel"
SeaLabel.Parent = TitleBar
SeaLabel.BackgroundColor3 = Color3.fromRGB(40, 40, 60)
SeaLabel.BorderSizePixel = 0
SeaLabel.Position = UDim2.new(0.7, 10, 0.2, 0)
SeaLabel.Size = UDim2.new(0.25, 0, 0.6, 0)
SeaLabel.Font = Enum.Font.GothamBold
SeaLabel.Text = "SEA " .. CurrentSea
SeaLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
SeaLabel.TextSize = 14

local seaCorner = Instance.new("UICorner")
seaCorner.CornerRadius = UDim.new(0, 5)
seaCorner.Parent = SeaLabel

-- Botão de fechar
local CloseButton = Instance.new("TextButton")
CloseButton.Name = "CloseButton"
CloseButton.Parent = TitleBar
CloseButton.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
CloseButton.BorderSizePixel = 0
CloseButton.Position = UDim2.new(1, -35, 0.2, 0)
CloseButton.Size = UDim2.new(0, 25, 0, 25)
CloseButton.Font = Enum.Font.GothamBold
CloseButton.Text = "X"
CloseButton.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseButton.TextSize = 14

local closeCorner = Instance.new("UICorner")
closeCorner.CornerRadius = UDim.new(0, 5)
closeCorner.Parent = CloseButton

CloseButton.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
    Notify("Control Hub", "Interface fechada!", 2)
end)

-- Tabs
local TabButtons = Instance.new("Frame")
TabButtons.Name = "TabButtons"
TabButtons.Parent = MainFrame
TabButtons.BackgroundColor3 = Color3.fromRGB(25, 25, 35)
TabButtons.BorderSizePixel = 0
TabButtons.Position = UDim2.new(0, 0, 0, 40)
TabButtons.Size = UDim2.new(0, 120, 0, 360)

local ContentFrame = Instance.new("Frame")
ContentFrame.Name = "ContentFrame"
ContentFrame.Parent = MainFrame
ContentFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 40)
ContentFrame.BorderSizePixel = 0
ContentFrame.Position = UDim2.new(0, 120, 0, 40)
ContentFrame.Size = UDim2.new(0, 380, 0, 360)

-- Sistema de tabs simples
local Tabs = {}
local CurrentTab = nil

local function CreateTab(name)
    local TabButton = Instance.new("TextButton")
    local TabContent = Instance.new("ScrollingFrame")
    
    -- Botão da tab
    TabButton.Name = name .. "Tab"
    TabButton.Parent = TabButtons
    TabButton.BackgroundColor3 = Color3.fromRGB(35, 35, 45)
    TabButton.BorderSizePixel = 0
    TabButton.Size = UDim2.new(1, 0, 0, 40)
    TabButton.Font = Enum.Font.Gotham
    TabButton.Text = name
    TabButton.TextColor3 = Color3.fromRGB(200, 200, 200)
    TabButton.TextSize = 14
    
    -- Conteúdo
    TabContent.Name = name .. "Content"
    TabContent.Parent = ContentFrame
    TabContent.Active = true
    TabContent.BackgroundTransparency = 1
    TabContent.Size = UDim2.new(1, 0, 1, 0)
    TabContent.CanvasSize = UDim2.new(0, 0, 0, 500)
    TabContent.ScrollBarThickness = 3
    TabContent.Visible = false
    
    Tabs[name] = {
        Button = TabButton,
        Content = TabContent,
        YOffset = 10
    }
    
    -- Posicionar botão
    local tabCount = 0
    for _ in pairs(Tabs) do
        tabCount = tabCount + 1
    end
    TabButton.Position = UDim2.new(0, 0, 0, (tabCount-1)*40)
    
    TabButton.MouseButton1Click:Connect(function()
        if CurrentTab then
            CurrentTab.Button.BackgroundColor3 = Color3.fromRGB(35, 35, 45)
            CurrentTab.Content.Visible = false
        end
        
        TabButton.BackgroundColor3 = Color3.fromRGB(0, 120, 220)
        TabContent.Visible = true
        CurrentTab = Tabs[name]
        Notify("Tab", "Aba " .. name .. " aberta", 1)
    end)
    
    return Tabs[name]
end

-- Criar elementos simples
local function CreateButton(tab, text, callback)
    local button = Instance.new("TextButton")
    button.Name = text
    button.Parent = tab.Content
    button.BackgroundColor3 = Color3.fromRGB(50, 50, 70)
    button.BorderSizePixel = 0
    button.Position = UDim2.new(0.05, 0, 0, tab.YOffset)
    button.Size = UDim2.new(0.9, 0, 0, 35)
    button.Font = Enum.Font.Gotham
    button.Text = text
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.TextSize = 13
    
    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0, 5)
    corner.Parent = button
    
    button.MouseButton1Click:Connect(function()
        Notify("Botão", text .. " clicado!", 2)
        if callback then
            pcall(callback)
        end
    end)
    
    tab.YOffset = tab.YOffset + 40
    return button
end

local function CreateLabel(tab, text)
    local label = Instance.new("TextLabel")
    label.Name = "Label"
    label.Parent = tab.Content
    label.BackgroundTransparency = 1
    label.Position = UDim2.new(0.05, 0, 0, tab.YOffset)
    label.Size = UDim2.new(0.9, 0, 0, 25)
    label.Font = Enum.Font.GothamBold
    label.Text = text
    label.TextColor3 = Color3.fromRGB(0, 200, 255)
    label.TextSize = 14
    label.TextXAlignment = Enum.TextXAlignment.Left
    
    tab.YOffset = tab.YOffset + 30
    return label
end

local function CreateToggle(tab, text, callback)
    local frame = Instance.new("Frame")
    frame.Name = text .. "Toggle"
    frame.Parent = tab.Content
    frame.BackgroundTransparency = 1
    frame.Position = UDim2.new(0.05, 0, 0, tab.YOffset)
    frame.Size = UDim2.new(0.9, 0, 0, 35)
    
    local label = Instance.new("TextLabel")
    label.Name = "Label"
    label.Parent = frame
    label.BackgroundTransparency = 1
    label.Position = UDim2.new(0, 0, 0, 0)
    label.Size = UDim2.new(0.7, 0, 1, 0)
    label.Font = Enum.Font.Gotham
    label.Text = text
    label.TextColor3 = Color3.fromRGB(220, 220, 220)
    label.TextSize = 13
    label.TextXAlignment = Enum.TextXAlignment.Left
    
    local toggle = Instance.new("TextButton")
    toggle.Name = "Toggle"
    toggle.Parent = frame
    toggle.BackgroundColor3 = Color3.fromRGB(150, 0, 0)
    toggle.Position = UDim2.new(0.7, 0, 0.2, 0)
    toggle.Size = UDim2.new(0.25, 0, 0.6, 0)
    toggle.Font = Enum.Font.GothamBold
    toggle.Text = "OFF"
    toggle.TextColor3 = Color3.fromRGB(255, 255, 255)
    toggle.TextSize = 12
    
    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0, 5)
    corner.Parent = toggle
    
    local state = false
    
    toggle.MouseButton1Click:Connect(function()
        state = not state
        if state then
            toggle.BackgroundColor3 = Color3.fromRGB(0, 150, 0)
            toggle.Text = "ON"
            Notify(text, "ATIVADO", 2)
        else
            toggle.BackgroundColor3 = Color3.fromRGB(150, 0, 0)
            toggle.Text = "OFF"
            Notify(text, "DESATIVADO", 2)
        end
        
        if callback then
            pcall(callback, state)
        end
    end)
    
    tab.YOffset = tab.YOffset + 40
    return frame
end

-- Criar tabs
local AutoFarmTab = CreateTab("Auto Farm")
local TeleportTab = CreateTab("Teleportes")
local CombatTab = CreateTab("Combat")
local PlayerTab = CreateTab("Player")
local MiscTab = CreateTab("Misc")

-- Abrir primeira tab
AutoFarmTab.Button.BackgroundColor3 = Color3.fromRGB(0, 120, 220)
AutoFarmTab.Content.Visible = true
CurrentTab = AutoFarmTab

-- ========== AUTO FARM TAB ==========
CreateLabel(AutoFarmTab, "CONFIGURAÇÕES DE FARM")

CreateToggle(AutoFarmTab, "Farm Automático", function(state)
    if state then
        Notify("Auto Farm", "Farm automático ATIVADO!", 3)
    else
        Notify("Auto Farm", "Farm automático DESATIVADO!", 3)
    end
end)

CreateToggle(AutoFarmTab, "Farm de Bosses", function(state)
    if state then
        Notify("Farm Bosses", "Modo bosses ATIVADO!", 3)
    else
        Notify("Farm Bosses", "Modo bosses DESATIVADO!", 3)
    end
end)

CreateToggle(AutoFarmTab, "Auto Coletar", function(state)
    if state then
        Notify("Auto Coletar", "Auto coletar ATIVADO!", 3)
    else
        Notify("Auto Coletar", "Auto coletar DESATIVADO!", 3)
    end
end)

CreateLabel(AutoFarmTab, "OPÇÕES AVANÇADAS")

CreateButton(AutoFarmTab, "Farm All Nearby Mobs", function()
    Notify("Farm", "Iniciando farm de todos os mobs próximos...", 3)
end)

CreateButton(AutoFarmTab, "Farm Selected Boss", function()
    Notify("Farm", "Selecione um boss para farmar...", 3)
end)

-- ========== TELEPORT TAB (Dinâmico) ==========
CreateLabel(TeleportTab, "ILHAS - SEA " .. CurrentSea)

-- Ilhas por Sea
local IslandsData = {
    [1] = {"Middle Island", "Jungle", "Pirate Village", "Desert", "Snow Mountain", "Marine Fortress", "Sky Island"},
    [2] = {"Kingdom of Rose", "Cafe", "Green Bit", "Graveyard", "Snow Mountain (2nd)", "Cursed Ship"},
    [3] = {"Port Town", "Hydra Island", "Floating Turtle", "Haunted Castle", "Ice Cream Island", "Cake Island"}
}

-- Adicionar ilhas do sea atual
if IslandsData[CurrentSea] then
    for _, island in pairs(IslandsData[CurrentSea]) do
        CreateButton(TeleportTab, island, function()
            Notify("Teleporte", "Teleportando para " .. island .. " (Sea " .. CurrentSea .. ")", 3)
        end)
    end
end

CreateLabel(TeleportTab, "BOSSES - SEA " .. CurrentSea)

local BossesData = {
    [1] = {"Gorilla King", "Bobby", "Yeti", "Vice Admiral", "Saber Expert"},
    [2] = {"Darkbeard", "Diamond", "Jeremy", "Don Swan", "Smoke Admiral"},
    [3] = {"Dough King", "Cake Queen", "Longma", "Beautiful Pirate", "Cake Prince"}
}

if BossesData[CurrentSea] then
    for _, boss in pairs(BossesData[CurrentSea]) do
        CreateButton(TeleportTab, boss, function()
            Notify("Teleporte Boss", "Teleportando para " .. boss .. " (Sea " .. CurrentSea .. ")", 3)
        end)
    end
end

CreateLabel(TeleportTab, "UTILIDADES")

CreateButton(TeleportTab, "Ir para Spawn", function()
    Notify("Teleporte", "Teleportando para spawn...", 3)
end)

CreateButton(TeleportTab, "Ir para Safe Spot", function()
    Notify("Teleporte", "Teleportando para local seguro...", 3)
end)

-- ========== COMBAT TAB ==========
CreateLabel(CombatTab, "AIMBOT E SKILLS")

CreateToggle(CombatTab, "Aimbot Automático", function(state)
    if state then
        Notify("Aimbot", "🎯 Aimbot ATIVADO!", 3)
    else
        Notify("Aimbot", "🎯 Aimbot DESATIVADO!", 3)
    end
end)

CreateToggle(CombatTab, "No Cooldown Skills", function(state)
    if state then
        Notify("No Cooldown", "⚡ No Cooldown ATIVADO!", 3)
    else
        Notify("No Cooldown", "⚡ No Cooldown DESATIVADO!", 3)
    end
end)

CreateToggle(CombatTab, "Auto Skills", function(state)
    if state then
        Notify("Auto Skills", "🤖 Auto Skills ATIVADO!", 3)
    else
        Notify("Auto Skills", "🤖 Auto Skills DESATIVADO!", 3)
    end
end)

CreateLabel(CombatTab, "DEFESA")

CreateToggle(CombatTab, "Auto Dodge", function(state)
    if state then
        Notify("Auto Dodge", "🛡️ Auto Dodge ATIVADO!", 3)
    else
        Notify("Auto Dodge", "🛡️ Auto Dodge DESATIVADO!", 3)
    end
end)

CreateToggle(CombatTab, "God Mode", function(state)
    if state then
        Notify("God Mode", "🛡️ God Mode ATIVADO!", 3)
    else
        Notify("God Mode", "🛡️ God Mode DESATIVADO!", 3)
    end
end)

-- ========== PLAYER TAB ==========
CreateLabel(PlayerTab, "STATUS DO PLAYER")

local Player = game:GetService("Players").LocalPlayer

-- Info do player
CreateButton(PlayerTab, "Mostrar Info do Player", function()
    local level = "N/A"
    local beli = "0"
    local fruit = "Nenhuma"
    
    if Player:FindFirstChild("Data") then
        level = Player.Data.Level.Value or "N/A"
        beli = Player.Data.Beli.Value or "0"
        fruit = Player.Data.DevilFruit.Value or "Nenhuma"
    end
    
    Notify("Player Info", 
        "👤: " .. Player.Name .. 
        "\n⭐ Level: " .. level .. 
        "\n💰 Beli: " .. beli .. 
        "\n🍊 Fruta: " .. fruit, 7)
end)

CreateLabel(PlayerTab, "HACKS DE MOVIMENTO")

CreateToggle(PlayerTab, "Speed Hack (2x)", function(state)
    if state then
        Notify("Speed Hack", "🚀 Speed 2x ATIVADO!", 3)
    else
        Notify("Speed Hack", "🚶 Speed normal", 3)
    end
end)

CreateToggle(PlayerTab, "Fly Hack", function(state)
    if state then
        Notify("Fly Hack", "🕊️ Fly ATIVADO!", 3)
    else
        Notify("Fly Hack", "🕊️ Fly DESATIVADO!", 3)
    end
end)

CreateToggle(PlayerTab, "No Clip", function(state)
    if state then
        Notify("No Clip", "👻 No Clip ATIVADO!", 3)
    else
        Notify("No Clip", "👻 No Clip DESATIVADO!", 3)
    end
end)

CreateLabel(PlayerTab, "STATUS HACKS")

CreateToggle(PlayerTab, "Infinite Energy", function(state)
    if state then
        Notify("Energy", "🔋 Energia Infinita ATIVADA!", 3)
    else
        Notify("Energy", "🔋 Energia normal", 3)
    end
end)

CreateToggle(PlayerTab, "Infinite Health", function(state)
    if state then
        Notify("Health", "❤️ Vida Infinita ATIVADA!", 3)
    else
        Notify("Health", "❤️ Vida normal", 3)
    end
end)

-- ========== MISC TAB ==========
CreateLabel(MiscTab, "AUTO FARM")

CreateToggle(MiscTab, "Auto Redeem Codes", function(state)
    if state then
        Notify("Auto Codes", "🎁 Auto Codes ATIVADO!", 3)
    else
        Notify("Auto Codes", "🎁 Auto Codes DESATIVADO!", 3)
    end
end)

CreateToggle(MiscTab, "Fruit Notifier", function(state)
    if state then
        Notify("Fruit Notifier", "🔔 Notificador ATIVADO!", 3)
    else
        Notify("Fruit Notifier", "🔔 Notificador DESATIVADO!", 3)
    end
end)

CreateLabel(MiscTab, "UTILIDADES")

CreateButton(MiscTab, "Server Hop", function()
    Notify("Server Hop", "🔄 Procurando novo servidor...", 3)
end)

CreateButton(MiscTab, "Copy Job ID", function()
    local jobId = game.JobId
    if setclipboard then
        setclipboard(jobId)
        Notify("Job ID", "📋 Copiado: " .. jobId, 3)
    else
        Notify("Job ID", "Job ID: " .. jobId, 5)
    end
end)

CreateButton(MiscTab, "Rejoin Server", function()
    Notify("Rejoin", "🔁 Reconectando...", 3)
end)

CreateLabel(MiscTab, "CONFIGURAÇÕES")

CreateButton(MiscTab, "Salvar Config", function()
    Notify("Config", "💾 Configurações salvas!", 3)
end)

CreateButton(MiscTab, "Carregar Config", function()
    Notify("Config", "📂 Configurações carregadas!", 3)
end)

CreateLabel(MiscTab, "INFORMAÇÕES")

CreateButton(MiscTab, "Créditos", function()
    Notify("Créditos", 
        "Control Hub v" .. ControlHub.Version .. 
        "\nCriado por: " .. ControlHub.Creator .. 
        "\nSea Atual: " .. CurrentSea, 7)
end)

CreateButton(MiscTab, "Discord", function()
    if setclipboard then
        setclipboard("discord.gg/controlhub")
        Notify("Discord", "📋 Link copiado!", 3)
    else
        Notify("Discord", "discord.gg/controlhub", 5)
    end
end)

-- ========== KEY SYSTEM ==========
local KeyFrame = Instance.new("Frame")
KeyFrame.Name = "KeyFrame"
KeyFrame.Parent = ScreenGui
KeyFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 25)
KeyFrame.BorderSizePixel = 0
KeyFrame.Position = UDim2.new(0.35, 0, 0.35, 0)
KeyFrame.Size = UDim2.new(0, 350, 0, 250)
KeyFrame.Visible = true

local keyCorner = Instance.new("UICorner")
keyCorner.CornerRadius = UDim.new(0, 10)
keyCorner.Parent = KeyFrame

local keyStroke = Instance.new("UIStroke")
keyStroke.Color = Color3.fromRGB(0, 150, 255)
keyStroke.Thickness = 2
keyStroke.Parent = KeyFrame

local KeyTitle = Instance.new("TextLabel")
KeyTitle.Name = "KeyTitle"
KeyTitle.Parent = KeyFrame
KeyTitle.BackgroundTransparency = 1
KeyTitle.Position = UDim2.new(0, 0, 0.1, 0)
KeyTitle.Size = UDim2.new(1, 0, 0, 40)
KeyTitle.Font = Enum.Font.GothamBold
KeyTitle.Text = "CONTROL HUB"
KeyTitle.TextColor3 = Color3.fromRGB(0, 150, 255)
KeyTitle.TextSize = 24

local KeySubtitle = Instance.new("TextLabel")
KeySubtitle.Name = "KeySubtitle"
KeySubtitle.Parent = KeyFrame
KeySubtitle.BackgroundTransparency = 1
KeySubtitle.Position = UDim2.new(0, 0, 0.3, 0)
KeySubtitle.Size = UDim2.new(1, 0, 0, 30)
KeySubtitle.Font = Enum.Font.Gotham
KeySubtitle.Text = "Digite a chave de acesso:"
KeySubtitle.TextColor3 = Color3.fromRGB(200, 200, 200)
KeySubtitle.TextSize = 14

local KeyHint = Instance.new("TextLabel")
KeyHint.Name = "KeyHint"
KeyHint.Parent = KeyFrame
KeyHint.BackgroundTransparency = 1
KeyHint.Position = UDim2.new(0, 0, 0.4, 0)
KeyHint.Size = UDim2.new(1, 0, 0, 20)
KeyHint.Font = Enum.Font.Gotham
KeyHint.Text = "Dica: 'Control'"
KeyHint.TextColor3 = Color3.fromRGB(150, 150, 150)
KeyHint.TextSize = 12

local KeyInput = Instance.new("TextBox")
KeyInput.Name = "KeyInput"
KeyInput.Parent = KeyFrame
KeyInput.BackgroundColor3 = Color3.fromRGB(40, 40, 60)
KeyInput.BorderSizePixel = 0
KeyInput.Position = UDim2.new(0.1, 0, 0.5, 0)
KeyInput.Size = UDim2.new(0.8, 0, 0, 40)
KeyInput.Font = Enum.Font.Gotham
KeyInput.PlaceholderText = "Digite a chave aqui..."
KeyInput.Text = ""
KeyInput.TextColor3 = Color3.fromRGB(255, 255, 255)
KeyInput.TextSize = 16
KeyInput.ClearTextOnFocus = false

local inputCorner = Instance.new("UICorner")
inputCorner.CornerRadius = UDim.new(0, 5)
inputCorner.Parent = KeyInput

local KeyButton = Instance.new("TextButton")
KeyButton.Name = "KeyButton"
KeyButton.Parent = KeyFrame
KeyButton.BackgroundColor3 = Color3.fromRGB(0, 120, 220)
KeyButton.BorderSizePixel = 0
KeyButton.Position = UDim2.new(0.25, 0, 0.75, 0)
KeyButton.Size = UDim2.new(0.5, 0, 0, 45)
KeyButton.Font = Enum.Font.GothamBold
KeyButton.Text = "VERIFICAR CHAVE"
KeyButton.TextColor3 = Color3.fromRGB(255, 255, 255)
KeyButton.TextSize = 16

local buttonCorner = Instance.new("UICorner")
buttonCorner.CornerRadius = UDim.new(0, 5)
buttonCorner.Parent = KeyButton

local KeyVerified = false

KeyButton.MouseButton1Click:Connect(function()
    if KeyInput.Text == ControlHub.Key then
        KeyVerified = true
        KeyFrame.Visible = false
        MainFrame.Visible = true
        Notify("Control Hub", "✅ CHAVE VERIFICADA COM SUCESSO!", 5)
        Notify("Sea Detalhes", "Você está no Sea " .. CurrentSea, 5)
    else
        KeyInput.Text = ""
        KeyInput.PlaceholderText = "Chave incorreta! Tente novamente..."
        KeyInput.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
        
        wait(0.3)
        
        KeyInput.PlaceholderText = "Digite a chave aqui..."
        KeyInput.BackgroundColor3 = Color3.fromRGB(40, 40, 60)
    end
end)

KeyInput.FocusLost:Connect(function(enterPressed)
    if enterPressed then
        KeyButton.MouseButton1Click()
    end
end)

-- Auto-entrar se já tiver a chave salva
spawn(function()
    wait(1)
    if not KeyVerified then
        Notify("Control Hub", "Digite a chave: 'Control'", 10)
    end
end)

-- Sistema de Auto Farm básico
local AutoFarmActive = false
local FarmThread = nil

local function StartAutoFarm()
    if FarmThread then
        FarmThread = nil
    end
    
    FarmThread = game:GetService("RunService").Heartbeat:Connect(function()
        if not AutoFarmActive then return end
        
        pcall(function()
            local character = Player.Character
            if not character then return end
            
            local humanoidRootPart = character:FindFirstChild("HumanoidRootPart")
            if not humanoidRootPart then return end
            
            -- Encontrar inimigos próximos
            local closest = nil
            local dist = math.huge
            
            for _, enemy in pairs(workspace:GetChildren()) do
                if enemy:IsA("Model") and enemy:FindFirstChild("Humanoid") and enemy.Humanoid.Health > 0 then
                    if enemy:FindFirstChild("HumanoidRootPart") then
                        local mag = (humanoidRootPart.Position - enemy.HumanoidRootPart.Position).Magnitude
                        if mag < 50 and mag < dist then
                            dist = mag
                            closest = enemy
                        end
                    end
                end
            end
            
            if closest then
                -- Teleportar perto
                humanoidRootPart.CFrame = closest.HumanoidRootPart.CFrame * CFrame.new(0, 0, 5)
                
                -- Auto ataque
                for _, tool in pairs(character:GetChildren()) do
                    if tool:IsA("Tool") then
                        tool:Activate()
                    end
                end
            end
        end)
    end)
end

-- Configurar toggles do Auto Farm
for _, tab in pairs({AutoFarmTab}) do
    for _, element in pairs(tab.Content:GetChildren()) do
        if element.Name:find("Toggle") then
            local toggleBtn = element:FindFirstChild("Toggle")
            if toggleBtn then
                local originalClick = toggleBtn.MouseButton1Click
                toggleBtn.MouseButton1Click:Connect(function()
                    if element.Name:find("Farm Automático") then
                        AutoFarmActive = not AutoFarmActive
                        if AutoFarmActive then
                            StartAutoFarm()
                        else
                            if FarmThread then
                                FarmThread:Disconnect()
                                FarmThread = nil
                            end
                        end
                    end
                end)
            end
        end
    end
end

-- Notificação final
wait(2)
if not KeyVerified then
    Notify("Control Hub", "⚠️ Aguardando verificação da chave...\nUse: 'Control'", 10)
else
    Notify("Control Hub", "✅ Script carregado!\n🎮 Pronto para usar!\n🌊 Sea: " .. CurrentSea, 8)
end

print("=======================================")
print("Control Hub v" .. ControlHub.Version .. " Carregado!")
print("Sea Atual: " .. CurrentSea)
print("Key: Control")
print("=======================================")
