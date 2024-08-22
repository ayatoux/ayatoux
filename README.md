-- Create the GUI
local gui = Instance.new("ScreenGui")
gui.Parent = game.Players.LocalPlayer.PlayerGui

local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 330, 0, 100)
frame.Position = UDim2.new(0, 10, 0, 10)
frame.BackgroundColor3 = Color3.new(1, 1, 1)
frame.Parent = gui

local button1 = Instance.new("TextButton")
button1.Size = UDim2.new(0, 100, 0, 50)
button1.Position = UDim2.new(0, 10, 0, 10)
button1.Text = "Dough Spike"
button1.BackgroundColor3 = Color3.new(1, 1, 1)
button1.Parent = frame

local button2 = Instance.new("TextButton")
button2.Size = UDim2.new(0, 100, 0, 50)
button2.Position = UDim2.new(0, 110, 0, 10)
button2.Text = "Dough Punch"
button2.BackgroundColor3 = Color3.new(1, 1, 1)
button2.Parent = frame

local button3 = Instance.new("TextButton")
button3.Size = UDim2.new(0, 100, 0, 50)
button3.Position = UDim2.new(0, 210, 0, 10)
button3.Text = "Level Up"
button3.BackgroundColor3 = Color3.new(1, 1, 1)
button3.Parent = frame

local button4 = Instance.new("TextButton")
button4.Size = UDim2.new(0, 100, 0, 50)
button4.Position = UDim2.new(0, 310, 0, 10)
button4.Text = "Geppo Book"
button4.BackgroundColor3 = Color3.new(1, 1, 1)
button4.Parent = frame

-- Create a variable to store the current state of each button
local button1State = false
local button2State = false
local button3State = false

-- Function to toggle button state
local function toggleButton(button, state)
    if state then
        button.BackgroundColor3 = Color3.new(0, 1, 0) -- Green
    else
        button.BackgroundColor3 = Color3.new(1, 1, 1) -- White
    end
end

-- Button 1 click event
button1.Activated:Connect(function()
    button1State = not button1State
    toggleButton(button1, button1State)
end)

-- Button 2 click event
button2.Activated:Connect(function()
    button2State = not button2State
    toggleButton(button2, button2State)
end)

-- Button 3 click event
button3.Activated:Connect(function()
    button3State = not button3State
    toggleButton(button3, button3State)
    
    if button3State then
        -- Start looping the level up function
        while button3State do
local args = {
    [1] = false
}

game:GetService("ReplicatedStorage").QuestResult:FireServer(unpack(args))
            wait() -- adjust the delay as needed
        end
    end
end)

-- Button 4 click event
button4.Activated:Connect(function()
    for i, v in pairs(workspace:GetDescendants()) do
        if v.Name == "geppoBook" and v:FindFirstChild("ClickDetector") then
            fireclickdetector(v.ClickDetector, 1)
        end
    end
end)

-- UserInputService to detect screen taps
local userInputService = game:GetService("UserInputService")

-- Function to run when screen is tapped
local function onTap()
    if button1State then
        local args = {
            [1] = "Dough",
            [2] = "Dough spikes",
            [3] = {}
        }
        game:GetService("ReplicatedStorage").remotes.skill:FireServer(unpack(args))
    elseif button2State then
        local args = {
            [1] = "Dough",
            [2] = "Dual dough punch",
            [3] = {}
        }
        game:GetService("ReplicatedStorage").remotes.skill:FireServer(unpack(args))
    end
end

-- Listen for screen taps
userInputService.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.Touch or input.UserInputType == Enum.UserInputType.MouseButton1 then
        onTap()
    end
end)
