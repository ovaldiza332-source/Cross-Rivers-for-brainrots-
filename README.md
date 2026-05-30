-- SERVIÇOS
local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local Player = Players.LocalPlayer
local Character = Player.Character or Player.CharacterAdded:Wait()
local HRP = Character:WaitForChild("HumanoidRootPart")

-- SUAS COORDENADAS
local Locais = {
    ["SPAWN"]            = CFrame.new(-38, 3, 59999),
    ["SALVAR BRAINROT"]  = CFrame.new(5, 10881, 60001)
}

-- INTERFACE PRINCIPAL
local Gui = Instance.new("ScreenGui")
Gui.Name = "EsleParaSalvarBrainrots"
Gui.Parent = Player:WaitForChild("PlayerGui")
Gui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
Gui.ResetOnSpawn = false
Gui.Enabled = true

-- QUADRADO FLUTUANTE COM NOME DO JOGO (BORDA AZUL)
local QuadradoJogo = Instance.new("Frame")
QuadradoJogo.Name = "QuadradoJogo"
QuadradoJogo.Size = UDim2.new(0, 135, 0, 45)
QuadradoJogo.Position = UDim2.new(0.02, 0, 0.1, 0)
QuadradoJogo.BackgroundColor3 = Color3.new(0.08, 0.08, 0.08) -- PRETO CINZENTO
QuadradoJogo.BorderSizePixel = 2
QuadradoJogo.BorderColor3 = Color3.new(0, 0.5, 1) -- AZUL
QuadradoJogo.Visible = true
QuadradoJogo.Draggable = true -- PODE MEXER PARA QUALQUER LADO
QuadradoJogo.Active = true
QuadradoJogo.ZIndex = 10
QuadradoJogo.Parent = Gui

local NomeJogo = Instance.new("TextLabel")
NomeJogo.Size = UDim2.new(0.68, 0, 1, 0)
NomeJogo.Position = UDim2.new(0.05, 0, 0, 0)
NomeJogo.BackgroundTransparency = 1
NomeJogo.Text = "ESLE PARA SALVAR BRAINROTS"
NomeJogo.TextColor3 = Color3.new(1, 1, 1)
NomeJogo.Font = Enum.Font.GothamBold
NomeJogo.TextSize = 8
NomeJogo.ZIndex = 11
NomeJogo.Parent = QuadradoJogo

-- TOGGLE DE ABRIR/FECHAR COLADO NO QUADRADO
local ToggleBtn = Instance.new("TextButton")
ToggleBtn.Name = "ToggleMenu"
ToggleBtn.Size = UDim2.new(0.28, 0, 0.82, 0)
ToggleBtn.Position = UDim2.new(0.70, 0, 0.09, 0)
ToggleBtn.BackgroundColor3 = Color3.new(0, 0.35, 0.7) -- AZUL ESCURO
ToggleBtn.BorderSizePixel = 1
ToggleBtn.BorderColor3 = Color3.new(1, 1, 1)
ToggleBtn.Text = "ABRIR"
ToggleBtn.TextColor3 = Color3.new(1, 1, 1)
ToggleBtn.Font = Enum.Font.GothamBold
ToggleBtn.TextSize = 9
ToggleBtn.ZIndex = 11
ToggleBtn.Parent = QuadradoJogo

-- MENU: FUNDO PRETO + BORDA AZUL
local Menu = Instance.new("Frame")
Menu.Name = "TP_MENU"
Menu.Size = UDim2.new(0, 250, 0, 260)
Menu.Position = UDim2.new(0.5, -125, 0.5, -130)
Menu.BackgroundColor3 = Color3.new(0.06, 0.06, 0.06) -- PRETO
Menu.BorderSizePixel = 3
Menu.BorderColor3 = Color3.new(0, 0.5, 1) -- AZUL
Menu.Visible = true
Menu.Active = true
Menu.Draggable = true -- PODE MEXER PARA QUALQUER LADO
Menu.ZIndex = 9
Menu.Parent = Gui

