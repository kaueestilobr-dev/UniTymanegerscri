-- SERVIÇOS
local TextChatService = game:GetService("TextChatService")
local CoreGui = game:GetService("CoreGui")
local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")

local player = Players.LocalPlayer

-- REMOVER ANTIGO
if CoreGui:FindFirstChild("UniTyHubV11") then CoreGui.UniTyHubV11:Destroy() end

local sg = Instance.new("ScreenGui")
sg.Name = "UniTyHubV11"
sg.Parent = CoreGui
sg.ResetOnSpawn = false

-- ==========================================
-- 1. TELA DE CARREGAMENTO (ESTILO BROOKHAVEN)
-- ==========================================
local loadFrame = Instance.new("Frame")
loadFrame.Size = UDim2.new(1, 0, 1, 0)
loadFrame.BackgroundColor3 = Color3.fromRGB(5, 5, 5)
loadFrame.ZIndex = 10
loadFrame.Parent = sg

local loadTitle = Instance.new("TextLabel")
loadTitle.Size = UDim2.new(1, 0, 0, 50)
loadTitle.Position = UDim2.new(0, 0, 0.4, 0)
loadTitle.Text = "UniTy Sistemas"
loadTitle.TextColor3 = Color3.fromRGB(0, 255, 255)
loadTitle.Font = Enum.Font.GothamBold
loadTitle.TextSize = 30
loadTitle.BackgroundTransparency = 1
loadTitle.ZIndex = 11
loadTitle.Parent = loadFrame

local loadCredit = Instance.new("TextLabel")
loadCredit.Size = UDim2.new(1, 0, 0, 30)
loadCredit.Position = UDim2.new(0, 0, 0.4, 40)
loadCredit.Text = "Desenvolvido por yDaLLaSs"
loadCredit.TextColor3 = Color3.fromRGB(255, 255, 255)
loadCredit.Font = Enum.Font.Gotham -- Letra normal
loadCredit.TextSize = 16
loadCredit.BackgroundTransparency = 1
loadCredit.ZIndex = 11
loadCredit.Parent = loadFrame

local barBg = Instance.new("Frame")
barBg.Size = UDim2.new(0, 300, 0, 4)
barBg.Position = UDim2.new(0.5, -150, 0.6, 0)
barBg.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
barBg.BorderSizePixel = 0
barBg.ZIndex = 11
barBg.Parent = loadFrame

local barFill = Instance.new("Frame")
barFill.Size = UDim2.new(0, 0, 1, 0)
barFill.BackgroundColor3 = Color3.fromRGB(0, 255, 255)
barFill.BorderSizePixel = 0
barFill.ZIndex = 12
barFill.Parent = barBg

task.spawn(function()
    barFill:TweenSize(UDim2.new(1, 0, 1, 0), "Out", "Linear", 2)
    task.wait(2.2)
    loadFrame:TweenPosition(UDim2.new(0, 0, -1, 0), "InOut", "Quart", 0.5)
    task.wait(0.6)
    loadFrame:Destroy()
end)

-- ==========================================
-- 2. PAINEL PRINCIPAL & BOLHA
-- ==========================================
local main = Instance.new("Frame")
main.Size = UDim2.new(0, 520, 0, 350)
main.Position = UDim2.new(0.5, -260, 0.5, -175)
main.BackgroundColor3 = Color3.fromRGB(10, 10, 12)
main.Active = true
main.Draggable = true
main.Parent = sg

Instance.new("UICorner", main)
local mStroke = Instance.new("UIStroke", main)
mStroke.Color = Color3.fromRGB(0, 255, 255)

local bubble = Instance.new("ImageButton")
bubble.Size = UDim2.new(0, 55, 0, 55)
bubble.Position = UDim2.new(0, 15, 0.5, 0)
bubble.BackgroundColor3 = Color3.fromRGB(15, 15, 20)
bubble.Image = "rbxthumb://type=AvatarHeadShot&id="..player.UserId.."&w=150&h=150"
bubble.Visible = false
bubble.Draggable = true
bubble.Parent = sg
Instance.new("UICorner", bubble).CornerRadius = UDim.new(1, 0)
Instance.new("UIStroke", bubble).Color = Color3.fromRGB(0, 255, 255)

