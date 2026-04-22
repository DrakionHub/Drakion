-- =========================
-- Drakion Hub - Blox Fruit
-- =========================
local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local player = Players.LocalPlayer
local function isPress(input)
    return input.UserInputType == Enum.UserInputType.MouseButton1
        or input.UserInputType == Enum.UserInputType.Touch
end

---- função para proporcionar a Gui de acordo com o dispositivo do usuário
local function adjustGuiSize(variave, Tmh, T)
    if UserInputService.TouchEnabled and not UserInputService.KeyboardEnabled then
    -- Mobile
    variave.Size = UDim2.new(0, Tmh/4 * 3, 0, T/4 * 3)
    else
    -- Pc
        variave.Size = UDim2.new(0, Tmh, 0, T)
   end
end

-- GUI PRINCIPAL
local gui = Instance.new("ScreenGui")
gui.Name = "DrakionHub"
gui.ResetOnSpawn = false
gui.Parent = player:WaitForChild("PlayerGui")

local mainFrame = Instance.new("Frame", gui)
mainFrame.Name = "MainFrame"
adjustGuiSize(mainFrame, 600, 350) -- tamanho base para PC, será ajustado para mobile
mainFrame.AnchorPoint = Vector2.new(0.5, 0.5)
mainFrame.Position = UDim2.new(0.5, 0, 0.5, 0)
-- começa escondido; será mostrado pelo botão de toggle
mainFrame.Visible = false
mainFrame.BorderSizePixel = 0
mainFrame.BackgroundTransparency = 0.15
mainFrame.BackgroundColor3 = Color3.fromRGB(0,0,0)

Instance.new("UICorner", mainFrame).CornerRadius = UDim.new(0, 5)

local stroke1 = Instance.new("UIStroke", mainFrame)
stroke1.Color = Color3.fromRGB(0,0,0)
stroke1.Thickness = 4
stroke1.Transparency = 0

-- =========================
-- DRAG UI
-- =========================
do
    local dragging, dragStart, startPos
    mainFrame.InputBegan:Connect(function(input)
      if isPress(input) then
           dragging = true
          dragStart = input.Position
           startPos = mainFrame.Position
      end
    end)

    mainFrame.InputEnded:Connect(function(input)
      if isPress(input) then
         dragging = false
       end
    end)

    UserInputService.InputChanged:Connect(function(input)
       if dragging and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
          local delta = input.Position - dragStart
          mainFrame.Position = UDim2.new(
              startPos.X.Scale, startPos.X.Offset + delta.X,
              startPos.Y.Scale, startPos.Y.Offset + delta.Y
           )
       end
    end)
end

---- função para proporcionar o textSize de acordo com o dispositivo do usuário
local UserInputService = game:GetService("UserInputService")

local function adjustTextSize(variavel, Tm)
    if UserInputService.TouchEnabled and not UserInputService.KeyboardEnabled then
    -- Mobile
    variavel.TextSize = Tm/4 * 3
    else
    -- Pc
        variavel.TextSize = Tm
    end 
end

local function adjustSize(variavel, Tm, Y)
    if UserInputService.TouchEnabled and not UserInputService.KeyboardEnabled then
    -- Mobile
    variavel.Size = UDim2.new(Tm/7 , 0, 0.35, 0)
    variavel.Position = UDim2.new(Y/1.05, 0, 0.33, 0)
    else
    -- Pc
    variavel.Size = UDim2.new(Tm/9, 0, 0.35, 0)
    variavel.Position = UDim2.new(Y, 0, 0.33, 0)
    end
end
-- =========================
-- SIDEBAR ESQUERDO
-- =========================
local sidebar = Instance.new("Frame", mainFrame)
sidebar.Name = "Sidebar"
sidebar.Size = UDim2.new(0.308, 0, 0.842, 0)
sidebar.Position = UDim2.new(0, 0, 0.157, 0)
sidebar.BackgroundColor3 = Color3.fromRGB(3,0,75)
sidebar.BorderSizePixel = 0
sidebar.BackgroundTransparency = 1

local stroke = Instance.new("UIStroke", sidebar)
stroke.Color = Color3.fromRGB(0,0,0)
stroke.Thickness = 4
stroke.Transparency = 0

Instance.new("UICorner", sidebar).CornerRadius = UDim.new(0, 5)

local headerFrame = Instance.new("Frame", mainFrame)
headerFrame.Name = "HeaderFrame"
headerFrame.Size = UDim2.new(1, 0, 0, 50)
headerFrame.Position = UDim2.new(0, 0, 0, 0)
headerFrame.BackgroundTransparency = 1
headerFrame.BorderSizePixel = 0

-- Logo
local logo = Instance.new("ImageLabel", mainFrame)
logo.Name = "Logo"
logo.Size = UDim2.new(0.1666, 0, 0.2857, 0)
logo.Position = UDim2.new(0, 0, -0.086, 0)
logo.BackgroundTransparency = 1
logo.Image = "rbxassetid://129327299482883" -- troque pelo ID do seu arquivo
logo.ScaleType = Enum.ScaleType.Fit
logo.ZIndex = 3

-- Título ao lado da logo
local sidebarHeader = Instance.new("TextLabel", mainFrame)
sidebarHeader.Name = "SidebarHeader"
sidebarHeader.Size = UDim2.new(0.88, 0, 0.183, 0)
sidebarHeader.Position = UDim2.new(0.23333, 0, -0.0171, 0)
sidebarHeader.BackgroundTransparency = 1
sidebarHeader.TextColor3 = Color3.fromRGB(255,255,255)
sidebarHeader.TextScaled = false
sidebarHeader.Text = "Drakion Hub"
sidebarHeader.BorderSizePixel = 0
adjustTextSize(sidebarHeader, 35)
sidebarHeader.TextXAlignment = Enum.TextXAlignment.Left
sidebarHeader.TextYAlignment = Enum.TextYAlignment.Center
sidebarHeader.FontFace = Font.new(
    "rbxasset://fonts/families/BuilderSans.json",
    Enum.FontWeight.ExtraBold,
    Enum.FontStyle.Normal
)

-- gradiente dourado:
local grad = Instance.new("UIGradient", sidebarHeader)
grad.Color = ColorSequence.new{
	ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 244, 200)),
	ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 218, 27)),
	ColorSequenceKeypoint.new(0.05, Color3.fromRGB(160, 120, 30)),
	ColorSequenceKeypoint.new(0.2, Color3.fromRGB(160, 120, 30)),
	ColorSequenceKeypoint.new(0.9, Color3.fromRGB(255, 218, 27)),
	ColorSequenceKeypoint.new(1, Color3.fromRGB(255, 244, 200))}


local stroke = Instance.new("UIStroke", sidebarHeader)
stroke.Color = Color3.fromRGB(0,0,0)
stroke.Thickness = 2

-- Menu Items
local menuItems = {
    "Discord",
    "Main Farm",
    "Itens Quest",
	"Farm Outher",
    "Dungeon and Raid",
    "Teleport",
    "Fruits",
    "Shop",
    "Setting",
}

