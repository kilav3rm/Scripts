local NotificationTable = {};

local NotificationFolder = Instance.new("Folder");

NotificationTable.CreateNotification = function(TitleData, Text, Image)
	
	if getgenv then
		if (game:GetService("CoreGui"):FindFirstChild("NotificationFolder")) then
			NotificationFolder = game:GetService("CoreGui"):FindFirstChild("NotificationFolder");
		else
			NotificationFolder.Name = "NotificationFolder"
			NotificationFolder.Parent = game:GetService("CoreGui");
		end
	else
		if (game:GetService("Players").LocalPlayer.PlayerGui:FindFirstChild("NotificationFolder")) then
			NotificationFolder = game:GetService("Players").LocalPlayer.PlayerGui:FindFirstChild("NotificationFolder");
		else
			NotificationFolder.Name = "NotificationFolder"
			NotificationFolder.Parent = game:GetService("Players").LocalPlayer.PlayerGui;
		end
	end
	
	local Notification = Instance.new("ScreenGui")
	local _Template = Instance.new("Frame")
	local Icon = Instance.new("ImageLabel")
	local UIAspectRatioConstraint = Instance.new("UIAspectRatioConstraint")
	local Title = Instance.new("TextLabel")
	local TextLabel = Instance.new("TextLabel")
	local UICorner = Instance.new("UICorner")
	local Frame = Instance.new("Frame")
	local UIGradient = Instance.new("UIGradient")


	Notification.Name = "Notification"
	Notification.Parent = NotificationFolder
	Notification.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
	Notification.Enabled = true;

	_Template.Name = "_Template"
	_Template.Parent = Notification
	_Template.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
	_Template.BackgroundTransparency = 0.050
	_Template.BorderColor3 = Color3.fromRGB(255, 255, 255)
	_Template.Position = UDim2.new(0.713929176, 0, 0.587826073, 0)
	_Template.Size = UDim2.new(0, 270, 0, 64)
	_Template.ZIndex = 9

	Icon.Name = "Icon"
	Icon.Parent = _Template
	Icon.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Icon.BackgroundTransparency = 1.000
	Icon.Position = UDim2.new(0.0277603213, 0, 0.182097465, 0)
	Icon.Size = UDim2.new(0, 40, 0, 40)
	Icon.Image = Image

	UIAspectRatioConstraint.Parent = Icon

	Title.Name = "Title"
	Title.Parent = _Template
	Title.BackgroundColor3 = Color3.fromRGB(200, 200, 200)
	Title.BackgroundTransparency = 1.000
	Title.Position = UDim2.new(0, 63, 0, 2)
	Title.Size = UDim2.new(0, 129, 0, 21)
	Title.Font = Enum.Font.SourceSansBold
	Title.Text = TitleData
	Title.TextColor3 = Color3.fromRGB(240, 240, 240)
	Title.TextScaled = true
	Title.TextSize = 14.000
	Title.TextWrapped = true
	Title.TextXAlignment = Enum.TextXAlignment.Left

	TextLabel.Parent = _Template
	TextLabel.BackgroundColor3 = Color3.fromRGB(90, 90, 90)
	TextLabel.BackgroundTransparency = 1.000
	TextLabel.Position = UDim2.new(0, 63, 0, 23)
	TextLabel.Size = UDim2.new(0, 178, 0, 35)
	TextLabel.Font = Enum.Font.SourceSans
	TextLabel.Text = Text
	TextLabel.TextColor3 = Color3.fromRGB(200, 200, 200)
	TextLabel.TextScaled = true
	TextLabel.TextSize = 14.000
	TextLabel.TextWrapped = true
	TextLabel.TextXAlignment = Enum.TextXAlignment.Left
	TextLabel.TextYAlignment = Enum.TextYAlignment.Top

	UICorner.Parent = _Template

	Frame.Parent = _Template
	Frame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Frame.BorderSizePixel = 0
	Frame.Position = UDim2.new(0.0148148146, 0, 0.9375, 0)
	Frame.Size = UDim2.new(0, 263, 0, 2)

	UIGradient.Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(255, 8, 231)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(64, 0, 255))}
	UIGradient.Parent = Frame
	
	return _Template;
end


NotificationFolder.ChildRemoved:Connect(function()
	local TweenService = game:GetService("TweenService");

	local TweenInfData = TweenInfo.new(.25);
	for _, NotificationObject in next, NotificationFolder:GetChildren() do
		local Notification = NotificationObject["_Template"];
		
		TweenService:Create(Notification, TweenInfData, {
			Position = UDim2.new(1, -280, 1, Notification.Position.Y.Offset + 68 + 1);
		}):Play();
	end

end)

NotificationTable.InsertNotification = function(Notification)

	local TweenService = game:GetService("TweenService");
	
	local ShowPosition = UDim2.new(1, -280, 1, -70 * #NotificationFolder:GetChildren() - 1);
	local HidePosition = UDim2.new(1, 70, 1, -70);
	
	Notification.Position = HidePosition;
	Notification.Visible = true;
	
	local TweenInfData = TweenInfo.new(0.4);
	TweenService:Create(Notification, TweenInfData, {
		Position = ShowPosition
	}):Play();
	wait(TweenInfData.Time);
	wait(4)
	TweenService:Create(Notification, TweenInfData, {
		Position = HidePosition
	}):Play();
	wait(TweenInfData.Time);
	
	Notification.Parent:Destroy();
end

NotificationTable.Notify = function(...)
    	local Args = {...};
    
    	assert(#Args < 4, "Error: Too many arguments for Notify | Expected 3");
    
    	for Index,Argument in next, Args do
    		Args[Index] = tostring(Argument);
    	end
    	
    	local NotifFrame = NotificationTable.CreateNotification(Args[1], Args[2], Args[3]);
    	
    	NotificationTable.InsertNotification(NotifFrame);
end

return NotificationTable;
