--// BLOX HUB COMPLETA
-- Feito por IA – Painel estiloso com círculo, key e tela de carregamento

--== CONFIG ==--
local KEY_CORRETA = "test1"

--== BASE ==--
local player = game.Players.LocalPlayer
local gui = Instance.new("ScreenGui")
gui.Name = "BloxHubGui"
gui.ResetOnSpawn = false
gui.IgnoreGuiInset = true
gui.Parent = player:WaitForChild("PlayerGui")

local TweenService = game:GetService("TweenService")
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UIS = game:GetService("UserInputService")
local LocalPlayer = player

--== FUNÇÕES ÚTEIS ==--
local function addCorner(obj, radius)
    local c = Instance.new("UICorner")
    c.CornerRadius = UDim.new(0, radius or 8)
    c.Parent = obj
end

local function makeDraggable(frame)
    local dragging, dragStart, startPos
    frame.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 then
            dragging = true
            dragStart = input.Position
            startPos = frame.Position
            input.Changed:Connect(function()
                if input.UserInputState == Enum.UserInputState.End then
                    dragging = false
                end
            end)
        end
    end)
    UIS.InputChanged:Connect(function(input)
        if dragging and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
            local delta = input.Position - dragStart
            frame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X,
                startPos.Y.Scale, startPos.Y.Offset + delta.Y)
        end
    end)
end

--== CÍRCULO INICIAL ==--
local circleButton = Instance.new("ImageButton")
circleButton.Size = UDim2.new(0, 80, 0, 80)
circleButton.Position = UDim2.new(0.05, 0, 0.8, 0)
circleButton.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
circleButton.BorderColor3 = Color3.fromRGB(100, 100, 100)
circleButton.AutoButtonColor = true
circleButton.Image = ""
circleButton.Parent = gui
addCorner(circleButton, 40)
makeDraggable(circleButton)

local circleLabel = Instance.new("TextLabel")
circleLabel.Size = UDim2.new(1, 0, 1, 0)
circleLabel.BackgroundTransparency = 1
circleLabel.Text = "⚙️"
circleLabel.TextScaled = true
circleLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
circleLabel.Font = Enum.Font.GothamBold
circleLabel.Active = false
circleLabel.Selectable = false
circleLabel.Parent = circleButton

--== TELA DE KEY ==--
local keyFrame = Instance.new("Frame")
keyFrame.Size = UDim2.new(0, 300, 0, 150)
keyFrame.Position = UDim2.new(0.5, -150, 0.45, -75)
keyFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
keyFrame.BorderColor3 = Color3.fromRGB(80, 80, 80)
keyFrame.Visible = false
keyFrame.Parent = gui
addCorner(keyFrame, 10)
makeDraggable(keyFrame)

local titleKey = Instance.new("TextLabel")
titleKey.Text = "DIGITE SUA KEY"
titleKey.Size = UDim2.new(1, 0, 0, 30)
titleKey.BackgroundTransparency = 1
titleKey.TextColor3 = Color3.fromRGB(200, 200, 200)
titleKey.Font = Enum.Font.GothamBold
titleKey.TextSize = 16
titleKey.Parent = keyFrame

local textBox = Instance.new("TextBox")
textBox.PlaceholderText = "Digite sua key..."
textBox.Size = UDim2.new(0.9, 0, 0, 35)
textBox.Position = UDim2.new(0.05, 0, 0.35, 0)
textBox.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
textBox.TextColor3 = Color3.fromRGB(255, 255, 255)
textBox.BorderColor3 = Color3.fromRGB(70, 70, 70)
textBox.Font = Enum.Font.Gotham
textBox.TextSize = 14
textBox.Parent = keyFrame
addCorner(textBox, 8)

local confirmButton = Instance.new("TextButton")
confirmButton.Text = "Confirmar"
confirmButton.Size = UDim2.new(0.9, 0, 0, 35)
confirmButton.Position = UDim2.new(0.05, 0, 0.7, 0)
confirmButton.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
confirmButton.TextColor3 = Color3.fromRGB(255, 255, 255)
confirmButton.Font = Enum.Font.GothamBold
confirmButton.TextSize = 14
confirmButton.BorderColor3 = Color3.fromRGB(80, 80, 80)
confirmButton.Parent = keyFrame
addCorner(confirmButton, 8)

--== TELA DE CARREGAMENTO ==--
local loadingFrame = Instance.new("Frame")
loadingFrame.Size = UDim2.new(0, 300, 0, 100)
loadingFrame.Position = UDim2.new(0.5, -150, 0.45, -50)
loadingFrame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
loadingFrame.BorderColor3 = Color3.fromRGB(90, 90, 90)
loadingFrame.Visible = false
loadingFrame.Parent = gui
addCorner(loadingFrame, 10)