-- ==========================================
-- 3. SIDEBAR (CONTEÚDO E PERFIL)
-- ==========================================
local sidebar = Instance.new("Frame")
sidebar.Size = UDim2.new(0, 160, 1, 0)
sidebar.BackgroundColor3 = Color3.fromRGB(15, 15, 18)
sidebar.Parent = main
Instance.new("UICorner", sidebar)

local hubT = Instance.new("TextLabel")
hubT.Size = UDim2.new(1, 0, 0, 40)
hubT.Text = "UniTy Sistemas"
hubT.TextColor3 = Color3.fromRGB(0, 255, 255)
hubT.Font = Enum.Font.GothamBold
hubT.TextSize = 16
hubT.BackgroundTransparency = 1
hubT.Parent = sidebar

local devT = Instance.new("TextLabel")
devT.Size = UDim2.new(1, 0, 0, 20)
devT.Position = UDim2.new(0, 0, 0, 35)
devT.Text = "Dev: yDaLLaSs"
devT.TextColor3 = Color3.fromRGB(200, 200, 200)
devT.Font = Enum.Font.Gotham -- Fonte normal
devT.TextSize = 12
devT.BackgroundTransparency = 1
devT.Parent = sidebar

local statusT = Instance.new("TextLabel")
statusT.Size = UDim2.new(1, 0, 0, 20)
statusT.Position = UDim2.new(0, 0, 0, 55)
statusT.Text = "UniTy Group: Em Dev"
statusT.TextColor3 = Color3.fromRGB(255, 170, 0)
statusT.Font = Enum.Font.GothamBold
statusT.TextSize = 10
statusT.BackgroundTransparency = 1
statusT.Parent = sidebar

-- Área de botões da barra lateral
local btnArea = Instance.new("Frame")
btnArea.Size = UDim2.new(1, 0, 1, -150)
btnArea.Position = UDim2.new(0, 0, 0, 85)
btnArea.BackgroundTransparency = 1
btnArea.Parent = sidebar
local layout = Instance.new("UIListLayout", btnArea)
layout.Padding = UDim.new(0, 5)
layout.HorizontalAlignment = Enum.HorizontalAlignment.Center

local function addTab(txt, color, func)
    local b = Instance.new("TextButton")
    b.Size = UDim2.new(0.9, 0, 0, 35)
    b.BackgroundColor3 = Color3.fromRGB(25, 25, 30)
    b.Text = txt
    b.TextColor3 = color
    b.Font = Enum.Font.Gotham -- Texto normal e limpo
    b.TextSize = 13
    b.Parent = btnArea
    Instance.new("UICorner", b)
    b.MouseButton1Click:Connect(func)
end

addTab("Mensagens", Color3.new(1,1,1), function() end)

addTab("Minimizar Bolha", Color3.fromRGB(0, 255, 150), function()
    main.Visible = false
    bubble.Visible = true
end)

addTab("Fechar Script", Color3.fromRGB(255, 50, 50), function()
    sg:Destroy()
end)

bubble.MouseButton1Click:Connect(function()
    main.Visible = true
    bubble.Visible = false
end)

-- Perfil no rodapé da lateral
local profileFrame = Instance.new("Frame")
profileFrame.Size = UDim2.new(1, 0, 0, 50)
profileFrame.Position = UDim2.new(0, 0, 1, -50)
profileFrame.BackgroundTransparency = 1
profileFrame.Parent = sidebar

local pIcon = Instance.new("ImageLabel")
pIcon.Size = UDim2.new(0, 35, 0, 35)
pIcon.Position = UDim2.new(0, 10, 0.5, -17)
pIcon.Image = "rbxthumb://type=AvatarHeadShot&id="..player.UserId.."&w=150&h=150"
pIcon.Parent = profileFrame
Instance.new("UICorner", pIcon).CornerRadius = UDim.new(1, 0)