local scrollFrame = Instance.new("ScrollingFrame", mainFrame)
scrollFrame.Name = "MenuScroll"
scrollFrame.Size = UDim2.new(0.308, 0, 0.806, 0)
scrollFrame.Position = UDim2.new(0, 0, 0.183, 0)
scrollFrame.BackgroundTransparency = 1
scrollFrame.BorderSizePixel = 0
scrollFrame.ScrollBarThickness = 6
scrollFrame.CanvasSize = UDim2.new(0, 0, 0, #menuItems * 40)
Instance.new("UICorner", scrollFrame).CornerRadius = UDim.new(0, 5)

--sinalizador de menu selecionado
local selectedIndicator = Instance.new("Frame", scrollFrame)
selectedIndicator.Name = "Indicator"
selectedIndicator.Size = UDim2.new(0.027, 0, 0.0596, 0)
selectedIndicator.Position = UDim2.new(0.0541, 0, 0.15, 0) -- posição inicial, será movida para o botão selecionado
selectedIndicator.BackgroundColor3 = Color3.fromRGB(255,255,255)
selectedIndicator.BorderSizePixel = 0
selectedIndicator.Visible = false -- começa invisível, só mostra quando um menu é selecionado
selectedIndicator.BackgroundTransparency = 0
Instance.new("UICorner", selectedIndicator).CornerRadius = UDim.new(0, 4)
selectedIndicator.ZIndex = 3

for i, itemName in ipairs(menuItems) do
    local menuButton = Instance.new("TextButton", scrollFrame)
    menuButton.Name = itemName
    menuButton.Size = UDim2.new(0.9, 0, 0.1, 0)
    menuButton.Position = UDim2.new(0.05, 0,  (i - 1) * 0.11, 0)
    menuButton.BackgroundColor3 = Color3.fromRGB(212,12,12)
	menuButton.BackgroundTransparency = 0.3
    menuButton.TextColor3 =
    Color3.fromRGB(255,255,255)
    menuButton.Text = itemName
    menuButton.BorderSizePixel = 0
    Instance.new("UICorner", menuButton).CornerRadius = UDim.new(0, 4)
    menuButton.TextScaled = false
    adjustTextSize(menuButton, 20)
    menuButton.Localize = false
    menuButton.ZIndex = 2
    menuButton.FontFace = Font.new(
    "rbxasset://fonts/families/BuilderSans.json",
    Enum.FontWeight.ExtraBold,
    Enum.FontStyle.Normal
)
    stroke = Instance.new("UIStroke", menuButton)
    stroke.Thickness = 2
    stroke.Transparency = 0

-- gradiente dourado:
local grad = Instance.new("UIGradient", menuButton)
grad.Color = ColorSequence.new{
	ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 244, 200)),
	ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 218, 27)),
	ColorSequenceKeypoint.new(0.05, Color3.fromRGB(160, 120, 30)),
	ColorSequenceKeypoint.new(0.2, Color3.fromRGB(160, 120, 30)),
	ColorSequenceKeypoint.new(0.9, Color3.fromRGB(255, 218, 27)),
	ColorSequenceKeypoint.new(1, Color3.fromRGB(255, 244, 200))}


    -- escurece ligeiramente ao passar o mouse
    menuButton.MouseEnter:Connect(function()
        menuButton.BackgroundTransparency = 0.6
    end)
    menuButton.MouseLeave:Connect(function()
        menuButton.BackgroundTransparency = 0.3
    end)

    -- move indicator when button is clicked
    menuButton.MouseButton1Click:Connect(function()
        selectedIndicator.Position = UDim2.new(0.0541, 0, 0.015 + (i - 1) * 0.111, 0)
        selectedIndicator.Visible = true
    end)
end

-- gradiente dourado:
local grad = Instance.new("UIGradient", selectedIndicator)
grad.Color = ColorSequence.new{
	ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 244, 200)),
	ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 218, 27)),
	ColorSequenceKeypoint.new(0.05, Color3.fromRGB(160, 120, 30)),
	ColorSequenceKeypoint.new(0.2, Color3.fromRGB(160, 120, 30)),
	ColorSequenceKeypoint.new(0.9, Color3.fromRGB(255, 218, 27)),
	ColorSequenceKeypoint.new(1, Color3.fromRGB(255, 244, 200))}


	grad.Rotation = 90

-- start indicator on Discord menu (first item)
selectedIndicator.Position = UDim2.new(0.0541, 0, 0.015, 0)
selectedIndicator.Visible = true
 
-- =========================
-- ÁREA PRINCIPAL (DIREITA)
-- =========================
local contentArea = Instance.new("Frame", mainFrame)
contentArea.Name = "ContentArea"
contentArea.Size = UDim2.new(0.6833, 0, 0.8428, 0)
contentArea.Position = UDim2.new(0.3166, 0, 0.1571, 0)
contentArea.BackgroundColor3 = Color3.fromRGB(3,0, 75)
contentArea.BorderSizePixel = 0
contentArea.BackgroundTransparency = 1
Instance.new("UICorner", contentArea).CornerRadius = UDim.new(0, 5)

local stroke2 = Instance.new("UIStroke", contentArea)
stroke2.Color = Color3.fromRGB(0,0,0)
stroke2.Thickness = 4
stroke2.Transparency = 0

-- Header da página
local pageHeader = Instance.new("TextLabel", contentArea)
pageHeader.Name = "PageHeader"
pageHeader.Size = UDim2.new(0.878, 0, 0.1694, 0)
pageHeader.Position = UDim2.new(0.1707, 0, -0.1796, 0)
pageHeader.TextColor3 = Color3.fromRGB(255, 255, 255)
pageHeader.BackgroundColor3 = Color3.fromRGB(3,0, 75)
pageHeader.BackgroundTransparency = 1
pageHeader.Text = " discord.gg/Nfh5Sczyqz"
pageHeader.BorderSizePixel = 0
pageHeader.TextScaled = false
adjustTextSize(pageHeader, 15)
pageHeader.Font = Enum.Font.LuckiestGuy
pageHeader.TextXAlignment = Enum.TextXAlignment.Center
pageHeader.TextYAlignment = Enum.TextYAlignment.Center
pageHeader.TextTransparency = 0
Instance.new("UICorner", pageHeader).CornerRadius = UDim.new(0, 5)

-- gradiente dourado:
local grad = Instance.new("UIGradient", pageHeader)
grad.Color = ColorSequence.new{
	ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 244, 200)),
	ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 218, 27)),
	ColorSequenceKeypoint.new(0.05, Color3.fromRGB(160, 120, 30)),
	ColorSequenceKeypoint.new(0.2, Color3.fromRGB(160, 120, 30)),
	ColorSequenceKeypoint.new(0.9, Color3.fromRGB(255, 218, 27)),
	ColorSequenceKeypoint.new(1, Color3.fromRGB(255, 244, 200))}


local stroke = Instance.new("UIStroke", pageHeader)
stroke.Color = Color3.fromRGB(0,0,0)
stroke.Thickness = 2

 -- white underline below PageHeader
local headerUnderline = Instance.new("Frame", pageHeader)
headerUnderline.Name = "HeaderUnderline"
headerUnderline.Size = UDim2.new(1.68, 0, 0.08, 0)
headerUnderline.Position = UDim2.new(-0.729, 0, 0.9765, 0) -- right under headerFrame height
headerUnderline.BackgroundColor3 = Color3.fromRGB(0,0,0)
headerUnderline.BorderSizePixel = 0
headerUnderline.ZIndex = 2

-- Botão X (Fechar)
local closeBtn = Instance.new("TextButton", pageHeader)
closeBtn.Name = "CloseButton"
closeBtn.Size = UDim2.new(0.0833, 0, 0.6003, 0)
closeBtn.Position = UDim2.new(0.8194, 0, 0.15, 0)
closeBtn.BackgroundColor3 = Color3.fromRGB(212,12,12)
closeBtn.TextColor3 = Color3.fromRGB(255,255,255)
closeBtn.TextScaled = true
closeBtn.Text = "×"
closeBtn.BorderSizePixel = 0
closeBtn.BackgroundTransparency = 0
Instance.new("UICorner", closeBtn).CornerRadius = UDim.new(0, 4)

local stroke3 = Instance.new("UIStroke", closeBtn)
stroke3.Color = Color3.fromRGB(255,255,255)
stroke3.Thickness = 0.5
stroke3.Transparency = 0

closeBtn.MouseButton1Click:Connect(function()
    gui:Destroy()
end)

-- botão simples para abrir/fechar a interface principal
local toggleBtn = Instance.new("ImageButton", gui)
toggleBtn.Name = "ToggleButton"
if UserInputService.TouchEnabled and not UserInputService.KeyboardEnabled then
    -- Mobile
    toggleBtn.Size = UDim2.new(0, 80, 0, 80)
    else    -- Pc
    toggleBtn.Size = UDim2.new(0,115,0,110.5)
end
if UserInputService.TouchEnabled and not UserInputService.KeyboardEnabled then
    -- Mobile
     toggleBtn.Position = UDim2.new(0,7,0.7,0)
    else    -- Pc
     toggleBtn.Position = UDim2.new(0,7,0.85,0)
end
toggleBtn.Image = "rbxassetid://129327299482883" -- troque pelo ID do seu arquivo (pode ser o mesmo da logo)
toggleBtn.BackgroundTransparency = 1
toggleBtn.BorderSizePixel = 0
toggleBtn.ZIndex = 2
Instance.new("UICorner", toggleBtn).CornerRadius = UDim.new(0, 10)

toggleBtn.MouseButton1Click:Connect(function()
    mainFrame.Visible = not mainFrame.Visible
end)
 -- =========================
 -- =========================
