local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local RunService = game:GetService("RunService")

local player = Players.LocalPlayer

local gui = Instance.new("ScreenGui")
gui.Name = "UniversalScriptGUI"
gui.ResetOnSpawn = false
gui.Parent = player:WaitForChild("PlayerGui")

local flying = false
local noclip = false
local spinning = false

local flySpeed = 60
local spinSpeed = 5
local walkSpeed = 16

local main = Instance.new("Frame")
main.Name = "Main"
main.Size = UDim2.fromOffset(500, 330)
main.Position = UDim2.fromOffset(20, 20)
main.BackgroundColor3 = Color3.fromRGB(20, 22, 28)
main.BorderSizePixel = 0
main.Parent = gui

-- TÍTULO
local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, -100, 0, 50)
title.Position = UDim2.fromOffset(20, 5)
title.BackgroundTransparency = 1
title.Text = "Universal Script"
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.TextSize = 24
title.Font = Enum.Font.GothamBold
title.TextXAlignment = Enum.TextXAlignment.Left
title.Parent = main

-- BOTÃO MINIMIZAR
local minimizeButton = Instance.new("TextButton")
minimizeButton.Size = UDim2.fromOffset(35, 35)
minimizeButton.Position = UDim2.new(1, -45, 0, 10)
minimizeButton.BackgroundColor3 = Color3.fromRGB(35, 38, 48)
minimizeButton.TextColor3 = Color3.fromRGB(255, 255, 255)
minimizeButton.Text = "−"
minimizeButton.TextSize = 24
minimizeButton.Font = Enum.Font.GothamBold
minimizeButton.Parent = main

-- BOTÃO ABRIR
local openButton = Instance.new("TextButton")
openButton.Size = UDim2.fromOffset(50, 50)
openButton.Position = UDim2.fromOffset(20, 20)
openButton.BackgroundColor3 = Color3.fromRGB(20, 22, 28)
openButton.TextColor3 = Color3.fromRGB(255, 255, 255)
openButton.Text = "+"
openButton.TextSize = 28
openButton.Font = Enum.Font.GothamBold
openButton.Visible = false
openButton.Parent = gui

minimizeButton.MouseButton1Click:Connect(function()
	main.Visible = false
	openButton.Visible = true
end)

openButton.MouseButton1Click:Connect(function()
	main.Visible = true
	openButton.Visible = false
end)

-- ARRASTAR MENU
local dragging = false
local dragStart
local startPos

title.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 then
		dragging = true
		dragStart = input.Position
		startPos = main.Position
	end
end)

UserInputService.InputChanged:Connect(function(input)
	if dragging and input.UserInputType == Enum.UserInputType.MouseMovement then
		local delta = input.Position - dragStart

		main.Position = UDim2.new(
			startPos.X.Scale,
			startPos.X.Offset + delta.X,
			startPos.Y.Scale,
			startPos.Y.Offset + delta.Y
		)
	end
end)

UserInputService.InputEnded:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 then
		dragging = false
	end
end)

-- FUNÇÃO BOTÃO
local function createButton(text, x, y)
	local button = Instance.new("TextButton")
	button.Size = UDim2.fromOffset(140, 42)
	button.Position = UDim2.fromOffset(x, y)
	button.BackgroundColor3 = Color3.fromRGB(35, 38, 48)
	button.TextColor3 = Color3.fromRGB(255, 255, 255)
	button.Text = text
	button.TextSize = 16
	button.Font = Enum.Font.GothamBold
	button.Parent = main

	return button
end

-- BOTÕES
local flyButton = createButton("Fly: OFF", 20, 70)
local noclipButton = createButton("Noclip: OFF", 20, 125)
local spinButton = createButton("Spin: OFF", 20, 180)
local settingsButton = createButton("⚙ Configurações", 20, 235)

-- FUNÇÃO LABEL
local function createLabel(text, x, y)
	local label = Instance.new("TextLabel")
	label.Size = UDim2.fromOffset(140, 20)
	label.Position = UDim2.fromOffset(x, y)
	label.BackgroundTransparency = 1
	label.Text = text
	label.TextColor3 = Color3.fromRGB(180, 180, 180)
	label.TextSize = 14
	label.Font = Enum.Font.Gotham
	label.Parent = main

	return label
