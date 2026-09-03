local Players = game:GetService("Players")
local CoreGui = game:GetService("CoreGui")
local UserInputService = game:GetService("UserInputService")
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
            tapsCount = 0
        end
    end
end)