-- DRAG UI botão da interface
-- =========================
do
    local dragging, dragStart, startPos
    toggleBtn.InputBegan:Connect(function(input)
        if isPress(input) then
            dragging = true
            dragStart = input.Position
            startPos = toggleBtn.Position
        end
    end)
    toggleBtn.InputEnded:Connect(function(input)
        if isPress(input) then dragging = false end
    end)
    UserInputService.InputChanged:Connect(function(input)
        if dragging and (input.UserInputType == Enum.UserInputType.MouseMovement
            or input.UserInputType == Enum.UserInputType.Touch) then
            local delta = input.Position - dragStart
            toggleBtn.Position = UDim2.new(
                startPos.X.Scale, startPos.X.Offset + delta.X,
                startPos.Y.Scale, startPos.Y.Offset + delta.Y
            )
        end
    end)
end

-- references to menu buttons for later use
local discordBtn = scrollFrame:FindFirstChild("Discord")
local mainFarmBtn = scrollFrame:FindFirstChild("Main Farm")
local itensQuestBtn = scrollFrame:FindFirstChild("Itens Quest")
local FarmOutherBtn = scrollFrame:FindFirstChild("Farm Outher")
local dungeonRaidBtn = scrollFrame:FindFirstChild("Dungeon and Raid")
local teleportBtn = scrollFrame:FindFirstChild("Teleport")
local fruitsBtn = scrollFrame:FindFirstChild("Fruits")
local shopBtn = scrollFrame:FindFirstChild("Shop")
local settingBtn = scrollFrame:FindFirstChild("Setting")

-- table holding each page frame for easy hiding/showing
local pages = {}

local function showOnly(frame)
    for _, f in pairs(pages) do
        f.Visible = (f == frame)
    end
    -- update header text if you want
    if frame and frame.Name then
        pageHeader.Text = frame.Name:gsub("([A-Z])"," %1"):gsub("^%s+","")
        pageHeader.Localize = false
    end
end

---- Titulo das funções
local function createPageTitle(text, y, posicao)
    local TituloEntreAsFuncoes = Instance.new("TextLabel", posicao)
    TituloEntreAsFuncoes.Name = text
    TituloEntreAsFuncoes.Size = UDim2.new(0.9, 0, 0, 50)
    TituloEntreAsFuncoes.Position = UDim2.new(0.05, 0, 0, y)
    TituloEntreAsFuncoes.BackgroundTransparency = 1
    TituloEntreAsFuncoes.TextColor3 = Color3.fromRGB(255,255,255)
    TituloEntreAsFuncoes.Text = text
    TituloEntreAsFuncoes.TextScaled = false
    TituloEntreAsFuncoes.BorderSizePixel = 0
    TituloEntreAsFuncoes.TextTransparency = 0
    Instance.new("UICorner", TituloEntreAsFuncoes).CornerRadius = UDim.new(0, 4)
    TituloEntreAsFuncoes.FontFace = Font.new(
        "rbxasset://fonts/families/BuilderSans.json",
        Enum.FontWeight.ExtraBold,
        Enum.FontStyle.Normal
    )
    TituloEntreAsFuncoes.Localize = false
    TituloEntreAsFuncoes.ZIndex = 2
    adjustTextSize(TituloEntreAsFuncoes, 20)

    local stroke3 = Instance.new("UIStroke", TituloEntreAsFuncoes)
    stroke3.Thickness = 2
    stroke3.Transparency = 0

    -- gradiente dourado:
    local grad = Instance.new("UIGradient", TituloEntreAsFuncoes)
    grad.Color = ColorSequence.new{
    	ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 244, 200)),
    	ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 218, 27)),
    	ColorSequenceKeypoint.new(0.05, Color3.fromRGB(160, 120, 30)),
    	ColorSequenceKeypoint.new(0.2, Color3.fromRGB(160, 120, 30)),
    	ColorSequenceKeypoint.new(0.9, Color3.fromRGB(255, 218, 27)),
    	ColorSequenceKeypoint.new(1, Color3.fromRGB(255, 244, 200))}

    local UnderLineTtulo = Instance.new("Frame", posicao)
    UnderLineTtulo.Name = "UnderLineAutoStatus"
    UnderLineTtulo.Size = UDim2.new(0.9, 0, 0, 5.99)
    UnderLineTtulo.Position = UDim2.new(0.05, 0, 0, y + 40)
    UnderLineTtulo.BackgroundTransparency = 0
    UnderLineTtulo.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    UnderLineTtulo.BorderSizePixel = 0
    Instance.new("UICorner", UnderLineTtulo).CornerRadius = UDim.new(0, 4)

    -- gradiente dourado:
    local grad = Instance.new("UIGradient", UnderLineTtulo)
    grad.Color = ColorSequence.new{
    	ColorSequenceKeypoint.new(0, Color3.fromRGB(212, 12, 12)),
    	ColorSequenceKeypoint.new(0.4, Color3.fromRGB(255, 218, 27)),
    	ColorSequenceKeypoint.new(0.5, Color3.fromRGB(160, 120, 30)),
    	ColorSequenceKeypoint.new(0.7, Color3.fromRGB(255, 218, 27)),
    	ColorSequenceKeypoint.new(0.9, Color3.fromRGB(212, 12, 12)),
    	ColorSequenceKeypoint.new(1, Color3.fromRGB(212, 12, 12))
    }

    grad.Transparency = NumberSequence.new{
        NumberSequenceKeypoint.new(0, 1),
       NumberSequenceKeypoint.new(0.4, 0),
       NumberSequenceKeypoint.new(0.7, 0),
      NumberSequenceKeypoint.new(1, 1),
    }
    return TituloEntreAsFuncoes 
end

--- Rodapé das Tabs
local function createFooter(y1, y2, posicao)
    local UnderLineRodape = Instance.new("Frame", posicao)
    UnderLineRodape.Name = "UnderLineRodape"
    UnderLineRodape.Size = UDim2.new(1, 0, 0, 5.99)
    UnderLineRodape.Position = UDim2.new(0 , 0, y1, 0)
    UnderLineRodape.BackgroundTransparency = 0
    UnderLineRodape.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    UnderLineRodape.BorderSizePixel = 0
    Instance.new("UICorner", UnderLineRodape).CornerRadius = UDim.new(0, 4)

    -- gradiente dourado:
    local grad = Instance.new("UIGradient", UnderLineRodape)
    grad.Color = ColorSequence.new{
	ColorSequenceKeypoint.new(0, Color3.fromRGB(212, 12, 12)),
	ColorSequenceKeypoint.new(0.4, Color3.fromRGB(255, 218, 27)),
	ColorSequenceKeypoint.new(0.5, Color3.fromRGB(160, 120, 30)),
	ColorSequenceKeypoint.new(0.7, Color3.fromRGB(255, 218, 27)),
	ColorSequenceKeypoint.new(0.9, Color3.fromRGB(212, 12, 12)),
	ColorSequenceKeypoint.new(1, Color3.fromRGB(212, 12, 12))
    }

    grad.Transparency = NumberSequence.new{
        NumberSequenceKeypoint.new(0, 1),
        NumberSequenceKeypoint.new(0.5, 0),
       NumberSequenceKeypoint.new(0.6, 0),
       NumberSequenceKeypoint.new(1, 1),
    }

    local LogoRodape = Instance.new("ImageLabel", posicao)
    LogoRodape.Size = UDim2.new(0, 35, 0, 35)
    LogoRodape.Position = UDim2.new(0.08,0,  y1 + y2, 0)
    LogoRodape.BackgroundTransparency = 1
    LogoRodape.Image = "rbxassetid://129327299482883"

    local TextRodape = Instance.new("TextLabel", posicao)
    TextRodape.Size = UDim2.new(0, 100, 0, 20)
    TextRodape.Position = UDim2.new(0.4, 0, y1 + y2 * 2,5, 0)
    TextRodape.BackgroundTransparency = 1
    TextRodape.TextColor3 = Color3.fromRGB(255, 255, 255)
    TextRodape.Text = "Drakion Hub  -  BY  龙'¨'珠- The Black -龙'¨'珠"
    TextRodape.TextScaled = false
    TextRodape.BorderSizePixel = 0
    TextRodape.TextTransparency = 0
    TextRodape.FontFace = Font.new(
     "rbxasset://fonts/families/GrenzeGotisch.json",
      Enum.FontWeight.ExtraBold,
      Enum.FontStyle.Normal
    )
    TextRodape.Localize = false
    TextRodape.ZIndex = 2
    adjustTextSize(TextRodape, 20)

     local grad = Instance.new("UIGradient", TextRodape)
     grad.Color = ColorSequence.new{
       ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 218, 27)),
       ColorSequenceKeypoint.new(0.1, Color3.fromRGB(160, 120, 30)),
       ColorSequenceKeypoint.new(1, Color3.fromRGB(255, 218, 27))}
        return UnderLineRodape, LogoRodape, TextRodape
     end

