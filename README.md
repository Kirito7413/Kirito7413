local UserInputService = game:GetService("UserInputService")
local isRunning = false
local VirtualButton

local function createVirtualButton()
    VirtualButton = Instance.new("TextButton")
    VirtualButton.Size = UDim2.new(0, 100, 0, 50)
    VirtualButton.Position = UDim2.new(0.5, -50, 0.9, -25)
    VirtualButton.Text = "Iniciar"
    VirtualButton.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui"):WaitForChild("ScreenGui")

    VirtualButton.MouseButton1Click:Connect(function()
        if not isRunning then
            UserInputService:SendKeyEvent(true, Enum.KeyCode.RightBracket, false, game)
            wait(0.1)
            UserInputService:SendKeyEvent(false, Enum.KeyCode.RightBracket, false, game)
            wait(0.1)
            isRunning = true
            VirtualButton.Text = "Parar"
        else
            isRunning = false
            VirtualButton.Text = "Iniciar"
        end
    end)
end

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

game.Players.LocalPlayer.CharacterAdded:Connect(function(character)
    createVirtualButton()

    while true do
        if isRunning then
            sendKeys()
        end
        wait(0.1)
    end
end)
