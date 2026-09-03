local CoreGui = game:GetService("CoreGui")
local TweenService = game:GetService("TweenService")
local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local SoundService = game:GetService("SoundService")
local LocalPlayer = Players.LocalPlayer

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Parent = CoreGui
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
ScreenGui.Name = "AuraSystemAudioGui"

-- TELA DE CARREGAMENTO INICIAL
local LoadBg = Instance.new("Frame")
LoadBg.Name = "LoadBg"
LoadBg.Parent = ScreenGui
LoadBg.BackgroundColor3 = Color3.fromRGB(13, 13, 16)
LoadBg.Size = UDim2.new(1, 0, 1, 0)
LoadBg.ZIndex = 9999

local LoadLogoText = Instance.new("TextLabel")
LoadLogoText.Name = "LoadLogoText"
LoadLogoText.Parent = LoadBg
LoadLogoText.BackgroundTransparency = 1
LoadLogoText.AnchorPoint = Vector2.new(0.5, 0.5)
LoadLogoText.Position = UDim2.new(0.5, 0, 0.5, 0)
LoadLogoText.Size = UDim2.new(0, 400, 0, 80)
LoadLogoText.Font = Enum.Font.GothamBold
LoadLogoText.Text = "GGMENU V2"
LoadLogoText.TextColor3 = Color3.fromRGB(220, 220, 230)
LoadLogoText.TextSize = 36
LoadLogoText.TextXAlignment = Enum.TextXAlignment.Center
LoadLogoText.TextYAlignment = Enum.TextYAlignment.Center
LoadLogoText.ZIndex = 10000

local LoadStroke = Instance.new("UIStroke")
LoadStroke.Color = Color3.fromRGB(45, 45, 55)
LoadStroke.Thickness = 1
LoadStroke.Parent = LoadLogoText

-- MÚSICA DO PAINEL
local BgMusic = Instance.new("Sound")
BgMusic.Name = "PanelMusic"
BgMusic.Parent = SoundService
BgMusic.SoundId = "rbxassetid://138968496511779"
BgMusic.Volume = 1.5
BgMusic:Play()