--- Botão das funções
local function createButton(text, y, posicao)
    local Botaoprincipal = Instance.new("Frame", posicao)
    Botaoprincipal.Name = text
    Botaoprincipal.Size = UDim2.new(0.9, 0, 0, 40)
    Botaoprincipal.Position = UDim2.new(0.05, 0, y, 0)
    Botaoprincipal.BackgroundTransparency = 0
    Botaoprincipal.BackgroundColor3 = Color3.fromRGB(0,0,0)
    Botaoprincipal.BorderSizePixel = 0
    Instance.new("UICorner", Botaoprincipal).CornerRadius = UDim.new(0, 4)
    Botaoprincipal.Localize = false

    local BotaoprincipalText = Instance.new("TextLabel", Botaoprincipal)
    BotaoprincipalText.Name = text.."Text"
    BotaoprincipalText.Size = UDim2.new(1, 0, 1, 0)
    BotaoprincipalText.Position = UDim2.new(0.05, 0, 0, 0)
    BotaoprincipalText.BackgroundTransparency = 1
    BotaoprincipalText.TextColor3 = Color3.fromRGB(255, 255, 255)
    BotaoprincipalText.Text = text
    BotaoprincipalText.TextScaled = false
    BotaoprincipalText.BorderSizePixel = 0
    BotaoprincipalText.TextTransparency = 0
    BotaoprincipalText.FontFace = Font.new(
        "rbxasset://fonts/families/BuilderSans.json",
        Enum.FontWeight.ExtraBold,
       Enum.FontStyle.Normal
    )
    BotaoprincipalText.TextXAlignment = Enum.TextXAlignment.Left
    BotaoprincipalText.TextYAlignment = Enum.TextYAlignment.Center
    BotaoprincipalText.Localize = false
    BotaoprincipalText.ZIndex = 2
    adjustTextSize(BotaoprincipalText, 18)

    local grad = Instance.new("UIGradient", BotaoprincipalText)
    grad.Color = ColorSequence.new{
    	ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 244, 200)),
    	ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 218, 27)),
    	ColorSequenceKeypoint.new(0.05, Color3.fromRGB(160, 120, 30)),
    	ColorSequenceKeypoint.new(0.2, Color3.fromRGB(160, 120, 30)),
    	ColorSequenceKeypoint.new(0.9, Color3.fromRGB(255, 218, 27)),
    	ColorSequenceKeypoint.new(1, Color3.fromRGB(255, 244, 200))}

    local stroke3 = Instance.new("UIStroke", BotaoprincipalText)
    stroke3.Thickness = 2

    ----botão do button
    local ButtonOfTheBotao = Instance.new("ImageButton", Botaoprincipal)
    ButtonOfTheBotao.Name = text.."Button"
    adjustSize(ButtonOfTheBotao, 0.4, 0.9)
    ButtonOfTheBotao.BackgroundTransparency = 0
    ButtonOfTheBotao.BackgroundColor3 = Color3.fromRGB(212,12,12)
    ButtonOfTheBotao.ImageTransparency = 1
    ButtonOfTheBotao.BorderSizePixel = 0
    Instance.new("UICorner", ButtonOfTheBotao).CornerRadius = UDim.new(0, 2)
    ButtonOfTheBotao.Localize = false

    local outerStroke = Instance.new("UIStroke", ButtonOfTheBotao)
    outerStroke.Color = Color3.fromRGB(0,0,0)
    outerStroke.Thickness = 2

    local inner = Instance.new("Frame", ButtonOfTheBotao)
    inner.Size = UDim2.new(1.5, 0, 1.5, 0)
    inner.Position = UDim2.new(-0.255, 0, -0.25, 0)
    inner.BackgroundTransparency = 1
    inner.BorderSizePixel = 0
    Instance.new("UICorner", inner).CornerRadius = UDim.new(0, 4)

    local innerStroke = Instance.new("UIStroke", inner)
    innerStroke.Color = Color3.fromRGB(212,12,12)
    innerStroke.Thickness = 2
    return Botaoprincipal
end

----notificações

local function showNotification(yt, text)
 
    -- Criar mini GUI de notificação
    local notificationGui = Instance.new("ScreenGui")
     notificationGui.Name = "NotificationGui"
     notificationGui.ResetOnSpawn = false
     notificationGui.Parent = player:WaitForChild("PlayerGui")
     
     local notificationFrame = Instance.new("Frame", notificationGui)
     notificationFrame.Name = "NotificationFrame"
     notificationFrame.Size = UDim2.new(0, 320, 0, yt)
     notificationFrame.AnchorPoint = Vector2.new(1, 1)
     notificationFrame.Position = UDim2.new(1, -10, 1, -10)
     notificationFrame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
     notificationFrame.BackgroundTransparency = 0.1
     notificationFrame.BorderSizePixel = 0
     Instance.new("UICorner", notificationFrame).CornerRadius = UDim.new(0, 5)
     
     local stroke3 = Instance.new("UIStroke", notificationFrame)
     stroke3.Color = Color3.fromRGB(212, 12, 12)
     stroke3.Thickness = 3
     stroke3.Transparency = 0

    local notificationText = Instance.new("TextLabel", notificationFrame)
    notificationText.Name = "NotificationText"
    notificationText.Size = UDim2.new(0, 250, 0, 40)
    notificationText.Position = UDim2.new(0, 60, 0, 9)
    notificationText.BackgroundTransparency = 1
    notificationText.TextColor3 = Color3.fromRGB(212, 12, 12)
    notificationText.Text = text
    notificationText.TextScaled = true
    notificationText.Font = Enum.Font.SourceSansBold
    notificationText.TextXAlignment = Enum.TextXAlignment.Center
    notificationText.TextYAlignment = Enum.TextYAlignment.Center

    local notificationicon = Instance.new("ImageLabel", notificationFrame)
    notificationicon.Name = "NotificationIcon"
    notificationicon.Size = UDim2.new(0, 50, 0, 50)
    notificationicon.Position = UDim2.new(0, 7, 0, 5)
    notificationicon.BackgroundTransparency = 1
    notificationicon.Image = "rbxassetid://129327299482883"
    notificationicon.BorderSizePixel = 0
    Instance.new("UICorner", notificationicon).CornerRadius = UDim.new(0, 10)
    notificationicon.ZIndex = 3


    wait(3)
    notificationGui:Destroy()
end