-- CABEÇALHO
local Cabecalho = Instance.new("Frame")
Cabecalho.Size = UDim2.new(1, 0, 0, 35)
Cabecalho.BackgroundColor3 = Color3.new(0.09, 0.09, 0.09) -- PRETO MAIS CLARO
Cabecalho.BorderSizePixel = 0
Cabecalho.ZIndex = 10
Cabecalho.Parent = Menu

local Titulo = Instance.new("TextLabel")
Titulo.Size = UDim2.new(0.80, 0, 1, 0)
Titulo.Position = UDim2.new(0.04, 0, 0, 0)
Titulo.BackgroundTransparency = 1
Titulo.Text = "TP MENU | ESLE PARA SALVAR"
Titulo.TextColor3 = Color3.new(1, 1, 1)
Titulo.Font = Enum.Font.GothamBold
Titulo.TextSize = 13
Titulo.TextXAlignment = Enum.TextXAlignment.Left
Titulo.ZIndex = 11
Titulo.Parent = Cabecalho

local FecharBtn = Instance.new("TextButton")
FecharBtn.Size = UDim2.new(0.14, 0, 0.82, 0)
FecharBtn.Position = UDim2.new(0.84, 0, 0.09, 0)
FecharBtn.BackgroundColor3 = Color3.new(0.12, 0.12, 0.12)
FecharBtn.Text = "X"
FecharBtn.TextColor3 = Color3.new(1, 1, 1)
FecharBtn.Font = Enum.Font.GothamBold
FecharBtn.TextSize = 16
FecharBtn.ZIndex = 11
FecharBtn.Parent = Cabecalho

-- ABAS LATERAIS: APENAS TP / INFO
local AbasLateral = Instance.new("Frame")
AbasLateral.Size = UDim2.new(0.28, 0, 0.78, 0)
AbasLateral.Position = UDim2.new(0.03, 0, 0.17, 0)
AbasLateral.BackgroundColor3 = Color3.new(0.09, 0.09, 0.09) -- PRETO
AbasLateral.BorderSizePixel = 0
AbasLateral.ZIndex = 10
AbasLateral.Parent = Menu

local TP_Aba = Instance.new("TextButton")
TP_Aba.Size = UDim2.new(1, 0, 0.45, 0)
TP_Aba.Position = UDim2.new(0, 0, 0.02, 0)
TP_Aba.BackgroundColor3 = Color3.new(0.07, 0.07, 0.07) -- PRETO MAIS ESCURO
TP_Aba.Text = "TP"
TP_Aba.TextColor3 = Color3.new(1, 1, 1)
TP_Aba.Font = Enum.Font.GothamBold
TP_Aba.TextSize = 13
TP_Aba.ZIndex = 11
TP_Aba.Parent = AbasLateral

local INFO_Aba = Instance.new("TextButton")
INFO_Aba.Size = UDim2.new(1, 0, 0.45, 0)
INFO_Aba.Position = UDim2.new(0, 0, 0.53, 0)
INFO_Aba.BackgroundColor3 = Color3.new(0.09, 0.09, 0.09) -- PRETO
INFO_Aba.Text = "INFO"
INFO_Aba.TextColor3 = Color3.new(0.7, 0.7, 0.7)
INFO_Aba.Font = Enum.Font.GothamBold
INFO_Aba.TextSize = 12
INFO_Aba.ZIndex = 11
INFO_Aba.Parent = AbasLateral

-- CONTEÚDO INFO
local InfoConteudo = Instance.new("Frame")
InfoConteudo.Size = UDim2.new(0.66, 0, 0.78, 0)
InfoConteudo.Position = UDim2.new(0.31, 0, 0.17, 0)
InfoConteudo.BackgroundColor3 = Color3.new(0.07, 0.07, 0.07) -- PRETO
InfoConteudo.Visible = false
InfoConteudo.ZIndex = 10
InfoConteudo.Parent = Menu

