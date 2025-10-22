local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local teleportEvent = ReplicatedStorage:WaitForChild("TeleportPlayerToExecutor")

local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-- Create simple UI for demonstration
local screenGui = Instance.new("ScreenGui", playerGui)
local frame = Instance.new("Frame", screenGui)
frame.Size = UDim2.new(0, 200, 0, 300)
frame.Position = UDim2.new(0, 10, 0.5, -150)
frame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)

local uiListLayout = Instance.new("UIListLayout", frame)

-- Function to add players to the UI list
local function refreshPlayerList()
	for _, targetPlayer in ipairs(Players:GetPlayers()) do
		if targetPlayer ~= player then
			local button = Instance.new("TextButton")
			button.Size = UDim2.new(1, 0, 0, 30)
			button.Text = targetPlayer.Name
			button.Parent = frame
			
			button.MouseButton1Click:Connect(function()
				-- Request server to teleport that player to the executor
				teleportEvent:FireServer(targetPlayer)
			end)
		end
	end
end

-- Initial load
refreshPlayerList()

-- Update when players join/leave
Players.PlayerAdded:Connect(function()
	for _, child in pairs(frame:GetChildren()) do
		if child:IsA("TextButton") then
			child:Destroy()
		end
	end
	refreshPlayerList()
end)

Players.PlayerRemoving:Connect(function()
	for _, child in pairs(frame:GetChildren()) do
		if child:IsA("TextButton") then
			child:Destroy()
		end
	end
	refreshPlayerList()
end)