------ função dos botões de selecionar
local function Selectbutton(posicao, textLabel, yoptions, yposition, options)
    local backgroundselect = Instance.new("Frame", posicao)
    backgroundselect.Size = UDim2.new(0.9, 0, 0, 40)
    backgroundselect.Position = UDim2.new(0.05, 0, yposition, 0)
    backgroundselect.BackgroundColor3 = Color3.fromRGB(0,0,0)
    backgroundselect.BorderSizePixel = 0
    Instance.new("UICorner", backgroundselect).CornerRadius = UDim.new(0, 4)
    backgroundselect.Localize = false

    local selectedLabel = Instance.new("TextLabel", backgroundselect)
    selectedLabel.Size = UDim2.new(1,-40,1,0)
    selectedLabel.Position = UDim2.new(0,0,0,0)
    selectedLabel.BackgroundTransparency = 1
    selectedLabel.Text = textLabel
    selectedLabel.TextColor3 = Color3.fromRGB(255,255,255)
    selectedLabel.TextXAlignment = Enum.TextXAlignment.Left
    selectedLabel.TextYAlignment = Enum.TextYAlignment.Center
    selectedLabel.BorderSizePixel = 0
    selectedLabel.FontFace = Font.new(
        "rbxasset://fonts/families/BuilderSans.json",
        Enum.FontWeight.ExtraBold,
        Enum.FontStyle.Normal
    )
    selectedLabel.Localize = false
    selectedLabel.ZIndex = 2
    adjustTextSize(selectedLabel, 18)

    local grad = Instance.new("UIGradient", selectedLabel)
    grad.Color = ColorSequence.new{
        ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 244, 200)),
        ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 218, 27)),
        ColorSequenceKeypoint.new(0.05, Color3.fromRGB(160, 120, 30)),
        ColorSequenceKeypoint.new(0.2, Color3.fromRGB(160, 120, 30)),
        ColorSequenceKeypoint.new(0.9, Color3.fromRGB(255, 218, 27)),
        ColorSequenceKeypoint.new(1, Color3.fromRGB(255, 244, 200))
    }

    local selectedLabelPadding = Instance.new("UIPadding", selectedLabel)
    selectedLabelPadding.PaddingLeft = UDim.new(0, 10)

    local Botaoselect = Instance.new("TextButton", backgroundselect)
    Botaoselect.Size = UDim2.new(0,40,1,0)
    Botaoselect.Position = UDim2.new(1,-40,0,0)
    Botaoselect.Text = "▼"
    Botaoselect.BackgroundColor3 = Color3.fromRGB(212, 12, 12)
    Botaoselect.TextColor3 = Color3.fromRGB(255,255,255)
    Botaoselect.BorderSizePixel = 0
    Instance.new("UICorner", Botaoselect).CornerRadius = UDim.new(0, 4)

    local gradArrow = Instance.new("UIGradient", Botaoselect)
    gradArrow.Color = ColorSequence.new{
        ColorSequenceKeypoint.new(0, Color3.fromRGB(212, 12, 12)),
        ColorSequenceKeypoint.new(0.4, Color3.fromRGB(255, 218, 27)),
        ColorSequenceKeypoint.new(0.7, Color3.fromRGB(255, 218, 27)),
        ColorSequenceKeypoint.new(0.9, Color3.fromRGB(212, 12, 12)),
        ColorSequenceKeypoint.new(1, Color3.fromRGB(212, 12, 12))
    }

    local searchBox = Instance.new("TextBox", backgroundselect)
    searchBox.Name = "SearchBox"
    searchBox.Size = UDim2.new(1,-40,1,0)
    searchBox.Position = UDim2.new(0, 0, 0, 0)
    searchBox.BackgroundColor3 = Color3.fromRGB(10,10,10)
    searchBox.BorderSizePixel = 0
    searchBox.TextColor3 = Color3.fromRGB(255,255,255)
    searchBox.PlaceholderText = "Search..."
    searchBox.Text = ""
    searchBox.ClearTextOnFocus = false
    searchBox.Font = Enum.Font.SourceSans
    adjustTextSize(searchBox, 16)
    searchBox.TextXAlignment = Enum.TextXAlignment.Left
    searchBox.TextYAlignment = Enum.TextYAlignment.Center
    local searchPadding = Instance.new("UIPadding", searchBox)
    searchPadding.PaddingLeft = UDim.new(0, 10)
    searchPadding.PaddingRight = UDim.new(0, 10)
    searchBox.ZIndex = 7
    searchBox.Visible = false
    Instance.new("UICorner", searchBox).CornerRadius = UDim.new(0, 4)
    searchBox.FontFace = Font.new(
        "rbxasset://fonts/families/BuilderSans.json",
        Enum.FontWeight.ExtraBold,
        Enum.FontStyle.Normal
    )
    searchBox.Localize = false
    searchBox.PlaceholderColor3 = Color3.fromRGB(255, 244, 200)

    local gradSearch = Instance.new("UIGradient", searchBox)
    gradSearch.Color = ColorSequence.new{
        ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 244, 200)),
        ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 218, 27)),
        ColorSequenceKeypoint.new(0.05, Color3.fromRGB(160, 120, 30)),
        ColorSequenceKeypoint.new(0.2, Color3.fromRGB(160, 120, 30)),
        ColorSequenceKeypoint.new(0.9, Color3.fromRGB(255, 218, 27)),
        ColorSequenceKeypoint.new(1, Color3.fromRGB(255, 244, 200))
    }

    local backgroundoptions = Instance.new("ScrollingFrame", posicao)
    backgroundoptions.Size = UDim2.new(0.9, 0, yoptions, 0)
    backgroundoptions.Position = UDim2.new(0.05, 0, yposition + 0.045, 0)
    backgroundoptions.BackgroundColor3 = Color3.fromRGB(0,0,0)
    backgroundoptions.BorderSizePixel = 0
    Instance.new("UICorner", backgroundoptions).CornerRadius = UDim.new(0, 4)
    backgroundoptions.ClipsDescendants = true
    backgroundoptions.Visible = false
    backgroundoptions.ScrollBarThickness = 6
    backgroundoptions.ZIndex = 5

    local stroke = Instance.new("UIStroke", backgroundoptions)
    stroke.Color = Color3.fromRGB(255,255,255)
    stroke.Thickness = 2
    local gradStroke = Instance.new("UIGradient", stroke)
    gradStroke.Color = ColorSequence.new{
        ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 244, 200)),
        ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 218, 27)),
        ColorSequenceKeypoint.new(0.05, Color3.fromRGB(160, 120, 30)),
        ColorSequenceKeypoint.new(0.2, Color3.fromRGB(160, 120, 30)),
        ColorSequenceKeypoint.new(0.9, Color3.fromRGB(255, 218, 27)),
        ColorSequenceKeypoint.new(1, Color3.fromRGB(255, 244, 200))
    }

    local layout = Instance.new("UIListLayout", backgroundoptions)
    layout.SortOrder = Enum.SortOrder.LayoutOrder
    layout.Padding = UDim.new(0, 2)

    local optionButtons = {}

    local function filterOptions()
        local query = searchBox.Text:lower()
        for _, optionBtn in ipairs(optionButtons) do
            optionBtn.Visible = query == "" or optionBtn.Text:lower():find(query, 1, true)
        end
        backgroundoptions.CanvasSize = UDim2.new(0, 0, 0, #optionButtons * 32)
    end

    local selectedOption
    local function updateSelection(button)
        if selectedOption == button.Text then
          -- Deselect
            selectedOption = nil
            selectedLabel.Text = textLabel
            backgroundoptions.Visible = false
            searchBox.Visible = false
            searchBox.Text = ""
            for _, btn in ipairs(optionButtons) do
                btn.BackgroundColor3 = Color3.fromRGB(0,0,0)
                btn.TextColor3 = Color3.fromRGB(255,255,255)
            end
        else
            -- Select
            selectedOption = button.Text
            selectedLabel.Text = selectedOption
            backgroundoptions.Visible = false
            searchBox.Visible = false
            searchBox.Text = ""
            for _, btn in ipairs(optionButtons) do
                btn.BackgroundColor3 = Color3.fromRGB(0,0,0)
                btn.TextColor3 = Color3.fromRGB(255,255,255)
            end
            button.BackgroundColor3 = Color3.fromRGB(255,255,255)
            button.TextColor3 = Color3.fromRGB(0,0,0)
        end
    end

    searchBox:GetPropertyChangedSignal("Text"):Connect(filterOptions)

    for i, name in ipairs(options) do
        local optionBtn = Instance.new("TextButton", backgroundoptions)
        optionBtn.Size = UDim2.new(1, 0, 0, 30)
        optionBtn.BackgroundColor3 = Color3.fromRGB(0,0,0)
        optionBtn.BorderSizePixel = 0
        optionBtn.TextColor3 = Color3.fromRGB(255,255,255)
        optionBtn.FontFace = Font.new(
            "rbxasset://fonts/families/BuilderSans.json",
            Enum.FontWeight.ExtraBold,
            Enum.FontStyle.Normal
        )
        adjustTextSize(optionBtn, 18)
        optionBtn.Text = name
        optionBtn.Localize = false
        optionBtn.Name = "Option"..i
        optionBtn.LayoutOrder = i
        optionBtn.TextXAlignment = Enum.TextXAlignment.Center
        optionBtn.TextYAlignment = Enum.TextYAlignment.Center
        optionBtn.ZIndex = 6
        Instance.new("UICorner", optionBtn).CornerRadius = UDim.new(0, 4)

        local gradOption = Instance.new("UIGradient", optionBtn)
        gradOption.Color = ColorSequence.new{
            ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 244, 200)),
            ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 218, 27)),
            ColorSequenceKeypoint.new(0.05, Color3.fromRGB(160, 120, 30)),
            ColorSequenceKeypoint.new(0.2, Color3.fromRGB(160, 120, 30)),
            ColorSequenceKeypoint.new(0.9, Color3.fromRGB(255, 218, 27)),
            ColorSequenceKeypoint.new(1, Color3.fromRGB(255, 244, 200))
        }

        optionBtn.MouseButton1Click:Connect(function()
            updateSelection(optionBtn)
        end)

        table.insert(optionButtons, optionBtn)
    end

    local function toggleDropdown()
        backgroundoptions.Visible = not backgroundoptions.Visible
        searchBox.Visible = backgroundoptions.Visible
        if backgroundoptions.Visible then
            searchBox.Text = ""
            filterOptions()
            backgroundoptions.CanvasPosition = Vector2.new(0, 0)
        end
    end

    Botaoselect.MouseButton1Click:Connect(toggleDropdown)

    return backgroundselect, backgroundoptions, selectedLabel