local TextoInfo = Instance.new("TextLabel")
TextoInfo.Size = UDim2.new(0.90, 0, 0.90, 0)
TextoInfo.Position = UDim2.new(0.05, 0, 0.05, 0)
TextoInfo.BackgroundTransparency = 1
TextoInfo.Text = "✅ TP funcionais\n✅ Menu arrastável\n✅ Visual Preto e Azul\n✅ Sem aba SET"
TextoInfo.TextColor3 = Color3.new(1, 1, 1)
TextoInfo.Font = Enum.Font.Gotham
TextoInfo.TextSize = 11
TextoInfo.TextWrapped = true
TextoInfo.ZIndex = 11
TextoInfo.Parent = InfoConteudo

-- CONTEÚDO TP
local TPConteudo = Instance.new("Frame")
TPConteudo.Size = UDim2.new(0.66, 0, 0.78, 0)
TPConteudo.Position = UDim2.new(0.31, 0, 0.17, 0)
TPConteudo.BackgroundColor3 = Color3.new(0.07, 0.07, 0.07) -- PRETO
TPConteudo.Visible = true
TPConteudo.ZIndex = 10
TPConteudo.Parent = Menu

-- FUNÇÃO CRIAR BOTÕES COM BORDA AZUL
local function CriarBotao(nome, posY)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(0.92, 0, 0, 85)
    btn.Position = UDim2.new(0.04, 0, posY, 0)
    btn.BackgroundColor3 = Color3.new(0.11, 0.11, 0.11) -- PRETO MAIS CLARO
    btn.BorderSizePixel = 1
    btn.BorderColor3 = Color3.new(0, 0.5, 1) -- AZUL
    btn.Text = "📍 "..nome
    btn.TextColor3 = Color3.new(1, 1, 1)
    btn.Font = Enum.Font.GothamBold
    btn.TextSize = 13
    btn.ZIndex = 11
    btn.Parent = TPConteudo

    btn.MouseButton1Click:Connect(function()
        Character = Player.Character or Player.CharacterAdded:Wait()
        HRP = Character:FindFirstChild("HumanoidRootPart")
        if HRP then HRP.CFrame = Locais[nome] end
    end)
end

-- ADICIONA PONTOS
CriarBotao("SPAWN", 0.05)
CriarBotao("SALVAR BRAINROT", 0.55)

-- TROCAR DE ABA
TP_Aba.MouseButton1Click:Connect(function()
    TP_Aba.BackgroundColor3 = Color3.new(0.07, 0.07, 0.07)
    TP_Aba.TextColor3 = Color3.new(1,1,1)
    INFO_Aba.BackgroundColor3 = Color3.new(0.09, 0.09, 0.09)
    INFO_Aba.TextColor3 = Color3.new(0.7,0.7,0.7)
    TPConteudo.Visible = true
    InfoConteudo.Visible = false
end)

INFO_Aba.MouseButton1Click:Connect(function()
    INFO_Aba.BackgroundColor3 = Color3.new(0.07,0.07,0.07)
    INFO_Aba.TextColor3 = Color3.new(1,1,1)
    TP_Aba.BackgroundColor3 = Color3.new(0.09,0.09,0.09)
    TP_Aba.TextColor3 = Color3.new(0.7,0.7,0.7)
    TPConteudo.Visible = false
    InfoConteudo.Visible = true
end)

-- ABRIR / FECHAR
ToggleBtn.MouseButton1Click:Connect(function()
    Menu.Visible = not Menu.Visible
    ToggleBtn.Text = Menu.Visible and "FECHAR" or "ABRIR"
end)

FecharBtn.MouseButton1Click:Connect(function()
    Menu.Visible = false
    ToggleBtn.Text = "ABRIR"
end)