end

createLabel("Fly Speed", 180, 55)
createLabel("Spin Speed", 180, 110)
createLabel("Walk Speed", 180, 165)

-- FLY SPEED
local flyBox = Instance.new("TextBox")
flyBox.Size = UDim2.fromOffset(140, 42)
flyBox.Position = UDim2.fromOffset(180, 70)
flyBox.Text = tostring(flySpeed)
flyBox.PlaceholderText = "Fly Speed"
flyBox.ClearTextOnFocus = false
flyBox.BackgroundColor3 = Color3.fromRGB(35, 38, 48)
flyBox.TextColor3 = Color3.fromRGB(255, 255, 255)
flyBox.TextSize = 16
flyBox.Font = Enum.Font.Gotham
flyBox.Parent = main

-- SPIN SPEED
local spinBox = Instance.new("TextBox")
spinBox.Size = UDim2.fromOffset(140, 42)
spinBox.Position = UDim2.fromOffset(180, 125)
spinBox.Text = tostring(spinSpeed)
spinBox.PlaceholderText = "Spin Speed"
spinBox.ClearTextOnFocus = false
spinBox.BackgroundColor3 = Color3.fromRGB(35, 38, 48)
spinBox.TextColor3 = Color3.fromRGB(255, 255, 255)
spinBox.TextSize = 16
spinBox.Font = Enum.Font.Gotham
spinBox.Parent = main

-- WALK SPEED
local speedBox = Instance.new("TextBox")
speedBox.Size = UDim2.fromOffset(140, 42)
speedBox.Position = UDim2.fromOffset(180, 180)
speedBox.Text = tostring(walkSpeed)
speedBox.PlaceholderText = "Walk Speed"
speedBox.ClearTextOnFocus = false
speedBox.BackgroundColor3 = Color3.fromRGB(35, 38, 48)
speedBox.TextColor3 = Color3.fromRGB(255, 255, 255)
speedBox.TextSize = 16
speedBox.Font = Enum.Font.Gotham
speedBox.Parent = main

-- CRÉDITO RAINBOW 🌈
local credits = Instance.new("TextLabel")
credits.Size = UDim2.fromOffset(200, 30)
credits.Position = UDim2.fromOffset(180, 250)
credits.BackgroundTransparency = 1
credits.Text = "⭐ Murixzzzz"
credits.TextColor3 = Color3.fromRGB(255, 0, 0)
credits.TextSize = 16
credits.Font = Enum.Font.GothamBold
credits.Parent = main

task.spawn(function()
	local hue = 0

	while credits.Parent do
		hue = (hue + 0.005) % 1
		credits.TextColor3 = Color3.fromHSV(hue, 1, 1)
		task.wait(0.03)
	end
end)

-- ALTERAR FLY SPEED
flyBox.FocusLost:Connect(function()
	local value = tonumber(flyBox.Text)

	if value then
		flySpeed = value
	else
		flyBox.Text = tostring(flySpeed)
	end
end)

-- ALTERAR SPIN SPEED
spinBox.FocusLost:Connect(function()
	local value = tonumber(spinBox.Text)

	if value then
		spinSpeed = value
	else
		spinBox.Text = tostring(spinSpeed)
	end
end)

-- ALTERAR WALK SPEED
speedBox.FocusLost:Connect(function()
	local value = tonumber(speedBox.Text)

	if value then
		walkSpeed = value

		local character = player.Character

		if character then
			local humanoid = character:FindFirstChildOfClass("Humanoid")

			if humanoid then
				humanoid.WalkSpeed = walkSpeed
			end
		end
	else
		speedBox.Text = tostring(walkSpeed)
	end
end)

