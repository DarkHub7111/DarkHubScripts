-- // // // UI Library Loading // // // --
local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
local SaveManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/SaveManager.lua"))()
local InterfaceManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/InterfaceManager.lua"))()

Fluent:Notify({
    Title = "executed ",
    Content = "executed successfully .",
    Duration = 5
})

local Window = Fluent:CreateWindow({
    Title = "Horse RaceðŸŽ",
    SubTitle = "https://www.youtube.com/@Dark.Hub711",
    TabWidth = 160,
    Size = UDim2.fromOffset(580, 460),
    Theme = "Darker",
    MinimizeKey = Enum.KeyCode.LeftControl 
})

local Tabs = {
    Main = Window:AddTab({ Title = "Main", Icon = "home" })
}

local Options = Fluent.Options

-- // Auto Train // --
local function getTreadmillBasedOnPower(currentPower, world)
    if world == 1 then
        if currentPower >= 5000000000 then
            return "Treadmill_1_12"
        elseif currentPower >= 1500000000 then
            return "Treadmill_1_11"
        elseif currentPower >= 300000000 then
            return "Treadmill_1_10"
        elseif currentPower >= 50000000 then
            return "Treadmill_1_9"
        elseif currentPower >= 15000000 then
            return "Treadmill_1_8"
        elseif currentPower >= 4000000 then
            return "Treadmill_1_7"
        elseif currentPower >= 1000000 then
            return "Treadmill_1_6"
        elseif currentPower >= 400000 then
            return "Treadmill_1_5"
        elseif currentPower >= 35000 then
            return "Treadmill_1_4"
        elseif currentPower >= 5000 then
            return "Treadmill_1_3"
        elseif currentPower >= 1000 then
            return "Treadmill_1_2"
        else
            return "Treadmill_1_1"
        end
    elseif world == 2 then
        if currentPower >= 68000000000000 then
            return "Treadmill_2_12"
        elseif currentPower >= 31000000000000 then
            return "Treadmill_2_11"
        elseif currentPower >= 14000000000000 then
            return "Treadmill_2_10"
        elseif currentPower >= 6400000000000 then
            return "Treadmill_2_9"
        elseif currentPower >= 2900000000000 then
            return "Treadmill_2_8"
        elseif currentPower >= 1200000000000 then
            return "Treadmill_2_7"
        elseif currentPower >= 570000000000 then
            return "Treadmill_2_6"
        elseif currentPower >= 260000000000 then
            return "Treadmill_2_5"
        elseif currentPower >= 120000000000 then
            return "Treadmill_2_4"
        elseif currentPower >= 53000000000 then
            return "Treadmill_2_3"
        elseif currentPower >= 24000000000 then
            return "Treadmill_2_2"
        else
            return "Treadmill_2_1"
        end
    elseif world == 3 then
        if currentPower >= 280000000000000 then
            return "Treadmill_3_12"
        elseif currentPower >= 140000000000000 then
            return "Treadmill_3_11"
        elseif currentPower >= 72000000000000 then
            return "Treadmill_3_10"
        elseif currentPower >= 36000000000000 then
            return "Treadmill_3_9"
        elseif currentPower >= 18000000000000 then
            return "Treadmill_3_8"
        elseif currentPower >= 8800000000000 then
            return "Treadmill_3_7"
        elseif currentPower >= 4400000000000 then
            return "Treadmill_3_6"
        elseif currentPower >= 2200000000000 then
            return "Treadmill_3_5"
        elseif currentPower >= 1100000000000 then
            return "Treadmill_3_4"
        elseif currentPower >= 560000000000 then
            return "Treadmill_3_3"
        elseif currentPower >= 280000000000 then
            return "Treadmill_3_2"
        else
            return "Treadmill_3_1"
        end
    elseif world == 4 then
        if currentPower >= 1100000000000000000 then
            return "Treadmill_4_12"
        elseif currentPower >= 560000000000000000 then
            return "Treadmill_4_11"
        elseif currentPower >= 280000000000000000 then
            return "Treadmill_4_10"
        elseif currentPower >= 140000000000000000 then
            return "Treadmill_4_9"
        elseif currentPower >= 70000000000000000 then
            return "Treadmill_4_8"
        elseif currentPower >= 35000000000000000 then
            return "Treadmill_4_7"
        elseif currentPower >= 17500000000000000 then
            return "Treadmill_4_6"
        elseif currentPower >= 8750000000000000 then
            return "Treadmill_4_5"
        elseif currentPower >= 4375000000000000 then
            return "Treadmill_4_4"
        elseif currentPower >= 2187500000000000 then
            return "Treadmill_4_3"
        elseif currentPower >= 1093750000000000 then
            return "Treadmill_4_2"
        else
            return "Treadmill_4_1"
        end
    else
        return "No Treadmill"  -- Caso o mundo não seja identificado
    end