task.spawn(function()
    task.wait(10)
    if BgMusic and BgMusic.IsPlaying then
        local tw = TweenService:Create(BgMusic, TweenInfo.new(2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {Volume = 0})
        tw:Play()
        tw.Completed:Connect(function()
            BgMusic:Stop()
        end)
    end
end)

-- PAINEL PRINCIPAL
local MainFrame = Instance.new("Frame")
local MainCorner = Instance.new("UICorner")
local MainStroke = Instance.new("UIStroke")
local TopBar = Instance.new("Frame")
local TopBarCorner = Instance.new("UICorner")
local Title = Instance.new("TextLabel")

MainFrame.Name = "MainFrame"
MainFrame.Parent = ScreenGui
MainFrame.BackgroundColor3 = Color3.fromRGB(13, 13, 16)
MainFrame.AnchorPoint = Vector2.new(0.5, 0.5)
MainFrame.Position = UDim2.new(0.5, 0, 0.5, 0)
MainFrame.Size = UDim2.new(0, 280, 0, 190)
MainFrame.Active = true
MainFrame.Draggable = true
MainFrame.Visible = false
MainFrame.BackgroundTransparency = 1
MainFrame.ZIndex = 1

MainCorner.CornerRadius = UDim.new(0, 12)
MainCorner.Parent = MainFrame

MainStroke.Color = Color3.fromRGB(45, 45, 55)
MainStroke.Thickness = 1.5
MainStroke.Transparency = 1
MainStroke.Parent = MainFrame

TopBar.Name = "TopBar"
TopBar.Parent = MainFrame
TopBar.BackgroundColor3 = Color3.fromRGB(18, 18, 22)
TopBar.BackgroundTransparency = 1
TopBar.Size = UDim2.new(1, 0, 0, 38)

TopBarCorner.CornerRadius = UDim.new(0, 12)
TopBarCorner.Parent = TopBar

local TopBarCover = Instance.new("Frame")
TopBarCover.Parent = TopBar
TopBarCover.BackgroundColor3 = Color3.fromRGB(18, 18, 22)
TopBarCover.BackgroundTransparency = 1
TopBarCover.BorderSizePixel = 0
TopBarCover.Position = UDim2.new(0, 0, 0.7, 0)
TopBarCover.Size = UDim2.new(1, 0, 0.3, 0)

local AvatarIcon = Instance.new("ImageLabel")
AvatarIcon.Name = "AvatarIcon"
AvatarIcon.Parent = TopBar
AvatarIcon.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
AvatarIcon.BackgroundTransparency = 1
AvatarIcon.Position = UDim2.new(0, 8, 0, 4)
AvatarIcon.Size = UDim2.new(0, 30, 0, 30)
AvatarIcon.Image = "rbxassetid://0"
AvatarIcon.ImageTransparency = 1

task.spawn(function()
    pcall(function()
        local content = Players:GetUserThumbnailAsync(LocalPlayer.UserId, Enum.ThumbnailType.HeadShot, Enum.ThumbnailSize.Size420x420)
        AvatarIcon.Image = content
    end)
end)

local AvatarCorner = Instance.new("UICorner")
AvatarCorner.CornerRadius = UDim.new(1, 0)
AvatarCorner.Parent = AvatarIcon

Title.Name = "Title"
Title.Parent = TopBar
Title.BackgroundTransparency = 1.00
Title.Position = UDim2.new(0, 45, 0, 0)
Title.Size = UDim2.new(1, -55, 1, 0)
Title.Font = Enum.Font.GothamBold
Title.Text = "GGMENU V2 — AURA"
Title.TextColor3 = Color3.fromRGB(220, 220, 230)
Title.TextSize = 13.00
Title.TextTransparency = 1
Title.TextXAlignment = Enum.TextXAlignment.Left

local ContentContainer = Instance.new("Frame")
ContentContainer.Parent = MainFrame
ContentContainer.BackgroundTransparency = 1
ContentContainer.Position = UDim2.new(0, 0, 0, 38)
ContentContainer.Size = UDim2.new(1, 0, 1, -38)

local FarmAuraToggle = Instance.new("TextButton")
FarmAuraToggle.Name = "FarmAuraToggle"
FarmAuraToggle.Parent = ContentContainer
FarmAuraToggle.BackgroundColor3 = Color3.fromRGB(22, 22, 28)
FarmAuraToggle.BackgroundTransparency = 1
FarmAuraToggle.Position = UDim2.new(0, 15, 0, 20)
FarmAuraToggle.Size = UDim2.new(0, 250, 0, 50)
FarmAuraToggle.Font = Enum.Font.GothamMedium
FarmAuraToggle.Text = "  Farm Aura: OFF"
FarmAuraToggle.TextColor3 = Color3.fromRGB(180, 70, 70)
FarmAuraToggle.TextTransparency = 1
FarmAuraToggle.TextSize = 14.00
FarmAuraToggle.TextXAlignment = Enum.TextXAlignment.Left

local FarmAuraCorner = Instance.new("UICorner")
FarmAuraCorner.CornerRadius = UDim.new(0, 8)
FarmAuraCorner.Parent = FarmAuraToggle

local FarmAuraStroke = Instance.new("UIStroke")
FarmAuraStroke.Color = Color3.fromRGB(35, 35, 45)
FarmAuraStroke.Thickness = 1
FarmAuraStroke.Transparency = 1
FarmAuraStroke.Parent = FarmAuraToggle

local StatusDot = Instance.new("Frame")
StatusDot.Name = "StatusDot"
StatusDot.Parent = FarmAuraToggle
StatusDot.AnchorPoint = Vector2.new(1, 0.5)
StatusDot.BackgroundColor3 = Color3.fromRGB(180, 70, 70)
StatusDot.BackgroundTransparency = 1
StatusDot.Position = UDim2.new(1, -15, 0.5, 0)
StatusDot.Size = UDim2.new(0, 10, 0, 10)

local DotCorner = Instance.new("UICorner")
DotCorner.CornerRadius = UDim.new(1, 0)
DotCorner.Parent = StatusDot

local farmAuraRunning = false

local function setFarmState(state)
    farmAuraRunning = state
    if farmAuraRunning then
        FarmAuraToggle.Text = "  Farm Aura: ON"
        FarmAuraToggle.TextColor3 = Color3.fromRGB(70, 200, 100)
        StatusDot.BackgroundColor3 = Color3.fromRGB(70, 200, 100)
        TweenService:Create(FarmAuraToggle, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(20, 32, 24)}):Play()
    else
        FarmAuraToggle.Text = "  Farm Aura: OFF"
        FarmAuraToggle.TextColor3 = Color3.fromRGB(180, 70, 70)
        StatusDot.BackgroundColor3 = Color3.fromRGB(180, 70, 70)
        TweenService:Create(FarmAuraToggle, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(22, 22, 28)}):Play()
    end
end

FarmAuraToggle.MouseButton1Click:Connect(function()
    setFarmState(not farmAuraRunning)
end)

-- LOOP DO FARM
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

