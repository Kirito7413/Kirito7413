-- Serviço necessário
local UserInputService = game:GetService("UserInputService")

-- Variáveis
local isRunning = false
local VirtualButton

-- Função para criar botão virtual
local function createVirtualButton()
    VirtualButton = Instance.new("TextButton")
    VirtualButton.Size = UDim2.new(0, 100, 0, 50)
    VirtualButton.Position = UDim2.new(0.5, -50, 0.9, -25)
    VirtualButton.Text = "Iniciar"
    VirtualButton.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui"):WaitForChild("ScreenGui")

    VirtualButton.MouseButton1Click:Connect(function()
        if not isRunning then
            -- Pressiona a tecla "]" uma vez
            UserInputService:SendKeyEvent(true, Enum.KeyCode.RightBracket, false, game)
            wait(0.1)
            UserInputService:SendKeyEvent(false, Enum.KeyCode.RightBracket, false, game)
            wait(0.1)
            -- Muda o estado para iniciar a repetição
            isRunning = true
            VirtualButton.Text = "Parar"
        else
            -- Para a repetição
            isRunning = false
            VirtualButton.Text = "Iniciar"
        end
    end)
end

-- Função para enviar teclas repetidamente
local function sendKeys()
    while isRunning do
        UserInputService:SendKeyEvent(true, Enum.KeyCode.S, false, game)
        wait(0.1)
        UserInputService:SendKeyEvent(false, Enum.KeyCode.S, false, game)
        wait(0.1)

        UserInputService:SendKeyEvent(true, Enum.KeyCode.Return, false, game)
        wait(0.1)
        UserInputService:SendKeyEvent(false, Enum.KeyCode.Return, false, game)
        wait(0.1)
    end
end

-- Inicializa o script após o jogador carregar
game.Players.LocalPlayer.CharacterAdded:Connect(function(character)
    createVirtualButton()

    -- Loop para verificar se deve enviar teclas
    while true do
        if isRunning then
            sendKeys()
        end
        wait(0.1)
    end
end)