end

-- Area onde ficam as Tabs
local contend = Instance.new("Frame", contentArea)
contend.Name = "Content"
contend.Size = UDim2.new(1, 0, 1, 0)
contend.BackgroundTransparency = 1
contend.BorderSizePixel = 0

------ Scroll Das Tabs
local function createScrollArea(text, Canvasy)
    local ScrollTabs = Instance.new("ScrollingFrame", contend)
    ScrollTabs.Name = text
    ScrollTabs.Size = UDim2.new(0.9, 0, 0.9, 0)
    ScrollTabs.Position = UDim2.new(0.05, 0, 0.05, 0)
    ScrollTabs.BackgroundColor3 = Color3.fromRGB(212,12,12)
    ScrollTabs.BackgroundTransparency = 0.4
    ScrollTabs.BorderSizePixel = 0
    ScrollTabs.ZIndex = 1
    Instance.new("UICorner", ScrollTabs).CornerRadius = UDim.new(0, 4)
    ScrollTabs.ScrollBarThickness = 8
    ScrollTabs.CanvasSize = UDim2.new(0, 0, 0, Canvasy)
    ScrollTabs.Visible = false
    return ScrollTabs
end

----- Scroll da Tab Discord
local ScrollDiscord = createScrollArea("Discord", 265,482)

-- titulo do menu discord
local discordTitle = createPageTitle("Discord", 0, ScrollDiscord)

---menu discord
local link = Instance.new("Frame", ScrollDiscord)
link.Name = "Link"
link.Size = UDim2.new(0.894, 0, 0.61, 0)
link.Position = UDim2.new(0.05, 0, 0.2, 0)
link.BackgroundTransparency = 0
link.BackgroundColor3 = Color3.fromRGB(0,0,0)
link.BorderSizePixel = 0
Instance.new("UICorner", link).CornerRadius = UDim.new(0, 4)
link.Localize = false
link.ZIndex = 2

local discordLink = Instance.new("TextButton", link)
discordLink.Name = "DiscordLink"
discordLink.Size = UDim2.new(0.8184, 0, 0.185, 0)
discordLink.BackgroundTransparency = 1
discordLink.TextColor3 = Color3.fromRGB(212, 12, 12)
discordLink.Text = "https://discord.gg/Nfh5Sczyqz"
discordLink.TextScaled = false
discordLink.BorderSizePixel = 0
discordLink.TextTransparency = 0
Instance.new("UICorner", discordLink).CornerRadius = UDim.new(0, 4)
discordLink.FontFace = Font.new(
    "rbxasset://fonts/families/BuilderSans.json",
    Enum.FontWeight.ExtraBold,
    Enum.FontStyle.Normal
)
discordLink.Localize = false
discordLink.ZIndex = 3
adjustTextSize(discordLink, 20)

-----imagem do servidor
local imagelink = Instance.new("ImageButton", link)
imagelink.Name = "ToggleButton"
imagelink.Size = UDim2.new(0.2273, 0, 0.463, 0 )
imagelink.Position = UDim2.new(0.0303, 0, 0.1852, 0)
imagelink.Image = "rbxassetid://129327299482883" -- troque pelo ID do seu arquivo (pode ser o mesmo da logo)
imagelink.BackgroundTransparency = 1
imagelink.BorderSizePixel = 0
Instance.new("UICorner", imagelink).CornerRadius = UDim.new(0, 10)
imagelink.ZIndex = 3

---nome do servidor
local serverName = Instance.new("TextLabel", link)
serverName.Name = "ServerName"
serverName.Size = UDim2.new(0.818, 0, 0.1852, 0)
serverName.Position = UDim2.new(0.212, 0, 0.327, 0)
serverName.BackgroundTransparency = 1
serverName.TextColor3 = Color3.fromRGB(255, 255, 255)
serverName.Text = "Drakion hub ┃ community"
serverName.TextScaled = false
serverName.BorderSizePixel = 0
serverName.TextTransparency = 0
Instance.new("UICorner", serverName).CornerRadius = UDim.new(0, 4)
serverName.FontFace = Font.new(
    "rbxasset://fonts/families/BuilderSans.json",
    Enum.FontWeight.ExtraBold,
    Enum.FontStyle.Normal
)
serverName.Localize = false
serverName.ZIndex = 3
adjustTextSize(serverName, 20)

local stroke3 = Instance.new("UIStroke", serverName)
stroke3.Thickness = 3
stroke3.Transparency = 0

-- gradiente dourado:
local grad = Instance.new("UIGradient", serverName)
grad.Color = ColorSequence.new{
	ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 244, 200)),
	ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 218, 27)),
	ColorSequenceKeypoint.new(0.05, Color3.fromRGB(160, 120, 30)),
	ColorSequenceKeypoint.new(0.2, Color3.fromRGB(160, 120, 30)),
	ColorSequenceKeypoint.new(0.9, Color3.fromRGB(255, 218, 27)),
	ColorSequenceKeypoint.new(1, Color3.fromRGB(255, 244, 200))}

--- botão de abrir o discord
local openDiscordBtn = Instance.new("TextButton", link)
openDiscordBtn.Name = "OpenDiscord"
openDiscordBtn.Size = UDim2.new(0.879, 0, 0.228, 0)
openDiscordBtn.Position = UDim2.new(0.0606, 0, 0.6792, 0)
openDiscordBtn.BackgroundTransparency = 0
openDiscordBtn.BackgroundColor3 = Color3.fromRGB(212,12,12)
openDiscordBtn.BorderSizePixel = 0
openDiscordBtn.TextColor3 = Color3.fromRGB(255,255,255)
openDiscordBtn.Text = "Join Discord"
Instance.new("UICorner", openDiscordBtn).CornerRadius = UDim.new(0, 4)
openDiscordBtn.Localize = false
openDiscordBtn.ZIndex = 3
openDiscordBtn.FontFace = Font.new(
    "rbxasset://fonts/families/BuilderSans.json",
    Enum.FontWeight.ExtraBold,
    Enum.FontStyle.Normal
)
adjustTextSize(openDiscordBtn, 20)

    openDiscordBtn.MouseButton1Click:Connect(function()
       if setclipboard then
         setclipboard("https://discord.gg/Nfh5Sczyqz")
         showNotification(60, "Text copied to clipboard!")
     else
         showNotification(60, "Clipboard not supported")
      end
    end)
    discordLink.MouseButton1Click:Connect(function()
        if setclipboard then
            setclipboard("https://discord.gg/Nfh5Sczyqz")
            showNotification(60, "Text copied to clipboard!")
        else
            showNotification(60, "Clipboard not supported")
        end
    end)

----Rodapé
local RodapeDiscord = createFooter(0.84, 0.015, ScrollDiscord)

-- register page
pages["Discord"] = ScrollDiscord
if discordBtn then
    discordBtn.MouseButton1Click:Connect(function()
        showOnly(ScrollDiscord)
        pageHeader.Text = "discord.gg/Nfh5Sczyqz"
        pageHeader.FontFace = Font.new(
         "rbxasset://fonts/families/BuilderSans.json",
          Enum.FontWeight.ExtraBold,
          Enum.FontStyle.Normal
          )
        adjustTextSize(pageHeader, 20)
        pageHeader.Localize = false
    end)
end

----scroll area main farm
local ScrollFarm = createScrollArea("Main Farm", 1000)