end

local function getCurrentPower()
    local player = game.Players.LocalPlayer
    local leaderstats = player:WaitForChild("leaderstats")
    local powerStat = leaderstats:WaitForChild("\226\154\161\239\184\143Power")  
    return tonumber(powerStat.Value) 
end

local function getWorldByPower(currentPower)
    if currentPower >= 5000000000 then
        return 1  -- Mundo 1
    elseif currentPower >= 11000000000000 then
        return 2  -- Mundo 2
    elseif currentPower >= 140000000000000 then
        return 3  -- Mundo 3
    elseif currentPower >= 560000000000000000 then
        return 4  -- Mundo 4
    else
        return 1  -- Caso o poder não se encaixe, por padrão, é Mundo 1
    end
end

local function startTraining(treadmill)
    game:GetService("ReplicatedStorage"):WaitForChild("Packages"):WaitForChild("_Index"):WaitForChild("sleitnick_knit@1.5.1"):WaitForChild("knit"):WaitForChild("Services"):WaitForChild("TrainService"):WaitForChild("RE"):WaitForChild("RunTrain"):FireServer(treadmill)
end

local AutoTrainEnabled = false
local AutoTrainrunning = false

local function startAutoTrain()
    if not AutoTrainEnabled or AutoTrainrunning then
        return  
    end

    AutoTrainrunning = true 

    while AutoTrainEnabled do
        local currentPower = getCurrentPower()
        local world = getWorldByPower(currentPower)  -- Identifica o mundo
        local bestTreadmill = getTreadmillBasedOnPower(currentPower, world)

        startTraining(bestTreadmill)

        task.wait(0.1)  
    end

    AutoTrainrunning = false  
end

do
-- // AutoTrain UI // --
local AutoTrainToggle = Tabs.Main:AddToggle("Auto Train", {
    Title = "Auto Train",
    Default = false,
    Callback = function(Value)
        AutoTrainEnabled = Value
        if Value and not AutoTrainrunning then
            startAutoTrain()  
        elseif not Value then
            AutoTrainEnabled = false 
        end
    end
})
end

local InfinitePotionEnabled = false

local function InfinitePotionLoop()
    while InfinitePotionEnabled do
        game:GetService("ReplicatedStorage").Packages._Index["sleitnick_knit@1.5.1"].knit.Services.ChestService.RF.ClaimDailyChest:InvokeServer()
        task.wait() -- Pequena pausa para evitar travamento
    end
end

-- Criando o Toggle na Fluent UI
local InfinitePotionToggle = Tabs.Main:AddToggle("Infinite Potion", {
    Title = "Infinite Potion + King Slime",
    Default = false,
    Callback = function(Value)
        InfinitePotionEnabled = Value
        if Value then
            InfinitePotionLoop() -- Inicia o loop se ativado
        else
            -- Para o loop quando desativado
            InfinitePotionEnabled = false
        end
    end
})

-- Notificando o usuÃ¡rio que o Toggle estÃ¡ pronto
Fluent:Notify({
    Title = "Infinite Potion Toggle",
    Content = "O botÃ£o de Infinite Potion + King Slime foi ativado!",
    Duration = 5
})

local VirtualUser = game:GetService("VirtualUser")
local Players = game:GetService("Players")

Players.LocalPlayer.Idled:Connect(function()
    VirtualUser:CaptureController()
    VirtualUser:ClickButton2(Vector2.new())
end)

Fluent:Notify({
    Title = "Anti-AFK",
    Content = "Anti-AFK ativado com sucesso!",
    Duration = 5
})

print("Anti-AFK ativado!")

-- CriaÃ§Ã£o da aba de Teleporte
local TeleportTab = Window:AddTab({
    Title = "Teleport",
    Icon = "map"
})