local FooterText = Instance.new("TextLabel")
FooterText.Parent = ContentContainer
FooterText.BackgroundTransparency = 1
FooterText.Position = UDim2.new(0, 15, 1, -25)
FooterText.Size = UDim2.new(1, -30, 0, 15)
FooterText.Font = Enum.Font.Gotham
FooterText.Text = "Pressione 5x na tela para alternar o menu"
FooterText.TextColor3 = Color3.fromRGB(90, 90, 110)
FooterText.TextTransparency = 1
FooterText.TextSize = 10.00
FooterText.TextXAlignment = Enum.TextXAlignment.Center

-- ANIMAÇÃO DE ENTRADA DO PAINEL
task.spawn(function()
    task.wait(2.5)
    
    local loadFadeOut = TweenService:Create(LoadBg, TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {BackgroundTransparency = 1})
    local loadTextFadeOut = TweenService:Create(LoadLogoText, TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {TextTransparency = 1})
    local loadStrokeFadeOut = TweenService:Create(LoadStroke, TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {Transparency = 1})
    
    loadFadeOut:Play()
    loadTextFadeOut:Play()
    loadStrokeFadeOut:Play()
    
    MainFrame.Visible = true
    local info = TweenInfo.new(0.5, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    
    TweenService:Create(MainFrame, info, {BackgroundTransparency = 0}):Play()
    TweenService:Create(MainStroke, info, {Transparency = 0}):Play()
    TweenService:Create(TopBar, info, {BackgroundTransparency = 0}):Play()
    TweenService:Create(TopBarCover, info, {BackgroundTransparency = 0}):Play()
    TweenService:Create(AvatarIcon, info, {ImageTransparency = 0}):Play()
    TweenService:Create(Title, info, {TextTransparency = 0}):Play()
    TweenService:Create(FarmAuraToggle, info, {BackgroundTransparency = 0, TextTransparency = 0}):Play()
    TweenService:Create(FarmAuraStroke, info, {Transparency = 0}):Play()
    TweenService:Create(StatusDot, info, {BackgroundTransparency = 0}):Play()
    TweenService:Create(FooterText, info, {TextTransparency = 0}):Play()
    
    loadFadeOut.Completed:Connect(function()
        LoadBg:Destroy()
    end)
end)

-- SISTEMA DE ABRIR/FECHAR O PAINEL COM 5 TOQUES RÁPIDOS
local tapsCount = 0
local lastTapTime = 0
local uiVisible = false

task.spawn(function()
    task.wait(3.0)
    uiVisible = true
end)

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
            local info = TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
            
            if uiVisible then
                MainFrame.Visible = true
                TweenService:Create(MainFrame, info, {BackgroundTransparency = 0}):Play()
                TweenService:Create(MainStroke, info, {Transparency = 0}):Play()
                TweenService:Create(TopBar, info, {BackgroundTransparency = 0}):Play()
                TweenService:Create(TopBarCover, info, {BackgroundTransparency = 0}):Play()
                TweenService:Create(AvatarIcon, info, {ImageTransparency = 0}):Play()
                TweenService:Create(Title, info, {TextTransparency = 0}):Play()
                TweenService:Create(FarmAuraToggle, info, {BackgroundTransparency = 0, TextTransparency = 0}):Play()
                TweenService:Create(FarmAuraStroke, info, {Transparency = 0}):Play()
                TweenService:Create(StatusDot, info, {BackgroundTransparency = 0}):Play()
                TweenService:Create(FooterText, info, {TextTransparency = 0}):Play()
            else
                local fadeOutInfo = TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.In)
                TweenService:Create(MainFrame, fadeOutInfo, {BackgroundTransparency = 1}):Play()
                TweenService:Create(MainStroke, fadeOutInfo, {Transparency = 1}):Play()
                TweenService:Create(TopBar, fadeOutInfo, {BackgroundTransparency = 1}):Play()
                TweenService:Create(TopBarCover, fadeOutInfo, {BackgroundTransparency = 1}):Play()
                TweenService:Create(AvatarIcon, fadeOutInfo, {ImageTransparency = 1}):Play()
                TweenService:Create(Title, fadeOutInfo, {TextTransparency = 1}):Play()
                TweenService:Create(FarmAuraToggle, fadeOutInfo, {BackgroundTransparency = 1, TextTransparency = 1}):Play()
                TweenService:Create(FarmAuraStroke, fadeOutInfo, {Transparency = 1}):Play()
                TweenService:Create(StatusDot, fadeOutInfo, {BackgroundTransparency = 1}):Play()
                
                local hideTw = TweenService:Create(FooterText, fadeOutInfo, {TextTransparency = 1})
                hideTw:Play()
                hideTw.Completed:Connect(function()
                    if not uiVisible then
                        MainFrame.Visible = false
                    end
                end)
            end
            tapsCount = 0
        end
    end
end)