-- ANIMAÇÃO DO FLY
local function setFlyAnimation(enabled)
	local character = player.Character
	if not character then return end

	local humanoid = character:FindFirstChildOfClass("Humanoid")
	if not humanoid then return end

	local animate = character:FindFirstChild("Animate")

	if enabled then
		if animate then
			local fall = animate:FindFirstChild("fall")

			if fall then
				fall.Disabled = true
			end
		end

		for _, track in pairs(humanoid:GetPlayingAnimationTracks()) do
			track:Stop(0.15)
		end

		humanoid:ChangeState(Enum.HumanoidStateType.Physics)
	else
		if animate then
			local fall = animate:FindFirstChild("fall")

			if fall then
				fall.Disabled = false
			end
		end

		humanoid:ChangeState(Enum.HumanoidStateType.GettingUp)
	end
end

-- FLY
local function startFly()
	local character = player.Character
	if not character then return end

	local root = character:FindFirstChild("HumanoidRootPart")
	local humanoid = character:FindFirstChildOfClass("Humanoid")

	if not root or not humanoid then return end

	flying = true
	flyButton.Text = "Fly: ON"

	setFlyAnimation(true)

	humanoid.AutoRotate = false
	root.AssemblyLinearVelocity = Vector3.zero
end

local function stopFly()
	flying = false
	flyButton.Text = "Fly: OFF"

	local character = player.Character

	if character then
		local root = character:FindFirstChild("HumanoidRootPart")
		local humanoid = character:FindFirstChildOfClass("Humanoid")

		if root then
			root.AssemblyLinearVelocity = Vector3.zero
		end

		if humanoid then
			humanoid.AutoRotate = true
		end
	end

	setFlyAnimation(false)
end

flyButton.MouseButton1Click:Connect(function()
	if flying then
		stopFly()
	else
		startFly()
	end
end)

-- MOVIMENTO DO FLY
RunService.Heartbeat:Connect(function()
	if not flying then return end
	if not player.Character then return end

	local character = player.Character
	local root = character:FindFirstChild("HumanoidRootPart")
	local humanoid = character:FindFirstChildOfClass("Humanoid")
	local camera = workspace.CurrentCamera

	if not root or not humanoid or not camera then return end

	local direction = Vector3.zero

	if UserInputService:IsKeyDown(Enum.KeyCode.W) then
		direction += camera.CFrame.LookVector
	end

	if UserInputService:IsKeyDown(Enum.KeyCode.S) then
		direction -= camera.CFrame.LookVector
	end

	if UserInputService:IsKeyDown(Enum.KeyCode.A) then
		direction -= camera.CFrame.RightVector
	end

	if UserInputService:IsKeyDown(Enum.KeyCode.D) then
		direction += camera.CFrame.RightVector
	end

	if UserInputService:IsKeyDown(Enum.KeyCode.Space) then
		direction += Vector3.new(0, 1, 0)
	end

	if UserInputService:IsKeyDown(Enum.KeyCode.LeftControl) then
		direction -= Vector3.new(0, 1, 0)
	end

	if direction.Magnitude > 0 then
		direction = direction.Unit * flySpeed
	else
		direction = Vector3.zero
	end

	root.AssemblyLinearVelocity = direction

	local forwardAmount = 0

	if UserInputService:IsKeyDown(Enum.KeyCode.W) then
		forwardAmount = -12
	elseif UserInputService:IsKeyDown(Enum.KeyCode.S) then
		forwardAmount = 12
	end

	local position = root.Position
	local look = camera.CFrame.LookVector
	local flatLook = Vector3.new(look.X, 0, look.Z)

	if flatLook.Magnitude > 0 then
		flatLook = flatLook.Unit

		local target =
			CFrame.lookAt(position, position + flatLook) *
			CFrame.Angles(math.rad(forwardAmount), 0, 0)

		root.CFrame = root.CFrame:Lerp(target, 0.15)
	end
end)

-- NOCLIP
noclipButton.MouseButton1Click:Connect(function()
	noclip = not noclip

	if noclip then
		noclipButton.Text = "Noclip: ON"
	else
		noclipButton.Text = "Noclip: OFF"
	end
end)