local loadingText = Instance.new("TextLabel")
loadingText.Size = UDim2.new(1, 0, 1, 0)
loadingText.BackgroundTransparency = 1
loadingText.TextColor3 = Color3.fromRGB(255, 255, 255)
loadingText.Font = Enum.Font.GothamBold
loadingText.TextScaled = true
loadingText.Text = "CARREGANDO..."
loadingText.Parent = loadingFrame

--== PAINEL BLOX HUB ==--
local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 500, 0, 400)
mainFrame.Position = UDim2.new(0.5, -250, 0.4, -200)
mainFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
mainFrame.BorderColor3 = Color3.fromRGB(90, 90, 90)
mainFrame.Visible = false
mainFrame.Parent = gui
addCorner(mainFrame, 10)
makeDraggable(mainFrame)

local title = Instance.new("TextLabel")
title.Text = "BLOX HUB"
title.Size = UDim2.new(1, 0, 0, 25)
title.BackgroundTransparency = 1
title.TextColor3 = Color3.fromRGB(200, 200, 200)
title.Font = Enum.Font.GothamBold
title.TextSize = 16
title.Parent = mainFrame

--== MENU ESQUERDO ==--
local leftMenu = Instance.new("ScrollingFrame")
leftMenu.Size = UDim2.new(0, 120, 1, -25)
leftMenu.Position = UDim2.new(0, 0, 0, 25)
leftMenu.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
leftMenu.BorderColor3 = Color3.fromRGB(80, 80, 80)
leftMenu.CanvasSize = UDim2.new(0, 0, 0, 300)
leftMenu.ScrollBarThickness = 5
leftMenu.Parent = mainFrame
addCorner(leftMenu, 8)

--== ÁREA DIREITA ==--
local rightArea = Instance.new("ScrollingFrame")
rightArea.Size = UDim2.new(1, -130, 1, -25)
rightArea.Position = UDim2.new(0, 130, 0, 25)
rightArea.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
rightArea.BorderColor3 = Color3.fromRGB(90, 90, 90)
rightArea.CanvasSize = UDim2.new(0, 0, 0, 600)
rightArea.ScrollBarThickness = 6
rightArea.Parent = mainFrame
addCorner(rightArea, 8)

--== BOTÕES DE MENU ==--
local categorias = {"Player", "Visual", "Menu"}
for i, nome in ipairs(categorias) do
    local botao = Instance.new("TextButton")
    botao.Text = nome
    botao.Size = UDim2.new(0.9, 0, 0, 35)
    botao.Position = UDim2.new(0.05, 0, 0, (i - 1) * 40)
    botao.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
    botao.TextColor3 = Color3.fromRGB(255, 255, 255)
    botao.Font = Enum.Font.GothamBold
    botao.TextSize = 14
    botao.BorderColor3 = Color3.fromRGB(70, 70, 70)
    botao.Parent = leftMenu
    addCorner(botao, 8)

    botao.MouseButton1Click:Connect(function()
        print("Categoria selecionada: " .. nome)
    end)
end

--== FUNÇÕES PLAYER (ESP, SPEED, JUMP) ==--
local espEnabled = false
local espBoxes = {}
local defaultWalkSpeed = LocalPlayer.Character and LocalPlayer.Character:FindFirstChildOfClass("Humanoid").WalkSpeed or 16
local defaultJumpPower = LocalPlayer.Character and LocalPlayer.Character:FindFirstChildOfClass("Humanoid").JumpPower or 50
local walkSpeedValue = 50
local jumpPowerValue = 100

local function createESP()
    for _, plr in pairs(Players:GetPlayers()) do
        if plr ~= LocalPlayer and plr.Character and not espBoxes[plr] then
            local box = Instance.new("BoxHandleAdornment")
            box.Adornee = plr.Character:FindFirstChild("HumanoidRootPart")
            box.Size = Vector3.new(2,5,1)
            box.Color3 = Color3.fromRGB(0,255,0)
            box.Transparency = 0.5
            box.AlwaysOnTop = true
            box.ZIndex = 10
            box.Parent = workspace
            espBoxes[plr] = box
        end
    end
end

local function removeESP()
    for _, box in pairs(espBoxes) do
        box:Destroy()
    end
    espBoxes = {}
end

Players.PlayerAdded:Connect(function(plr)
    plr.CharacterAdded:Connect(function()
        if espEnabled then
            createESP()
        end
    end)
end)