-- titulo do menu farm
local MainFarmTitle = createPageTitle("Main Farm", 0, ScrollFarm)
---- menu Farm

---Farm Level
 local FarmLevel = createButton("Farm Level", 0.065, ScrollFarm)
--- farm bones
local FarmBones = createButton("Farm Bones", 0.11, ScrollFarm)
----farm katakuri
local FarmKatakuri = createButton("Farm Katakuri", 0.155, ScrollFarm)
----farm Tyrant of the Skies
local FarmTyrant = createButton("Farm Tyrant of the Skies", 0.2, ScrollFarm)
----farm Nearest
local FarmNearest = createButton("Farm Nearest", 0.245, ScrollFarm)

----Titulo do menu materiais
local MaterialsTitle = createPageTitle("Materials", 280, ScrollFarm)
-----menu materiais
------select materials
local SelectMaterials = Selectbutton(ScrollFarm, "Select Material...",  0.13, 0.345, {"Vampire Fang","Fish Tail","Gunpowder","Mystic Droplet","Conjured Cocoa","Dragon Scale","Leather","Ectoplasm","Mini Tusk","Magma Ore","Scrap Metal","Angel Wings","Radioactive Material","Demonic Wisp"})

----button active Auto Materials
local AutoMaterials = createButton("Auto Materials", 0.395, ScrollFarm)

--- titulo do menu maestria
local MaestriaTitle = createPageTitle("Maestria", 430, ScrollFarm)
---- menu maestria

-----Select Method Maestria
local MethodMaestria = Selectbutton(ScrollFarm, "Method Maestria...", 0.09, 0.5, {"Sword","Blox Fruit","Gun"})

----Rolagem de porcentagem de vida para Farm maestria

local adjustScrolling = function(variavel, variavel2)
    if UserInputService.TouchEnabled and not UserInputService.KeyboardEnabled then
    ---- mobile
    variavel2.Size = UDim2.new(0.0318/3 * 4, 0, 1, 0)
    variavel.Size = UDim2.new(0.85, 0, 0.01, 0)
    variavel.Position = UDim2.new(0, 27.5/4 * 3, 0.61, 0)
    else
    ---- pc
    variavel2.Size = UDim2.new(0.0318, 0, 1, 0)
    variavel.Size = UDim2.new(0.85, 0, 0.01, 0)
    variavel.Position = UDim2.new(0, 27.5, 0.61, 0)
    end
end

local ScrollMaestria = Instance.new("Frame", ScrollFarm)
ScrollMaestria.Size = UDim2.new(0.9, 0, 0.1, 0)
ScrollMaestria.Position = UDim2.new(0.05, 0, 0.55, 0)
ScrollMaestria.BackgroundColor3 = Color3.fromRGB(0,0,0)
ScrollMaestria.BackgroundTransparency = 0
ScrollMaestria.BorderSizePixel = 0
Instance.new("UICorner", ScrollMaestria).CornerRadius = UDim.new(0, 4)
ScrollMaestria.Localize = false

local FrameTextHealth = Instance.new("Frame", ScrollMaestria)
FrameTextHealth.Size = UDim2.new(0.4, 0, 0.4, 0)
FrameTextHealth.Position = UDim2.new(0.03, 0, 0.1, 0)
FrameTextHealth.BackgroundColor3 = Color3.fromRGB(20,20,20)
FrameTextHealth.BackgroundTransparency = 0
FrameTextHealth.BorderSizePixel = 0
Instance.new("UICorner", FrameTextHealth).CornerRadius = UDim.new(0, 4)

local TextHealth = Instance.new("TextLabel", FrameTextHealth)
TextHealth.Size = UDim2.new(0.752, 0, 1, 0)
TextHealth.Position = UDim2.new(-0.15, 0, 0, 0)
TextHealth.BackgroundTransparency = 1
TextHealth.Text = "Health:"
TextHealth.TextColor3 = Color3.fromRGB(255, 255, 255)
adjustTextSize(TextHealth, 18)
TextHealth.Font = Enum.Font.SourceSansBold
TextHealth.TextYAlignment = Enum.TextYAlignment.Center

local grad = Instance.new("UIGradient", TextHealth)
grad.Color = ColorSequence.new{
    ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 244, 200)),
    ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 218, 27)),
    ColorSequenceKeypoint.new(0.05, Color3.fromRGB(160, 120, 30)),
    ColorSequenceKeypoint.new(0.2, Color3.fromRGB(160, 120, 30)),
    ColorSequenceKeypoint.new(0.9, Color3.fromRGB(255, 218, 27)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(255, 244, 200))}

local backgroundscrolling = Instance.new("Frame", ScrollFarm)
backgroundscrolling.BackgroundColor3 = Color3.new(0.2,0.2,0.2)
backgroundscrolling.BorderSizePixel = 0
backgroundscrolling.ClipsDescendants = true
backgroundscrolling.Active = true
Instance.new("UICorner", backgroundscrolling).CornerRadius = UDim.new(0, 4)

local frontscroll = Instance.new("Frame", backgroundscrolling)
frontscroll.Size = UDim2.new(0, 0, 1, 0)
frontscroll.BackgroundColor3 = Color3.fromRGB(212,12,12)
frontscroll.BorderSizePixel = 0
Instance.new("UICorner", frontscroll).CornerRadius = UDim.new(0, 4)

local buttonScroll = Instance.new("ImageButton", backgroundscrolling)
adjustScrolling(backgroundscrolling, buttonScroll)
buttonScroll.Position = UDim2.new(0, 0, 0, 0)
buttonScroll.BackgroundColor3 = Color3.fromRGB(255,255,255)
buttonScroll.BorderSizePixel = 0
buttonScroll.ZIndex = 2
buttonScroll.AutoButtonColor = false
Instance.new("UICorner", buttonScroll).CornerRadius = UDim.new(0, 8)

local valuescroll = Instance.new("TextLabel", ScrollFarm)
valuescroll.Position = UDim2.new(0.28, 0, 0.564, 0)
valuescroll.Size = UDim2.new(0.04, 0, 0.031, 0)
valuescroll.Text = "0%"
valuescroll.TextColor3 = Color3.fromRGB(255,255,255)
valuescroll.BackgroundTransparency = 1
valuescroll.Font = Enum.Font.SourceSansBold
adjustTextSize(valuescroll, 20)

local grad = Instance.new("UIGradient", valuescroll)
grad.Color = ColorSequence.new{
    ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 218, 27)),
    ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 218, 27)),
    ColorSequenceKeypoint.new(0.05, Color3.fromRGB(160, 120, 30)),
    ColorSequenceKeypoint.new(0.2, Color3.fromRGB(160, 120, 30)),
    ColorSequenceKeypoint.new(0.9, Color3.fromRGB(255, 218, 27)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(255, 218, 27))}

local minValue, maxValue = 0, 1036
local dragging = false

local function setSliderFromX(px)
    local left = backgroundscrolling.AbsolutePosition.X
    local width = backgroundscrolling.AbsoluteSize.X
    local ratio = math.clamp((px - left) / width, 0, 0.965)
    frontscroll.Size = UDim2.new(ratio + 0.01, 0, 1, 0)
    buttonScroll.Position = UDim2.new(ratio, 0, 0, 0)
    local value = math.floor(minValue + ratio * (maxValue - minValue) + 0.5)
    valuescroll.Text = tostring(value / 10) .. "%"
    return value
end

buttonScroll.InputBegan:Connect(function(input)
    if isPress(input) then
        dragging = true
    end
end)

buttonScroll.InputEnded:Connect(function(input)
    if isPress(input) then
        dragging = false
    end
end)

backgroundscrolling.InputBegan:Connect(function(input)
    if isPress(input) then
        dragging = true
        setSliderFromX(input.Position.X)
    end
end)

backgroundscrolling.InputEnded:Connect(function(input)
    if isPress(input) then
        dragging = false
    end
end)

game:GetService("UserInputService").InputChanged:Connect(function(input)
    if dragging and (input.UserInputType == Enum.UserInputType.MouseMovement
        or input.UserInputType == Enum.UserInputType.Touch) then
        setSliderFromX(input.Position.X)
    end
end)

----Auto Maestria
local AutoMaestria = createButton("Auto Maestria", 0.66, ScrollFarm)

--- Titulo do menu status
local StatusTitle = createPageTitle("Status", 695, ScrollFarm)
----menu status