-- FunÃ§Ã£o para teleportar para o mundo especÃ­fico
local function teleportToWorld(worldName)
    local args

    -- Definir os argumentos conforme o mundo escolhido
    if worldName == "World 2" then
        args = { [1] = "Area_2" }
        print("Preparando para teleportar para World 2...") -- Personalize a mensagem se necessÃ¡rio
    elseif worldName == "World 3" then
        args = { [1] = "Area_3" }
        print("Preparando para teleportar para World 3...") -- Personalize a mensagem se necessÃ¡rio
    elseif worldName == "World 4" then
        args = { [1] = "Area_4" }
        print("Preparando para teleportar para World 4...") -- Personalize a mensagem se necessÃ¡rio
    end

    -- Primeiro, fazer o rejoin
    game:GetService("TeleportService"):Teleport(game.PlaceId, game.Players.LocalPlayer)

    -- ApÃ³s o rejoin, teleportar para a Ã¡rea especÃ­fica
    game:GetService("ReplicatedStorage"):WaitForChild("Packages"):WaitForChild("_Index"):WaitForChild("sleitnick_knit@1.5.1"):WaitForChild("knit"):WaitForChild("Services"):WaitForChild("AreaService"):WaitForChild("RE"):WaitForChild("UpdatePlayerCurrentArea"):FireServer(unpack(args))
end

-- Adicionando botÃµes para cada mundo na aba de Teleporte
TeleportTab:AddButton({
    Title = "World 2",
    Callback = function()
        teleportToWorld("World 2")
    end
})

TeleportTab:AddButton({
    Title = "World 3",
    Callback = function()
        teleportToWorld("World 3")
    end
})

TeleportTab:AddButton({
    Title = "World 4",
    Callback = function()
        teleportToWorld("World 4")
    end
})

-- Adicionando o parágrafo
Tabs.Main:AddParagraph({
    Title = "Auto Race", 
    Content = 'Click on "Auto race" and start the race!' 
})

local AutoRaceEnabled = false

-- Lista de mundos disponÃ­veis
local worlds = {
    ["Fruit World"] = "Area_Fruit",
    ["World 1"] = "Area_1",
    ["World 2"] = "Area_2",
    ["World 3"] = "Area_3",
    ["World 4"] = "Area_4"
}

local function startAutoRace()
    while AutoRaceEnabled do
        local args = {[1] = SelectedWorld}

        game:GetService("ReplicatedStorage")
            :WaitForChild("Packages")
            :WaitForChild("_Index")
            :WaitForChild("sleitnick_knit@1.5.1")
            :WaitForChild("knit")
            :WaitForChild("Services")
            :WaitForChild("AutoService")
            :WaitForChild("RE")
            :WaitForChild("AutoFightStart")
            :FireServer(unpack(args))

        print("Auto Race ativado para:", SelectedWorld) -- Teste no Console
        task.wait(5) -- Tempo de espera antes de ativar novamente
    end
end

Tabs.Main:AddButton({ Title = "Auto Race", Callback = function() 
loadstring(game:HttpGet('https://pastebin.com/raw/Ncq51Xjr'))();
 end })
-- Variável para controlar o estado do Auto Rebirth
local AutoRebirthEnabled = false
local AutoRebirthRunning = false

-- Definindo a variável para habilitar/desabilitar o Auto Rebirth
local AutoRebirthEnabled = false
local AutoRebirthRunning = false

-- Função que inicia o Auto Rebirth
local function startAutoRebirth()
    while AutoRebirthEnabled do
        -- Chamando o serviço de Rebirth no ReplicatedStorage para realizar o Rebirth
        game:GetService("ReplicatedStorage"):WaitForChild("Packages"):WaitForChild("_Index"):WaitForChild("sleitnick_knit@1.5.1"):WaitForChild("knit"):WaitForChild("Services"):WaitForChild("RebirthService"):WaitForChild("RF"):WaitForChild("Rebirth"):InvokeServer()
        
        -- Espera de 5 segundos antes de realizar outro Rebirth
        task.wait(5)
    end
end

-- Adicionando o toggle no menu principal para controlar o Auto Rebirth
Tabs.Main:AddToggle("Auto Rebirth", {
    Title = "Auto Rebirth",          
    Default = false,                 
    Callback = function(Value)
        AutoRebirthEnabled = Value    

        if Value and not AutoRebirthRunning then
            AutoRebirthRunning = true
            startAutoRebirth()  -- Inicia o Auto Rebirth
        elseif not Value then
            AutoRebirthEnabled = false  -- Desliga o Auto Rebirth
        end
    end
})
-- Criando uma nova aba "Misc"
local MiscTab = Window:AddTab({
    Title = "Misc",  -- Título da nova aba
    Icon = "box"     -- Ícone associado à aba
})
-- Variáveis para os toggles
local AutoCrate1Enabled = false
local AutoCrate2Enabled = false
local EggGhostClaimEnabled = false