RunService.Stepped:Connect(function()
	if noclip and player.Character then

		for _, part in pairs(player.Character:GetDescendants()) do
			if part:IsA("BasePart") then
				part.CanCollide = false
			end
		end
	end
end)

-- SPIN
spinButton.MouseButton1Click:Connect(function()
	spinning = not spinning

	if spinning then
		spinButton.Text = "Spin: ON"
	else
		spinButton.Text = "Spin: OFF"
	end
end)

RunService.Heartbeat:Connect(function()
	if spinning and player.Character then

		local root = player.Character:FindFirstChild("HumanoidRootPart")

		if root then
			root.CFrame = root.CFrame * CFrame.Angles(0, math.rad(spinSpeed), 0)
		end
	end
end)

-- TECLA E PARA FLY
UserInputService.InputBegan:Connect(function(input, processed)

	if processed then return end

	if input.KeyCode == Enum.KeyCode.E then

		if flying then
			stopFly()
		else
			startFly()
		end
	end
end)

-- CONFIGURAÇÕES
settingsButton.MouseButton1Click:Connect(function()

	local settingsGui = Instance.new("Frame")
	settingsGui.Size = UDim2.fromOffset(400, 250)
	settingsGui.Position = UDim2.new(0.5, -200, 0.5, -125)
	settingsGui.BackgroundColor3 = Color3.fromRGB(20, 22, 28)
	settingsGui.BorderSizePixel = 0
	settingsGui.Parent = gui

	local settingsTitle = Instance.new("TextLabel")
	settingsTitle.Size = UDim2.new(1, -60, 0, 50)
	settingsTitle.Position = UDim2.fromOffset(20, 5)
	settingsTitle.BackgroundTransparency = 1
	settingsTitle.Text = "Configurações"
	settingsTitle.TextColor3 = Color3.fromRGB(255, 255, 255)
	settingsTitle.TextSize = 22
	settingsTitle.Font = Enum.Font.GothamBold
	settingsTitle.TextXAlignment = Enum.TextXAlignment.Left
	settingsTitle.Parent = settingsGui

	local closeButton = Instance.new("TextButton")
	closeButton.Size = UDim2.fromOffset(35, 35)
	closeButton.Position = UDim2.new(1, -45, 0, 10)
	closeButton.BackgroundColor3 = Color3.fromRGB(35, 38, 48)
	closeButton.TextColor3 = Color3.fromRGB(255, 255, 255)
	closeButton.Text = "✕"
	closeButton.TextSize = 20
	closeButton.Font = Enum.Font.GothamBold
	closeButton.Parent = settingsGui

	closeButton.MouseButton1Click:Connect(function()
		settingsGui:Destroy()
	end)

	local controls = Instance.new("TextLabel")
	controls.Size = UDim2.new(1, -40, 0, 160)
	controls.Position = UDim2.fromOffset(20, 65)
	controls.BackgroundTransparency = 1
	controls.Text =
		"CONTROLES\n\n" ..
		"E  →  Ativar / desativar Fly\n" ..
		"WASD  →  Movimentar no Fly\n" ..
		"Space  →  Subir\n" ..
		"Ctrl  →  Descer\n\n" ..
		"Fly Speed, Spin Speed e Walk Speed\n" ..
		"podem ser alterados no menu principal."

	controls.TextColor3 = Color3.fromRGB(200, 200, 200)
	controls.TextSize = 15
	controls.Font = Enum.Font.Gotham
	controls.TextXAlignment = Enum.TextXAlignment.Left
	controls.TextYAlignment = Enum.TextYAlignment.Top
	controls.Parent = settingsGui
end)

-- RESET AO RENASCER
player.CharacterAdded:Connect(function(character)

	task.wait(1)

	flying = false
	noclip = false
	spinning = false

	flyButton.Text = "Fly: OFF"
	noclipButton.Text = "Noclip: OFF"
	spinButton.Text = "Spin: OFF"

	local humanoid = character:WaitForChild("Humanoid")
	humanoid.WalkSpeed = walkSpeed
	humanoid.AutoRotate = true
end)
