local Players = game:GetService("Players")
local CoreGui = game:GetService("CoreGui")
local UserInputService = game:GetService("UserInputService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local LocalPlayer = Players.LocalPlayer

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Parent = CoreGui
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
ScreenGui.Name = "AuraSystemGui"

-- PAINEL PRINCIPAL (AURA SYSTEM)
local MainFrame = Instance.new("Frame")
local UICorner = Instance.new("UICorner")
local UIStroke = Instance.new("UIStroke")
local Title = Instance.new("TextLabel")
local FarmAuraToggle = Instance.new("TextButton")
local FarmAuraCorner = Instance.new("UICorner")

MainFrame.Name = "MainFrame"
MainFrame.Parent = ScreenGui
MainFrame.BackgroundColor3 = Color3.fromRGB(18, 18, 18)
MainFrame.Position = UDim2.new(0.5, -110, 0.5, -60)
MainFrame.Size = UDim2.new(0, 220, 0, 115)
MainFrame.Active = true
MainFrame.Draggable = true

UICorner.CornerRadius = UDim.new(0, 8)
UICorner.Parent = MainFrame

UIStroke.Color = Color3.fromRGB(45, 45, 45)
UIStroke.Thickness = 1.5
UIStroke.Parent = MainFrame

Title.Name = "Title"
Title.Parent = MainFrame
Title.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
Title.BackgroundTransparency = 1.00
Title.Position = UDim2.new(0, 0, 0, 10)
Title.Size = UDim2.new(0, 220, 0, 25)
Title.Font = Enum.Font.GothamBold
Title.Text = "AURA SYSTEM"
Title.TextColor3 = Color3.fromRGB(240, 240, 240)
Title.TextSize = 14.00

FarmAuraToggle.Name = "FarmAuraToggle"
FarmAuraToggle.Parent = MainFrame
FarmAuraToggle.BackgroundColor3 = Color3.fromRGB(28, 28, 28)
FarmAuraToggle.Position = UDim2.new(0, 15, 0, 45)
FarmAuraToggle.Size = UDim2.new(0, 190, 0, 45)
FarmAuraToggle.Font = Enum.Font.GothamSemibold
FarmAuraToggle.Text = "Farm Aura: OFF"
FarmAuraToggle.TextColor3 = Color3.fromRGB(200, 50, 50)
FarmAuraToggle.TextSize = 13.00

FarmAuraCorner.CornerRadius = UDim.new(0, 6)
FarmAuraCorner.Parent = FarmAuraToggle

local farmAuraRunning = false

FarmAuraToggle.MouseButton1Click:Connect(function()
    farmAuraRunning = not farmAuraRunning
    if farmAuraRunning then
        FarmAuraToggle.Text = "Farm Aura: ON"
        FarmAuraToggle.TextColor3 = Color3.fromRGB(50, 200, 50)
    else
        FarmAuraToggle.Text = "Farm Aura: OFF"
        FarmAuraToggle.TextColor3 = Color3.fromRGB(200, 50, 50)
    end
end)

task.spawn(function()
    while true do
        if farmAuraRunning then
            pcall(function()
                game:GetService("ReplicatedStorage"):WaitForChild("Events"):WaitForChild("Farm"):FireServer()
            end)
            task.wait(0.2)
            pcall(function()
                game:GetService("ReplicatedStorage"):WaitForChild("Events"):WaitForChild("Energy"):FireServer()
            end)
            task.wait(2)
            pcall(function()
                game:GetService("ReplicatedStorage"):WaitForChild("Events"):WaitForChild("Rebirth"):InvokeServer()
            end)
        end
        task.wait(0.1)
    end
end)

-- CHAT GLOBAL INTEGRADO
local ChatFrame = Instance.new("Frame")
local ChatCorner = Instance.new("UICorner")
local ChatStroke = Instance.new("UIStroke")
local ChatTitle = Instance.new("TextLabel")
local ChatContainer = Instance.new("ScrollingFrame")
local UIListLayout = Instance.new("UIListLayout")
local InputBox = Instance.new("TextBox")
local InputCorner = Instance.new("UICorner")
local SendButton = Instance.new("TextButton")
local SendCorner = Instance.new("UICorner")
local ScriptToggle = Instance.new("TextButton")
local ScriptToggleCorner = Instance.new("UICorner")

ChatFrame.Name = "GlobalChatFrame"
ChatFrame.Parent = ScreenGui
ChatFrame.BackgroundColor3 = Color3.fromRGB(18, 18, 18)
ChatFrame.Position = UDim2.new(0.5, 120, 0.5, -130)
ChatFrame.Size = UDim2.new(0, 350, 0, 260)
ChatFrame.Active = true
ChatFrame.Draggable = true

ChatCorner.CornerRadius = UDim.new(0, 8)
ChatCorner.Parent = ChatFrame

ChatStroke.Color = Color3.fromRGB(45, 45, 45)
ChatStroke.Thickness = 1.5
ChatStroke.Parent = ChatFrame

ChatTitle.Name = "Title"
ChatTitle.Parent = ChatFrame
ChatTitle.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
ChatTitle.BackgroundTransparency = 1.00
ChatTitle.Position = UDim2.new(0, 0, 0, 8)
ChatTitle.Size = UDim2.new(0, 350, 0, 20)
ChatTitle.Font = Enum.Font.GothamBold
ChatTitle.Text = "GLOBAL SCRIPT CHAT"
ChatTitle.TextColor3 = Color3.fromRGB(240, 240, 240)
ChatTitle.TextSize = 13.00

ChatContainer.Name = "ChatContainer"
ChatContainer.Parent = ChatFrame
ChatContainer.Active = true
ChatContainer.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
ChatContainer.BorderSizePixel = 0
ChatContainer.Position = UDim2.new(0, 10, 0, 35)
ChatContainer.Size = UDim2.new(0, 330, 0, 170)
ChatContainer.CanvasSize = UDim2.new(0, 0, 0, 0)
ChatContainer.ScrollBarThickness = 4

UIListLayout.Parent = ChatContainer
UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
UIListLayout.Padding = UDim.new(0, 6)

InputBox.Name = "InputBox"
InputBox.Parent = ChatFrame
InputBox.BackgroundColor3 = Color3.fromRGB(28, 28, 28)
InputBox.Position = UDim2.new(0, 10, 0, 215)
InputBox.Size = UDim2.new(0, 210, 0, 35)
InputBox.Font = Enum.Font.Gotham
InputBox.PlaceholderText = "Digite sua mensagem..."
InputBox.PlaceholderColor3 = Color3.fromRGB(100, 100, 100)
InputBox.Text = ""
InputBox.TextColor3 = Color3.fromRGB(230, 230, 230)
InputBox.TextSize = 12.00
InputBox.TextXAlignment = Enum.TextXAlignment.Left

InputCorner.CornerRadius = UDim.new(0, 6)
InputCorner.Parent = InputBox

ScriptToggle.Name = "ScriptToggle"
ScriptToggle.Parent = ChatFrame
ScriptToggle.BackgroundColor3 = Color3.fromRGB(28, 28, 28)
ScriptToggle.Position = UDim2.new(0, 225, 0, 215)
ScriptToggle.Size = UDim2.new(0, 35, 0, 35)
ScriptToggle.Font = Enum.Font.GothamBold
ScriptToggle.Text = "</>"
ScriptToggle.TextColor3 = Color3.fromRGB(200, 50, 50)
ScriptToggle.TextSize = 11.00

ScriptToggleCorner.CornerRadius = UDim.new(0, 6)
ScriptToggleCorner.Parent = ScriptToggle

SendButton.Name = "SendButton"
SendButton.Parent = ChatFrame
SendButton.BackgroundColor3 = Color3.fromRGB(45, 120, 255)
SendButton.Position = UDim2.new(0, 265, 0, 215)
SendButton.Size = UDim2.new(0, 75, 0, 35)
SendButton.Font = Enum.Font.GothamBold
SendButton.Text = "Enviar"
SendButton.TextColor3 = Color3.fromRGB(255, 255, 255)
SendButton.TextSize = 12.00

SendCorner.CornerRadius = UDim.new(0, 6)
SendCorner.Parent = SendButton

local isScriptMode = false

ScriptToggle.MouseButton1Click:Connect(function()
    isScriptMode = not isScriptMode
    if isScriptMode then
        ScriptToggle.TextColor3 = Color3.fromRGB(50, 200, 50)
        InputBox.PlaceholderText = "Cole seu script aqui..."
    else
        ScriptToggle.TextColor3 = Color3.fromRGB(200, 50, 50)
        InputBox.PlaceholderText = "Digite sua mensagem..."
    end
end)

local function AddChatMessage(senderName, userId, message, isScript, rawScriptContent)
    local MessageFrame = Instance.new("Frame")
    MessageFrame.Parent = ChatContainer
    MessageFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
    MessageFrame.BorderSizePixel = 0
    MessageFrame.Size = UDim2.new(1, -8, 0, isScript and 65 or 40)
    
    local FrameCorner = Instance.new("UICorner")
    FrameCorner.CornerRadius = UDim.new(0, 6)
    FrameCorner.Parent = MessageFrame

    local AvatarImg = Instance.new("ImageLabel")
    AvatarImg.Parent = MessageFrame
    AvatarImg.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
    AvatarImg.Position = UDim2.new(0, 6, 0, 6)
    AvatarImg.Size = UDim2.new(0, 28, 0, 28)
    AvatarImg.Image = "https://www.roblox.com/headshot-thumbnail/image?userId="..tostring(userId).."&width=420&height=420&format=png"
    
    local ImgCorner = Instance.new("UICorner")
    ImgCorner.CornerRadius = UDim.new(1, 0)
    ImgCorner.Parent = AvatarImg

    local NameLabel = Instance.new("TextLabel")
    NameLabel.Parent = MessageFrame
    NameLabel.BackgroundTransparency = 1
    NameLabel.Position = UDim2.new(0, 42, 0, 6)
    NameLabel.Size = UDim2.new(1, -48, 0, 14)
    NameLabel.Font = Enum.Font.GothamBold
    NameLabel.Text = senderName
    NameLabel.TextColor3 = Color3.fromRGB(150, 180, 255)
    NameLabel.TextSize = 11
    NameLabel.TextXAlignment = Enum.TextXAlignment.Left

    local ContentLabel = Instance.new("TextLabel")
    ContentLabel.Parent = MessageFrame
    ContentLabel.BackgroundTransparency = 1
    ContentLabel.Position = UDim2.new(0, 42, 0, 20)
    ContentLabel.Size = UDim2.new(1, -48, 0, isScript and 20 or 16)
    ContentLabel.Font = Enum.Font.Gotham
    ContentLabel.Text = message
    ContentLabel.TextColor3 = Color3.fromRGB(220, 220, 220)
    ContentLabel.TextSize = 11
    ContentLabel.TextXAlignment = Enum.TextXAlignment.Left
    ContentLabel.TextWrapped = true

    if isScript then
        local CopyButton = Instance.new("TextButton")
        CopyButton.Parent = MessageFrame
        CopyButton.BackgroundColor3 = Color3.fromRGB(45, 180, 80)
        CopyButton.Position = UDim2.new(0, 42, 0, 42)
        CopyButton.Size = UDim2.new(0, 100, 0, 18)
        CopyButton.Font = Enum.Font.GothamBold
        CopyButton.Text = "Copiar Script"
        CopyButton.TextColor3 = Color3.fromRGB(255, 255, 255)
        CopyButton.TextSize = 10
        
        local CopyCorner = Instance.new("UICorner")
        CopyCorner.CornerRadius = UDim.new(0, 4)
        CopyCorner.Parent = CopyButton

        CopyButton.MouseButton1Click:Connect(function()
            if setclipboard then
                setclipboard(rawScriptContent)
                CopyButton.Text = "Copiado!"
                task.wait(1.5)
                CopyButton.Text = "Copiar Script"
            end
        end)
    end

    ChatContainer.CanvasSize = UDim2.new(0, 0, 0, UIListLayout.AbsoluteContentSize.Y + 10)
    ChatContainer.CanvasPosition = Vector2.new(0, ChatContainer.CanvasSize.Y.Offset)
end

-- TENTATIVA DE USAR UM EVENTO DO JOGO OU CRIAR CANAL REPLICADO SE POSSÍVEL
local chatRemote = ReplicatedStorage:FindFirstChild("GlobalScriptChatEvent")

SendButton.MouseButton1Click:Connect(function()
    local text = InputBox.Text
    if text ~= "" then
        local scriptContent = text
        local displayMsg = text
        if isScriptMode then
            displayMsg = "[SCRIPT COMPARTILHADO]"
        end
        
        -- Mostra na própria tela
        AddChatMessage(LocalPlayer.Name, LocalPlayer.UserId, displayMsg, isScriptMode, scriptContent)
        
        -- Se houver um remote compartilhado, envia para os outros
        if chatRemote and chatRemote:IsA("RemoteEvent") then
            pcall(function()
                chatRemote:FireServer(displayMsg, isScriptMode, scriptContent)
            end)
        end
        
        InputBox.Text = ""
    end
end)

-- Ouve mensagens de outros jogadores caso o jogo tenha o Remote criado
if chatRemote and chatRemote:IsA("RemoteEvent") then
    chatRemote.OnClientEvent:Connect(function(player, displayMsg, isScript, scriptContent)
        if player ~= LocalPlayer then
            AddChatMessage(player.Name, player.UserId, displayMsg, isScript, scriptContent)
        end
    end)
end

AddChatMessage("SistemaGlobal", 1, "Painel unificado carregado com sucesso!", false, "")

-- SISTEMA DE ABRIR/FECHAR COM 5 TOQUES RÁPIDOS
local tapsCount = 0
local lastTapTime = 0
local uiVisible = true

UserInputService.InputBegan:Connect(function(input, gameProcessed)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        local currentTime = tick()
        if currentTime - lastTapTime < 0.4 then
            tapsCount = tapsCount + 1
        else
            tapsCount = 1
        end
        lastTapTime = currentTime
        
        if tapsCount >= 5 then
            uiVisible = not uiVisible
            MainFrame.Visible = uiVisible
            ChatFrame.Visible = uiVisible
            tapsCount = 0
        end
    end
end)