-- Função para abrir a Crate 1 em loop
local function autoOpenCrate1()
    while AutoCrate1Enabled do
        local args = { [1] = "Crate_1" }
        game:GetService("ReplicatedStorage"):WaitForChild("Packages"):WaitForChild("_Index")
            :WaitForChild("sleitnick_knit@1.5.1").knit.Services.ItemCrateService.RE.UnboxCrate:FireServer(unpack(args))
        task.wait(1) -- Espera 1 segundo para evitar spam
    end
end

-- Função para abrir a Crate 2 em loop
local function autoOpenCrate2()
    while AutoCrate2Enabled do
        local args = { [1] = "Crate_2" }
        game:GetService("ReplicatedStorage"):WaitForChild("Packages"):WaitForChild("_Index")
            :WaitForChild("sleitnick_knit@1.5.1").knit.Services.ItemCrateService.RE.UnboxCrate:FireServer(unpack(args))
        task.wait(1) -- Espera 1 segundo para evitar spam
    end
end

-- Função para auto claim do Egg Ghost
local function autoClaimEggGhost()
    while EggGhostClaimEnabled do
        game:GetService("ReplicatedStorage"):WaitForChild("Packages"):WaitForChild("_Index")
            :WaitForChild("sleitnick_knit@1.5.1").knit.Services.OnlineRewardService.RF.ClaimOnlineQuestReward:InvokeServer()
        task.wait(5) -- Espera 5 segundos para evitar spam
    end
end

-- Criando toggles no MiscTab
MiscTab:AddToggle("AutoCrate1", {
    Title = "Auto Crate 1",
    Default = false,
    Callback = function(Value)
        AutoCrate1Enabled = Value
        if Value then
            autoOpenCrate1()
        end
    end
})

MiscTab:AddToggle("AutoCrate2", {
    Title = "Auto Crate 2",
    Default = false,
    Callback = function(Value)
        AutoCrate2Enabled = Value
        if Value then
            autoOpenCrate2()
        end
    end
})

MiscTab:AddToggle("AutoClaimEggGhost", {
    Title = "Auto Claim Egg Ghost",
    Default = false,
    Callback = function(Value)
        EggGhostClaimEnabled = Value
        if Value then
            autoClaimEggGhost()
        end
    end
})
local GiftsClaimEnabled = false  -- Variável para controlar o estado

MiscTab:AddToggle("Auto Claim Gifts", {
    Title = "Auto Claim Gifts",
    Default = false,
    Callback = function(Value)
        GiftsClaimEnabled = Value

        if GiftsClaimEnabled then
            task.spawn(function()
                while GiftsClaimEnabled do
                    for i = 1, 12 do  -- Supondo que existam 12 presentes
                        local args = { [1] = i }
                        game:GetService("ReplicatedStorage"):WaitForChild("Packages"):WaitForChild("_Index"):WaitForChild("sleitnick_knit@1.5.1"):WaitForChild("knit"):WaitForChild("Services"):WaitForChild("OnlineRewardService"):WaitForChild("RE"):WaitForChild("ClaimOnlineReward"):FireServer(unpack(args))
                        task.wait(1) -- Pequena espera entre os claims
                    end
                    task.wait(5) -- Tempo de espera antes de tentar novamente
                end
            end)
        end
    end
})
-- Criação da aba "Pet"
local PetTab = Window:AddTab({
    Title = "Pet",  -- Título da aba
    Icon = "pets"   -- Ícone associado à aba
})

-- Botão "Equipe Best Pet"
PetTab:AddButton({
    Title = "Equipe Best Pet",  -- Título do botão
    Callback = function()
        game:GetService("ReplicatedStorage"):WaitForChild("Packages"):WaitForChild("_Index"):WaitForChild("sleitnick_knit@1.5.1"):WaitForChild("knit"):WaitForChild("Services"):WaitForChild("PetService"):WaitForChild("RE"):WaitForChild("EquipBestPets"):FireServer()
    end
})
-- Botão "Craft Pet"
PetTab:AddButton({
    Title = "Craft Pet",  -- Título do botão
    Callback = function()
       game:GetService("ReplicatedStorage"):WaitForChild("Packages"):WaitForChild("_Index"):WaitForChild("sleitnick_knit@1.5.1"):WaitForChild("knit"):WaitForChild("Services"):WaitForChild("PetService"):WaitForChild("RE"):WaitForChild("EnlargeAllPets"):FireServer()
    end
})


-- Notificação de sucesso
Fluent:Notify({
    Title = "Pet",
    Content = "A aba Pet foi criada com sucesso!",
    Duration = 5
})
local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()