-----Select Method Status
local MethodStatus = Selectbutton(ScrollFarm, "Method Status...", 0.15, 0.765, {"Melee","Defense","Sword","Gun","Blox Fruit"})

----Auto Status
local AutoStatusBtn = createButton("Auto Status", 0.815, ScrollFarm)

----Rodapé
local Rodapemainfarm = createFooter(0.96, 0.004, ScrollFarm)

-- register page and setup click to show it
pages["Main Farm"] = ScrollFarm
if mainFarmBtn then
    mainFarmBtn.MouseButton1Click:Connect(function()
        showOnly(ScrollFarm)
        pageHeader.Text = "Main Farm"
    end)
end

----scroll area Itens Quest
local ScrollItensQuest = createScrollArea("Itens Quest", 700)

-- titulo do menu Bones
local itensQuestTitle = createPageTitle("Bones", 0, ScrollItensQuest)

---- menu Bones
local RamdomSurprise = createButton("Random Surprise", 0.090, ScrollItensQuest)
local Summonsoulreaper = createButton("Auto Summon Soul Reaper", 0.154, ScrollItensQuest)
local atacksoulreaper = createButton("Auto Attack Soul Reaper", 0.218, ScrollItensQuest)

-----titulo do menu Collect
local CollectTitle = createPageTitle("Collect", 192.5, ScrollItensQuest)

---- menu Collect
local CollectChest = createButton("Collect Chest", 0.365, ScrollItensQuest)
local CollectBerry = createButton("Collect Berry", 0.429, ScrollItensQuest)

------titulo do menu TTK
local TTKTitle = createPageTitle("True Triple Katana", 340.2, ScrollItensQuest)

---- menu TTK
local BuyLegendarySword = createButton("Buy Legendary Sword", 0.576, ScrollItensQuest)
local BuyTrueTripleKatana = createButton("Buy True Triple Katana", 0.641, ScrollItensQuest)

-----titulo do menu aura colors
local AuraColorsTitle = createPageTitle("Aura Colors", 488.6, ScrollItensQuest)

---- menu aura colors
local RainbowColors = createButton("Rainbow Colors", 0.788, ScrollItensQuest)
local AutoBuyHaki = createButton("Auto Buy Haki", 0.852, ScrollItensQuest)

----Rodapé
local RodapeItensQuest = createFooter(0.942, 0.00571, ScrollItensQuest)

-- register page
pages["ItensQuest"] = ScrollItensQuest
if itensQuestBtn then
    itensQuestBtn.MouseButton1Click:Connect(function()
        showOnly(ScrollItensQuest)
    end)
end

---- scroll area Farm Outher
local ScrollFarmOuther = createScrollArea("Farm Outher", 1100)

-- Titulo do menu First Sea
local FirstSeaTitle = createPageTitle("First Sea", 0, ScrollFarmOuther)

---menu First Sea
local AutoSecondSea = createButton("Auto Second Sea", 0.059, ScrollFarmOuther)

----Titulo do menu Second Sea
local SecondSeaTitle = createPageTitle("Second Sea", 104.9, ScrollFarmOuther)

--- menu Second Sea
local AutoThirdSea = createButton("Auto Third Sea", 0.155, ScrollFarmOuther)

--- menu game events
local GameEventsTitle = createPageTitle("Game Events", 210.5, ScrollFarmOuther)

--- menu game events
local AutoPirateRaid = createButton("Auto Pirate Raid", 0.251, ScrollFarmOuther)
local AutoFactoryRaid = createButton("Auto Factory Raid", 0.291, ScrollFarmOuther)

--- Titulo do menu Law Raid Boss
local LawRaidBossTitle = createPageTitle("Law Raid Boss", 360.6, ScrollFarmOuther)

--- menu Law Raid Boss
local AutoBuymicroship = createButton("Auto Buy microship", 0.387, ScrollFarmOuther)
local StartRaidLaw = createButton("Start raid law", 0.427, ScrollFarmOuther)
local AutoAttackLaw = createButton("Auto Attack Law", 0.467, ScrollFarmOuther)

--- Título do menu Rip Indra
local RipIndraTitle = createPageTitle("Rip Indra", 554.7, ScrollFarmOuther)

--- menu Rip Indra
local AutoKillIndra = createButton("Auto Kill Indra", 0.563, ScrollFarmOuther)
local AutoSpawnRipIndra = createButton("Auto Spawn Rip Indra", 0.603, ScrollFarmOuther)

---- Título do menu Bosses
local BossesTitle = createPageTitle("Bosses", 704.8, ScrollFarmOuther)

--- menu Bosses
local AutoDarkbeard = createButton("Auto Darkbeard", 0.699, ScrollFarmOuther)
local AutoEliteHunter = createButton("Auto Elite Hunter", 0.739, ScrollFarmOuther)
local SelectBoss = Selectbutton(ScrollFarmOuther, "Select Boss...", 0.13, 0.779, {"Gorilla King","Chef","The Saw","Yeti","Mob Leader","Vice Admiral","Saber Expert","Warden","Chief Warden","Swan","Magma Admiral","Fishman Lord","Wysper","Thunder God","Cyborg","Diamond","Jeremy","Orbitus","Don Swan","Smoke Admiral","Awakened Ice Admiral","Tide Keeper Boss","Stone","Hydra Leader","Kilo Admiral","Captain Elephant","Beautiful Pirate","Longma","Cake Queen"})
local AtackBossselected = createButton("Atack Boss selected", 0.824, ScrollFarmOuther)

---Rodapé Farm Outher
local RodapeFarmOuther = createFooter(0.96, 0.003636, ScrollFarmOuther)

-- register page
pages["FarmOuther"] = ScrollFarmOuther
if FarmOutherBtn then
    FarmOutherBtn.MouseButton1Click:Connect(function()
        showOnly(ScrollFarmOuther)
    end)
end

---- scroll area Dungeon and Raid
local ScrollDungeonRaid = createScrollArea("Dungeon and Raid", 1000)

-- Menu Dungeon and Raid
local dungeonRaidTitle = createPageTitle("Dungeon and Raid", 50, ScrollDungeonRaid)

-- register page
pages["DungeonRaid"] = ScrollDungeonRaid

if dungeonRaidBtn then
    dungeonRaidBtn.MouseButton1Click:Connect(function()
        showOnly(ScrollDungeonRaid)
    end)
end

---- scroll area Teleport
local ScrollTeleport = createScrollArea("Teleport", 1000)

-- Menu Teleport
local teleportTitle = createPageTitle("Teleport", 50, ScrollTeleport)

-- register page
pages["Teleport"] = ScrollTeleport
if teleportBtn then
    teleportBtn.MouseButton1Click:Connect(function()
        showOnly(ScrollTeleport)
    end)
end

---- scroll area Fruits
local ScrollFruits = createScrollArea("Fruits", 1000)

-- Menu Fruits
local fruitsTitle = createPageTitle("Fruits", 50, ScrollFruits)

-- register page
pages["Fruits"] = ScrollFruits
if fruitsBtn then
    fruitsBtn.MouseButton1Click:Connect(function()
        showOnly(ScrollFruits)
    end)
end

---- scroll area Shop
local ScrollShop = createScrollArea("Shop", 1000)

----Menu Shop
local shopTitle = createPageTitle("Shop", 50, ScrollShop)

-- register page
pages["Shop"] = ScrollShop
if shopBtn then
    shopBtn.MouseButton1Click:Connect(function()
        showOnly(ScrollShop)
    end)
end

---- scroll area Setting
local ScrollSetting = createScrollArea("Setting", 1000)

-- Menu Setting
local settingTitle = createPageTitle("Setting", 50, ScrollSetting)

-- register page
pages["Setting"] = ScrollSetting
if settingBtn then
    settingBtn.MouseButton1Click:Connect(function()
        showOnly(ScrollSetting)
    end)
end

-- start with no page shown
for _, v in pairs(pages) do
    if v then
        v.Visible = false
    end
end
showOnly(ScrollDiscord)
pageHeader.Text = "discord.gg/Nfh5Sczyqz"
        pageHeader.FontFace = Font.new(
         "rbxasset://fonts/families/BuilderSans.json",
          Enum.FontWeight.ExtraBold,
          Enum.FontStyle.Normal
          )
        adjustTextSize(pageHeader, 20)
        pageHeader.Localize = false