local function setSpeed(speed)
    if LocalPlayer.Character and LocalPlayer.Character:FindFirstChildOfClass("Humanoid") then
        LocalPlayer.Character:FindFirstChildOfClass("Humanoid").WalkSpeed = speed
    end
end

local function setJump(jump)
    if LocalPlayer.Character and LocalPlayer.Character:FindFirstChildOfClass("Humanoid") then
        LocalPlayer.Character:FindFirstChildOfClass("Humanoid").JumpPower = jump
    end
end

local function resetSpeed() setSpeed(defaultWalkSpeed) end
local function resetJump() setJump(defaultJumpPower) end

--== BOTÕES PLAYER ==--
local function createButton(text,posY,func)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(0.9,0,0,30)
    btn.Position = UDim2.new(0.05,0,posY,0)
    btn.Text = text
    btn.BackgroundColor3 = Color3.fromRGB(40,40,40)
    btn.TextColor3 = Color3.fromRGB(255,255,255)
    btn.Font = Enum.Font.GothamBold
    btn.TextSize = 14
    btn.Parent = rightArea
    addCorner(btn,6)
    btn.MouseButton1Click:Connect(func)
    return btn
end

-- ESP
createButton("Ativar/Desativar ESP",0,function()
    espEnabled = not espEnabled
    if espEnabled then createESP() else removeESP() end
end)

-- Velocidade
local speedBox = Instance.new("TextBox")
speedBox.Size = UDim2.new(0.4,0,0,30)
speedBox.Position = UDim2.new(0.05,0,0.05,0)
speedBox.PlaceholderText = "WalkSpeed"
speedBox.Text = tostring(walkSpeedValue)
speedBox.BackgroundColor3 = Color3.fromRGB(30,30,30)
speedBox.TextColor3 = Color3.fromRGB(255,255,255)
speedBox.BorderColor3 = Color3.fromRGB(70,70,70)
speedBox.Font = Enum.Font.Gotham
speedBox.TextSize = 14
speedBox.Parent = rightArea
addCorner(speedBox,6)

createButton("Ativar Velocidade",0.1,function()
    walkSpeedValue = tonumber(speedBox.Text) or walkSpeedValue
    setSpeed(walkSpeedValue)
end)

createButton("Desativar Velocidade",0.15,resetSpeed)

-- Pulo
local jumpBox = Instance.new("TextBox")
jumpBox.Size = UDim2.new(0.4,0,0,30)
jumpBox.Position = UDim2.new(0.05,0,0.25,0)
jumpBox.PlaceholderText = "JumpPower"
jumpBox.Text = tostring(jumpPowerValue)
jumpBox.BackgroundColor3 = Color3.fromRGB(30,30,30)
jumpBox.TextColor3 = Color3.fromRGB(255,255,255)
jumpBox.BorderColor3 = Color3.fromRGB(70,70,70)
jumpBox.Font = Enum.Font.Gotham
jumpBox.TextSize = 14
jumpBox.Parent = rightArea
addCorner(jumpBox,6)

createButton("Ativar Pulo",0.3,function()
    jumpPowerValue = tonumber(jumpBox.Text) or jumpPowerValue
    setJump(jumpPowerValue)
end)

createButton("Desativar Pulo",0.35,resetJump)

--== FUNCIONALIDADE PRINCIPAL ==--
circleButton.MouseButton1Click:Connect(function()
    circleButton.Visible = false
    keyFrame.Visible = true
    keyFrame.BackgroundTransparency = 1
    TweenService:Create(keyFrame,TweenInfo.new(0.4),{BackgroundTransparency=0}):Play()
end)

confirmButton.MouseButton1Click:Connect(function()
    local key = textBox.Text
    if key == KEY_CORRETA then
        keyFrame.Visible = false
        loadingFrame.Visible = true
        loadingText.Text = "CARREGANDO..."
        task.wait(0.6)
        loadingText.Text = "INICIALIZANDO..."
        task.wait(0.6)
        loadingText.Text = "ABRINDO PAINEL..."
        task.wait(0.6)
        TweenService:Create(loadingFrame,TweenInfo.new(0.4),{BackgroundTransparency=1}):Play()
        task.wait(0.4)
        loadingFrame.Visible = false
        mainFrame.Visible = true
        mainFrame.BackgroundTransparency = 1
        TweenService:Create(mainFrame,TweenInfo.new(0.5),{BackgroundTransparency=0}):Play()
    else
        textBox.Text = ""
        textBox.PlaceholderText = "Key incorreta!"
    end
end)