local Window = Fluent:CreateWindow({
    Title = "Select World Example",
    Size = UDim2.fromOffset(580, 460),
    Theme = "Darker",
})

local Tabs = {
    Main = Window:AddTab({ Title = "Main", Icon = "home" })
}

Tabs.Main:AddDropdown("Select World", {
    Values = {"World 1", "World 2", "World 3", "World 4"},
    Default = 1,
    Callback = function(value)
        if value == "World 1" then
            local args = { [1] = "Area_1" }
            game:GetService("ReplicatedStorage"):WaitForChild("Packages"):WaitForChild("_Index"):WaitForChild("sleitnick_knit@1.5.1"):WaitForChild("knit"):WaitForChild("Services"):WaitForChild("AreaService"):WaitForChild("RE"):WaitForChild("UpdatePlayerCurrentArea"):FireServer(unpack(args))
        
        elseif value == "World 2" then
            local args = { [1] = "Area_2" }
            game:GetService("ReplicatedStorage"):WaitForChild("Packages"):WaitForChild("_Index"):WaitForChild("sleitnick_knit@1.5.1"):WaitForChild("knit"):WaitForChild("Services"):WaitForChild("AreaService"):WaitForChild("RE"):WaitForChild("UpdatePlayerCurrentArea"):FireServer(unpack(args))
        
        elseif value == "World 3" then
            local args = { [1] = "Area_3" }
            game:GetService("ReplicatedStorage"):WaitForChild("Packages"):WaitForChild("_Index"):WaitForChild("sleitnick_knit@1.5.1"):WaitForChild("knit"):WaitForChild("Services"):WaitForChild("AreaService"):WaitForChild("RE"):WaitForChild("UpdatePlayerCurrentArea"):FireServer(unpack(args))
        
        elseif value == "World 4" then
            local args = { [1] = "Area_4" }
            game:GetService("ReplicatedStorage"):WaitForChild("Packages"):WaitForChild("_Index"):WaitForChild("sleitnick_knit@1.5.1"):WaitForChild("knit"):WaitForChild("Services"):WaitForChild("AreaService"):WaitForChild("RE"):WaitForChild("UpdatePlayerCurrentArea"):FireServer(unpack(args))
        end
    end
})
local screenGui = Instance.new("ScreenGui")
screenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

local imageButton = Instance.new("ImageButton")
imageButton.Size = UDim2.new(0, 50, 0, 50)  -- Set size to 100x100 pixels
imageButton.Position = UDim2.new(1, -110, 0, 10)  -- Set position
imageButton.BackgroundTransparency = 1  -- Make the background transparent
imageButton.Image = "rbxassetid://127146707195866"  -- Your image ID
imageButton.Parent = screenGui
local uiStroke = Instance.new("UIStroke")
uiStroke.Parent = imageButton
uiStroke.Thickness = 4  -- Adjust the thickness of the border
uiStroke.Color = Color3.fromRGB(255, 105, 180)  -- Pink color
uiStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
uiStroke.Transparency = 0
    
    local corner = Instance.new("UICorner")
    corner.Parent = imageButton
    
    imageButton.MouseButton1Click:Connect(function()
        if WindowHidden == false then
            Window:Minimize()
            WindowHidden = true
        else
            Window:Minimize()
            WindowHidden = false
        end
    end)
    
    local dragging = false
    local dragInput
    local startPos
    local startSize
    
    imageButton.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 then
            dragging = true
            startPos = input.Position
            startSize = imageButton.Position
    
            input.Changed:Connect(function()
                if input.UserInputState == Enum.UserInputState.End then
                    dragging = false
                end
            end)
        end
    end)
    
    imageButton.InputChanged:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseMovement and dragging then
            local delta = input.Position - startPos
            imageButton.Position = UDim2.new(startSize.X.Scale, startSize.X.Offset + delta.X, startSize.Y.Scale, startSize.Y.Offset + delta.Y)
        end
    end)
SaveManager:SetLibrary(Fluent)
InterfaceManager:SetLibrary(Fluent)
SaveManager:IgnoreThemeSettings()
SaveManager:SetIgnoreIndexes({})
InterfaceManager:SetFolder("FluentScriptHub")
SaveManager:SetFolder("FluentScriptHub/specific-game")

InterfaceManager:BuildInterfaceSection(Tabs.Settings)
SaveManager:BuildConfigSection(Tabs.Settings)


Window:SelectTab(1)

Fluent:Notify({
    Title = "Horserace",
    Content = "The script has been loaded.",
    Duration = 8
})


SaveManager:LoadAutoloadConfig()