local pName = Instance.new("TextLabel")
pName.Size = UDim2.new(1, -55, 1, 0)
pName.Position = UDim2.new(0, 50, 0, 0)
pName.Text = player.DisplayName
pName.TextColor3 = Color3.fromRGB(255, 255, 255)
pName.Font = Enum.Font.GothamSemibold
pName.TextSize = 12
pName.TextXAlignment = Enum.TextXAlignment.Left
pName.BackgroundTransparency = 1
pName.Parent = profileFrame

-- ==========================================
-- 4. CONTEÚDO (CRIAÇÃO DE BOTÕES)
-- ==========================================
local content = Instance.new("Frame")
content.Size = UDim2.new(1, -170, 1, -20)
content.Position = UDim2.new(0, 165, 0, 10)
content.BackgroundTransparency = 1
content.Parent = main

local inNome = Instance.new("TextBox")
inNome.Size = UDim2.new(1, 0, 0, 40)
inNome.PlaceholderText = "Nome do Botão (Ex: RENDER)"
inNome.BackgroundColor3 = Color3.fromRGB(30, 30, 35)
inNome.TextColor3 = Color3.new(1,1,1)
inNome.Font = Enum.Font.Gotham -- Fonte limpa
inNome.Parent = content
Instance.new("UICorner", inNome)

local inMsg = Instance.new("TextBox")
inMsg.Size = UDim2.new(1, 0, 0, 80)
inMsg.Position = UDim2.new(0, 0, 0, 50)
inMsg.PlaceholderText = "Texto da frase para o Chat..."
inMsg.TextWrapped = true
inMsg.BackgroundColor3 = Color3.fromRGB(30, 30, 35)
inMsg.TextColor3 = Color3.new(1,1,1)
inMsg.Font = Enum.Font.Gotham
inMsg.Parent = content
Instance.new("UICorner", inMsg)

local btnCreate = Instance.new("TextButton")
btnCreate.Size = UDim2.new(1, 0, 0, 45)
btnCreate.Position = UDim2.new(0, 0, 0, 140)
btnCreate.Text = "GERAR BOTÃO"
btnCreate.BackgroundColor3 = Color3.fromRGB(0, 100, 255)
btnCreate.TextColor3 = Color3.new(1,1,1)
btnCreate.Font = Enum.Font.GothamBold
btnCreate.Parent = content
Instance.new("UICorner", btnCreate)

-- Função para criar botões de PvP na tela
btnCreate.MouseButton1Click:Connect(function()
    if inNome.Text ~= "" and inMsg.Text ~= "" then
        local p = Instance.new("TextButton")
        p.Size = UDim2.new(0, 130, 0, 45)
        p.Position = UDim2.new(0.5, 0, 0.5, 0)
        p.Text = inNome.Text
        p.BackgroundColor3 = Color3.fromRGB(15, 15, 20)
        p.TextColor3 = Color3.new(1,1,1)
        p.Font = Enum.Font.GothamBold -- Letra normal sem efeitos estranhos
        p.Draggable = true
        p.Parent = sg
        Instance.new("UICorner", p)
        Instance.new("UIStroke", p).Color = Color3.fromRGB(0, 255, 255)

        local del = Instance.new("TextButton")
        del.Size = UDim2.new(0, 20, 0, 20)
        del.Position = UDim2.new(1, -10, 0, -10)
        del.Text = "X"
        del.BackgroundColor3 = Color3.fromRGB(200, 0, 0)
        del.TextColor3 = Color3.new(1,1,1)
        del.Font = Enum.Font.GothamBold
        del.Parent = p
        Instance.new("UICorner", del).CornerRadius = UDim.new(1, 0)

        p.MouseButton1Click:Connect(function()
            if TextChatService.ChatVersion == Enum.ChatVersion.TextChatService then
                TextChatService.TextChannels.RBXGeneral:SendAsync(inMsg.Text)
            else
                game:GetService("ReplicatedStorage").DefaultChatSystemChatEvents.SayMessageRequest:FireServer(inMsg.Text, "All")
            end
        end)
        del.MouseButton1Click:Connect(function() p:Destroy() end)
    end
end)
