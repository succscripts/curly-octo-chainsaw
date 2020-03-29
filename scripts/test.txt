-- Instances:
 
local spookyxrgui = Instance.new("ScreenGui")
local mainframe = Instance.new("Frame")
local Frame = Instance.new("Frame")
local TextLabel = Instance.new("TextLabel")
local adminbutton = Instance.new("TextButton")
local wallwalkbutton = Instance.new("TextButton")
local feposebutton = Instance.new("TextButton")
local penisbutton = Instance.new("TextButton")
local aimbotespbutton = Instance.new("TextButton")
local invisflingbutton = Instance.new("TextButton")
local servercrashbutton = Instance.new("TextButton")
local closebutton = Instance.new("TextButton")
local openbutton = Instance.new("TextButton")
 
--Properties:
 
spookyxrgui.Name = "spookyxrgui"
spookyxrgui.Parent = game.CoreGui
spookyxrgui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
 
mainframe.Name = "mainframe"
mainframe.Parent = spookyxrgui
mainframe.BackgroundColor3 = Color3.fromRGB(26, 26, 26)
mainframe.BorderColor3 = Color3.fromRGB(48, 48, 48)
mainframe.Position = UDim2.new(0.124634862, 0, 0.14158164, 0)
mainframe.Size = UDim2.new(0, 293, 0, 141)
 
Frame.Parent = mainframe
Frame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
Frame.BorderColor3 = Color3.fromRGB(17, 18, 17)
Frame.Size = UDim2.new(0, 293, 0, 18)
 
TextLabel.Parent = mainframe
TextLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
TextLabel.BackgroundTransparency = 1.000
TextLabel.Position = UDim2.new(-0.102389067, 0, -0.105263159, 0)
TextLabel.Size = UDim2.new(0, 200, 0, 50)
TextLabel.Font = Enum.Font.Highway
TextLabel.Text = "SpookyXR's Trolling GUi"
TextLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
TextLabel.TextSize = 14.000
 
adminbutton.Name = "adminbutton"
adminbutton.Parent = mainframe
adminbutton.BackgroundColor3 = Color3.fromRGB(13, 13, 13)
adminbutton.BorderColor3 = Color3.fromRGB(59, 59, 59)
adminbutton.Position = UDim2.new(0.0409556329, 0, 0.184210524, 0)
adminbutton.Size = UDim2.new(0, 84, 0, 31)
adminbutton.Font = Enum.Font.SourceSans
adminbutton.Text = "Infinite Yield"
adminbutton.TextColor3 = Color3.fromRGB(255, 255, 255)
adminbutton.TextSize = 14.000
adminbutton.MouseButton1Down:connect(function()
loadstring(game:HttpGet(('https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source'),true))()
end)
 
wallwalkbutton.Name = "wallwalkbutton"
wallwalkbutton.Parent = mainframe
wallwalkbutton.BackgroundColor3 = Color3.fromRGB(13, 13, 13)
wallwalkbutton.BorderColor3 = Color3.fromRGB(59, 59, 59)
wallwalkbutton.Position = UDim2.new(0.354659677, 0, 0.183136418, 0)
wallwalkbutton.Size = UDim2.new(0, 84, 0, 31)
wallwalkbutton.Font = Enum.Font.SourceSans
wallwalkbutton.Text = "Walk On Walls"
wallwalkbutton.TextColor3 = Color3.fromRGB(255, 255, 255)
wallwalkbutton.TextSize = 14.000
wallwalkbutton.MouseButton1Down:connect(function()
getgenv()["cofiG"] = getgenv()["cofiG"] or {}
local hasToUpdate = true
local alreadyRan = cofiG.gravityController ~= nil
 
local http = game:GetService'HttpService'
local readfile,writefile,fileexists = readfile or syn_io_read,writefile or syn_io_write,isfile or readfile
 
local rawUrl,baseUrl = "https://ixss.keybase.pub/rblx/gravityController/", "https://keybase.pub/ixss/rblx/gravityController/"
 
do
    _G.req = [[
        local require = function(lol)
            lol = "https://raw.githubusercontent.com/msva/lua-htmlparser/master/src/"..lol:gsub("%.","/")..".lua";
            return loadstring(_G.req..game:HttpGet(lol))();
        end;
    ]]
   
    local require = function(lol)
        lol = "https://raw.githubusercontent.com/msva/lua-htmlparser/master/src/"..lol:gsub("%.","/")..".lua";
        return loadstring(_G.req..game:HttpGet(lol))();
    end;
   
    cofiG.htmlparser = cofiG.htmlparser or require"htmlparser"
end
 
do  -- check if exists
if fileexists'gravityController.json' then
local json = readfile'gravityController.json'
if json then
cofiG.gravityController = http:JSONDecode(json)
hasToUpdate = cofiG.gravityController.Version ~= game:HttpGet(rawUrl.."Version.txt")
end
end
game.StarterGui:SetCore("ChatMakeSystemMessage", {
Text = hasToUpdate and "Updating script..." or "Running script!";
Font = Enum.Font.Code;
Color = Color3.fromRGB(255, 60, 60);
FontSize = Enum.FontSize.Size96;  
})
end
 
 
if hasToUpdate then -- update/download
   
    function getScripts()
        local ret = {}
        local text = game:HttpGet(baseUrl, false)
       
        local root = cofiG.htmlparser.parse(text)
        local files = root:select(".file")
       
        for i,v in pairs(files) do
            if string.sub(v.attributes.href, string.len(v.attributes.href)-3) == ".lua" then
                local name = string.sub(v.attributes.href,string.len(baseUrl)+1, string.len(v.attributes.href)-4)
                local script = rawUrl..name..".lua"
                ret[name] = game:HttpGet(script)
            elseif string.sub(v.attributes.href, string.len(v.attributes.href)-3) == ".txt" then
                local name = string.sub(v.attributes.href,string.len(baseUrl)+1, string.len(v.attributes.href)-4)
                local script = rawUrl..name..".txt"
                ret[name] = game:HttpGet(script)
            end
        end
       
        return ret
    end
    cofiG.gravityController = getScripts()
    writefile('gravityController.json', http:JSONEncode(cofiG.gravityController))
    warn('Script updated!')
end
 
local a,b = pcall(loadstring(cofiG.gravityController.Loader))
 
if not a then
error('Loader ', b)
end
 
if not alreadyRan then
game.StarterGui:SetCore("ChatMakeSystemMessage", {
Text = game:HttpGet('https://ixss.keybase.pub/Watermark.txt', true)..", originally made by EgoMoose.";
Font = Enum.Font.Code;
Color = Color3.fromRGB(244, 0, 175);
FontSize = Enum.FontSize.Size96;  
})
end
end)
 
feposebutton.Name = "feposebutton"
feposebutton.Parent = mainframe
feposebutton.BackgroundColor3 = Color3.fromRGB(13, 13, 13)
feposebutton.BorderColor3 = Color3.fromRGB(59, 59, 59)
feposebutton.Position = UDim2.new(0.668941975, 0, 0.177631572, 0)
feposebutton.Size = UDim2.new(0, 84, 0, 31)
feposebutton.Font = Enum.Font.SourceSans
feposebutton.Text = "FE Pose"
feposebutton.TextColor3 = Color3.fromRGB(255, 255, 255)
feposebutton.TextSize = 14.000
feposebutton.MouseButton1Down:connect(function()
-- credit to Zeezy9892 on v3rm
 
local fePosev3 = Instance.new("ScreenGui")
local Menu = Instance.new("Frame")
local Buttons = Instance.new("Frame")
local Swirl = Instance.new("TextButton")
local UIGridLayout = Instance.new("UIGridLayout")
local TPose = Instance.new("TextButton")
local LongArms = Instance.new("TextButton")
local CrazyHats = Instance.new("TextButton")
local Ring = Instance.new("TextButton")
local Orbit = Instance.new("TextButton")
local NoFace = Instance.new("TextButton")
local BlockHead = Instance.new("TextButton")
local NoClothes = Instance.new("TextButton")
local Helicopter = Instance.new("TextButton")
local Sit = Instance.new("TextButton")
local SwirlHats = Instance.new("TextButton")
local Topbar = Instance.new("Frame")
local Close = Instance.new("TextButton")
local Minimize = Instance.new("TextButton")
local Title = Instance.new("TextLabel")
local MinMenu = Instance.new("Frame")
local Close_2 = Instance.new("TextButton")
local Maximize = Instance.new("TextButton")
local Title_2 = Instance.new("TextLabel")
fePosev3.Name = "fePose v3"
fePosev3.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
fePosev3.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
fePosev3.ResetOnSpawn = false
Menu.Name = "Menu"
Menu.Parent = fePosev3
Menu.AnchorPoint = Vector2.new(1, 1)
Menu.BackgroundColor3 = Color3.new(0, 0, 0)
Menu.BorderColor3 = Color3.new(0.0352941, 0.0352941, 0.0352941)
Menu.Position = UDim2.new(1, -10, 1, -115)
Menu.Size = UDim2.new(0, 250, 0, 195)
Buttons.Name = "Buttons"
Buttons.Parent = Menu
Buttons.AnchorPoint = Vector2.new(0.5, 1)
Buttons.BackgroundColor3 = Color3.new(0.0470588, 0.0470588, 0.0470588)
Buttons.BorderColor3 = Color3.new(0, 0, 0)
Buttons.Position = UDim2.new(0.5, 0, 1, 0)
Buttons.Size = UDim2.new(1, 0, 1, -25)
Swirl.Name = "Swirl"
Swirl.Parent = Buttons
Swirl.AnchorPoint = Vector2.new(0.5, 1)
Swirl.BackgroundColor3 = Color3.new(0.121569, 0.121569, 0.121569)
Swirl.BorderColor3 = Color3.new(0, 0, 0)
Swirl.Font = Enum.Font.Arial
Swirl.Text = "Swirl"
Swirl.TextColor3 = Color3.new(1, 1, 1)
Swirl.TextSize = 12
UIGridLayout.Parent = Buttons
UIGridLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
UIGridLayout.SortOrder = Enum.SortOrder.LayoutOrder
UIGridLayout.VerticalAlignment = Enum.VerticalAlignment.Center
UIGridLayout.CellPadding = UDim2.new(0, 10, 0, 10)
UIGridLayout.CellSize = UDim2.new(0, 70, 0, 30)
UIGridLayout.FillDirectionMaxCells = 3
TPose.Name = "TPose"
TPose.Parent = Buttons
TPose.AnchorPoint = Vector2.new(0.5, 1)
TPose.BackgroundColor3 = Color3.new(0.121569, 0.121569, 0.121569)
TPose.BorderColor3 = Color3.new(0, 0, 0)
TPose.Font = Enum.Font.Arial
TPose.Text = "T-Pose"
TPose.TextColor3 = Color3.new(1, 1, 1)
TPose.TextSize = 12
LongArms.Name = "LongArms"
LongArms.Parent = Buttons
LongArms.AnchorPoint = Vector2.new(0.5, 1)
LongArms.BackgroundColor3 = Color3.new(0.121569, 0.121569, 0.121569)
LongArms.BorderColor3 = Color3.new(0, 0, 0)
LongArms.Font = Enum.Font.Arial
LongArms.Text = "LongArms"
LongArms.TextColor3 = Color3.new(1, 1, 1)
LongArms.TextSize = 12
CrazyHats.Name = "CrazyHats"
CrazyHats.Parent = Buttons
CrazyHats.AnchorPoint = Vector2.new(0.5, 1)
CrazyHats.BackgroundColor3 = Color3.new(0.121569, 0.121569, 0.121569)
CrazyHats.BorderColor3 = Color3.new(0, 0, 0)
CrazyHats.Font = Enum.Font.Arial
CrazyHats.Text = "CrazyHats"
CrazyHats.TextColor3 = Color3.new(1, 1, 1)
CrazyHats.TextSize = 12
Ring.Name = "Ring"
Ring.Parent = Buttons
Ring.AnchorPoint = Vector2.new(0.5, 1)
Ring.BackgroundColor3 = Color3.new(0.121569, 0.121569, 0.121569)
Ring.BorderColor3 = Color3.new(0, 0, 0)
Ring.Font = Enum.Font.Arial
Ring.Text = "Ring"
Ring.TextColor3 = Color3.new(1, 1, 1)
Ring.TextSize = 12
Orbit.Name = "Orbit"
Orbit.Parent = Buttons
Orbit.AnchorPoint = Vector2.new(0.5, 1)
Orbit.BackgroundColor3 = Color3.new(0.121569, 0.121569, 0.121569)
Orbit.BorderColor3 = Color3.new(0, 0, 0)
Orbit.Font = Enum.Font.Arial
Orbit.Text = "Orbit"
Orbit.TextColor3 = Color3.new(1, 1, 1)
Orbit.TextSize = 12
NoFace.Name = "NoFace"
NoFace.Parent = Buttons
NoFace.AnchorPoint = Vector2.new(0.5, 1)
NoFace.BackgroundColor3 = Color3.new(0.121569, 0.121569, 0.121569)
NoFace.BorderColor3 = Color3.new(0, 0, 0)
NoFace.Font = Enum.Font.Arial
NoFace.Text = "NoFace"
NoFace.TextColor3 = Color3.new(1, 1, 1)
NoFace.TextSize = 12
BlockHead.Name = "BlockHead"
BlockHead.Parent = Buttons
BlockHead.AnchorPoint = Vector2.new(0.5, 1)
BlockHead.BackgroundColor3 = Color3.new(0.121569, 0.121569, 0.121569)
BlockHead.BorderColor3 = Color3.new(0, 0, 0)
BlockHead.Font = Enum.Font.Arial
BlockHead.Text = "Blockhead"
BlockHead.TextColor3 = Color3.new(1, 1, 1)
BlockHead.TextSize = 12
NoClothes.Name = "NoClothes"
NoClothes.Parent = Buttons
NoClothes.AnchorPoint = Vector2.new(0.5, 1)
NoClothes.BackgroundColor3 = Color3.new(0.121569, 0.121569, 0.121569)
NoClothes.BorderColor3 = Color3.new(0, 0, 0)
NoClothes.Font = Enum.Font.Arial
NoClothes.Text = "NoClothes"
NoClothes.TextColor3 = Color3.new(1, 1, 1)
NoClothes.TextSize = 12
Helicopter.Name = "Helicopter"
Helicopter.Parent = Buttons
Helicopter.AnchorPoint = Vector2.new(0.5, 1)
Helicopter.BackgroundColor3 = Color3.new(0.121569, 0.121569, 0.121569)
Helicopter.BorderColor3 = Color3.new(0, 0, 0)
Helicopter.Font = Enum.Font.Arial
Helicopter.Text = "Heli"
Helicopter.TextColor3 = Color3.new(1, 1, 1)
Helicopter.TextSize = 12
Sit.Name = "Sit"
Sit.Parent = Buttons
Sit.AnchorPoint = Vector2.new(0.5, 1)
Sit.BackgroundColor3 = Color3.new(0.121569, 0.121569, 0.121569)
Sit.BorderColor3 = Color3.new(0, 0, 0)
Sit.Font = Enum.Font.Arial
Sit.Text = "Sit"
Sit.TextColor3 = Color3.new(1, 1, 1)
Sit.TextSize = 12
SwirlHats.Name = "SwirlHats"
SwirlHats.Parent = Buttons
SwirlHats.AnchorPoint = Vector2.new(0.5, 1)
SwirlHats.BackgroundColor3 = Color3.new(0.121569, 0.121569, 0.121569)
SwirlHats.BorderColor3 = Color3.new(0, 0, 0)
SwirlHats.Font = Enum.Font.Arial
SwirlHats.Text = "SwirlHats"
SwirlHats.TextColor3 = Color3.new(1, 1, 1)
SwirlHats.TextSize = 12
Topbar.Name = "Topbar"
Topbar.Parent = Menu
Topbar.AnchorPoint = Vector2.new(0.5, 0)
Topbar.BackgroundColor3 = Color3.new(0.0941177, 0.0941177, 0.0941177)
Topbar.BorderColor3 = Color3.new(0, 0, 0)
Topbar.Position = UDim2.new(0.5, 0, 0, 0)
Topbar.Size = UDim2.new(1, 0, 0, 25)
Close.Name = "Close"
Close.Parent = Topbar
Close.AnchorPoint = Vector2.new(1, 0)
Close.BackgroundColor3 = Color3.new(0, 0, 0)
Close.BorderSizePixel = 0
Close.Position = UDim2.new(1, 0, 0, 0)
Close.Size = UDim2.new(0, 18, 0, 18)
Close.Font = Enum.Font.SourceSans
Close.Text = "X"
Close.TextColor3 = Color3.new(1, 1, 1)
Close.TextSize = 14
Minimize.Name = "Minimize"
Minimize.Parent = Topbar
Minimize.AnchorPoint = Vector2.new(1, 0)
Minimize.BackgroundColor3 = Color3.new(0, 0, 0)
Minimize.BorderSizePixel = 0
Minimize.Position = UDim2.new(1, -20, 0, 0)
Minimize.Size = UDim2.new(0, 18, 0, 18)
Minimize.Font = Enum.Font.SourceSans
Minimize.Text = "_"
Minimize.TextColor3 = Color3.new(1, 1, 1)
Minimize.TextSize = 14
Title.Name = "Title"
Title.Parent = Topbar
Title.AnchorPoint = Vector2.new(0.5, 0)
Title.BackgroundColor3 = Color3.new(1, 1, 1)
Title.BackgroundTransparency = 1
Title.BorderSizePixel = 0
Title.Position = UDim2.new(0.5, 0, 0, 0)
Title.Size = UDim2.new(0.600000024, 0, 1, 0)
Title.Font = Enum.Font.Arial
Title.Text = "fePose v3 by xyz#8586"
Title.TextColor3 = Color3.new(1, 1, 1)
Title.TextSize = 12
MinMenu.Name = "MinMenu"
MinMenu.Parent = fePosev3
MinMenu.AnchorPoint = Vector2.new(1, 1)
MinMenu.BackgroundColor3 = Color3.new(0.0941177, 0.0941177, 0.0941177)
MinMenu.BorderColor3 = Color3.new(0, 0, 0)
MinMenu.Position = UDim2.new(1, -10, 1, -10)
MinMenu.Size = UDim2.new(0, 75, 0, 25)
Close_2.Name = "Close"
Close_2.Parent = MinMenu
Close_2.AnchorPoint = Vector2.new(1, 0)
Close_2.BackgroundColor3 = Color3.new(0, 0, 0)
Close_2.BorderSizePixel = 0
Close_2.Position = UDim2.new(1, 0, 0, 0)
Close_2.Size = UDim2.new(0, 18, 0, 18)
Close_2.Font = Enum.Font.SourceSans
Close_2.Text = "X"
Close_2.TextColor3 = Color3.new(1, 1, 1)
Close_2.TextSize = 14
Maximize.Name = "Maximize"
Maximize.Parent = MinMenu
Maximize.AnchorPoint = Vector2.new(1, 0)
Maximize.BackgroundColor3 = Color3.new(0, 0, 0)
Maximize.BorderSizePixel = 0
Maximize.Position = UDim2.new(1, -20, 0, 0)
Maximize.Size = UDim2.new(0, 18, 0, 18)
Maximize.Font = Enum.Font.SourceSans
Maximize.Text = "+"
Maximize.TextColor3 = Color3.new(1, 1, 1)
Maximize.TextSize = 14
Title_2.Name = "Title"
Title_2.Parent = MinMenu
Title_2.BackgroundColor3 = Color3.new(1, 1, 1)
Title_2.BackgroundTransparency = 1
Title_2.BorderSizePixel = 0
Title_2.Size = UDim2.new(0.600000024, 0, 1, 0)
Title_2.Font = Enum.Font.Arial
Title_2.Text = "FP"
Title_2.TextColor3 = Color3.new(1, 1, 1)
Title_2.TextSize = 12
local function GQYAP_fake_script()
    local script = Instance.new('LocalScript', fePosev3)
    local HttpService = game:GetService("HttpService")
    local Players = game:GetService("Players")
    local RunService = game:GetService("RunService")
    local UserInputService = game:GetService("UserInputService")
    local ReplicatedFirst = game:GetService("ReplicatedFirst")
    local Player = game:GetService("Players").LocalPlayer
    local PlayerGui = Player:WaitForChild("PlayerGui")
   
    local Gui = script.Parent
    local Menu = Gui.Menu
    local Buttons = Menu.Buttons
    local Topbar = Menu.Topbar
    local MinMenu = Gui.MinMenu
   
    Topbar.Close.MouseButton1Click:Connect(function()
        Gui:Destroy()
    end)
   
    Topbar.Minimize.MouseButton1Click:Connect(function()
        MinMenu.Parent = Gui
        Menu.Parent = ReplicatedFirst
    end)
   
    MinMenu.Close.MouseButton1Click:Connect(function()
        Gui:Destroy()
    end)
   
    MinMenu.Maximize.MouseButton1Click:Connect(function()
        Menu.Parent = Gui
        MinMenu.Parent = ReplicatedFirst
    end)
    -- scripted by zeezy
    local function makeDraggable(guiToSet)
        local dragging
        local dragInput
        local dragStart
        local startPos
        local function update(input)
            local delta = input.Position - dragStart
            guiToSet.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
        end
        guiToSet.InputBegan:Connect(function(input)
            if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
                dragging = true
                dragStart = input.Position
                startPos = guiToSet.Position
                input.Changed:Connect(function()
                    if input.UserInputState == Enum.UserInputState.End then
                        dragging = false
                    end
                end)
            end
        end)
        guiToSet.InputChanged:Connect(function(input)
            if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
                dragInput = input
            end
        end)
        UserInputService.InputChanged:Connect(function(input)
            if input == dragInput and dragging then
                update(input)
            end
        end)
    end
   
    makeDraggable(Menu)
    makeDraggable(MinMenu)
    MinMenu.Parent = ReplicatedFirst
    local function setButton(buttonName,functionToSet)
        local newbutton = Buttons:WaitForChild(buttonName,10)
        newbutton.MouseButton1Click:Connect(functionToSet)
    end
   
    local function getCharacter()
        local new = Player.Character or Player.CharacterAdded:Wait()
        return new
    end
   
    local function getHumanoid()
        local new = getCharacter():WaitForChild("Humanoid")
        return new
    end
   
    local function getPart(part)
        local new = getCharacter():WaitForChild(part,10)
        return new
    end
   
    local function getHats()
        local hatTable = {}
        for i,v in ipairs(getCharacter():GetChildren()) do
            if v:IsA("Accessory") then
                table.insert(hatTable,v.Handle)
            end
        end
        return hatTable
    end
   
    pcall(function()
        while true do
            wait()
            p.MaximumSimulationRadius = math.huge
            p.SimulationRadius = math.huge
        end
    end)
   
    local function noMesh(part)
        local mesh = part:FindFirstChildWhichIsA("DataModelMesh")
        if mesh then mesh:Destroy() end
    end
   
    local function newGUID()
        local new = HttpService:GenerateGUID(false)
        return new
    end
   
    local function bindRS(functionToBind)
        local id = newGUID()
        RunService:BindToRenderStep(id,300,functionToBind)
        getHumanoid().Died:Connect(function()
            RunService:UnbindFromRenderStep(id)
        end)
    end
   
    local function zeroGrav(part)
        local BodyForce = Instance.new("BodyForce")
        BodyForce.force = Vector3.new(0, workspace.Gravity, 0) * part:GetMass()
        BodyForce.Parent = part
    end
   
    local function cpos(part,base,xOffset,yOffset,zOffset,xRotate,yRotate,zRotate)
        if not part then warn("Part missing") return end
        if not base then warn("Base missing") return end
        zeroGrav(part)
        part:BreakJoints()
        bindRS(function()
            part.CFrame = base.CFrame * CFrame.new(xOffset,yOffset,zOffset) * CFrame.Angles(math.rad(xRotate),math.rad(yRotate),math.rad(zRotate))
        end)
    end
   
   
    local function spinpos(part,base,spinOffset,speed,x,y,z)
        if not part then warn("Part missing") return end
        if not base then warn("Base missing") return end
        local count = 0
        zeroGrav(part)
        part:BreakJoints()
        bindRS(function()
            part.CFrame = base.CFrame * CFrame.Angles(count+spinOffset,0,count+spinOffset) * CFrame.new(x,y,z)
            count = count + speed
        end)
    end
   
    local function ringpos(part,base,spinOffset,speed,x,y,z)
        if not part then warn("Part missing") return end
        if not base then warn("Base missing") return end
        local count = 0
        zeroGrav(part)
        part:BreakJoints()
        bindRS(function()
            part.CFrame = base.CFrame  * CFrame.new(x,y,z) * CFrame.Angles(count+spinOffset,0,count+spinOffset)
            count = count + speed
        end)
    end
   
    -- made by Zeezy#7203
    local function helipos(part,base,angle,spinOffset,distance,speed)
        if not part then warn("Part missing") return end
        if not base then warn("Base missing") return end
        local count = 0
        local anew = math.rad(angle)
        local offsetnew = math.rad(spinOffset)
        zeroGrav(part)
        part:BreakJoints()
        bindRS(function()
            part.CFrame = (base.CFrame * CFrame.Angles(anew,0,count+offsetnew)) * CFrame.new(0,distance,0)
            count = count + speed
        end)
    end
   
    local function sidehelipos(part,base,angle,spinOffset,distance,speed)
        if not part then warn("Part missing") return end
        if not base then warn("Base missing") return end
        local count = 0
        local anew = math.rad(angle)
        local offsetnew = math.rad(spinOffset)
        zeroGrav(part)
        part:BreakJoints()
        bindRS(function()
            part.CFrame = (base.CFrame * CFrame.new(0,-1,0) * CFrame.Angles(count+offsetnew,0,anew)) * CFrame.new(0,distance,0)
            count = count + speed
        end)
    end
   
   
    local function LongArms()
        cpos(getPart("Left Leg"),getPart("Left Arm"),0,-1.85,0,0,0,0)
        cpos(getPart("Right Leg"),getPart("Right Arm"),0,-1.85,0,0,0,0)
    end
   
    local function Swirl()
        local torso = getPart("Torso")
        cpos(getPart("Left Arm"),torso,-1,1.5,0,0,0,-90)
        cpos(getPart("Right Arm"),torso,1.5,1,0,0,0,180)
        cpos(getPart("Left Leg"),torso,-1.5,-1,0,0,0,0)
        cpos(getPart("Right Leg"),torso,1,-1.5,0,0,0,90)
    end
   
    local function TPose()
        local torso = getPart("Torso")
        cpos(getPart("Left Arm"),torso,-2,0.5,0,0,0,-90)
        cpos(getPart("Right Arm"),torso,2,0.5,0,0,0,90)
    end
   
    local function NoClothes()
        local shirt = getCharacter():FindFirstChildOfClass("Shirt")
        local pants = getCharacter():FindFirstChildOfClass("Pants")
        if shirt then shirt:Destroy() end
        if pants then pants:Destroy() end
    end
   
    local function SwirlHats()
        local head = getPart("Head")
        for i,v in ipairs(getHats()) do
            noMesh(v)
            zeroGrav(v)
            spinpos(v,head,i,0.1,0,0,0)
        end
    end
   
    local function NoFace()
        local head = getPart("Head")
        if head then
            local facedecal = head:FindFirstChildOfClass("Decal")
            if facedecal then facedecal:Destroy() end
        end
    end
    -- made by Zeezy#7203
    local function Sit()
        local humanoid = getHumanoid()
        if humanoid then
            humanoid.Sit = true
        end
    end
   
    local function Helicopter()
        local torso = getPart("Torso")
        local head = getPart("Head")
        helipos(getPart("Left Arm"),head,90,-90,-1.5,0.4)
        helipos(getPart("Right Arm"),head,90,90,-1.5,0.4)
        cpos(getPart("Left Leg"),torso,0,0,1.5,270,0,0)
        sidehelipos(getPart("Right Leg"),getPart("Left Leg"),0,90,0,0.5)
    end
   
    local function CrazyHats()
        local head = getPart("Head")
        for i,v in ipairs(getHats()) do
            noMesh(v)
            zeroGrav(v)
            v:BreakJoints()
            local rkt = Instance.new("RocketPropulsion")
            rkt.Target = getPart("Head")
            rkt.MaxSpeed = 100
            rkt.MaxTorque = Vector3.new(888888,888888,888888)
            rkt.MaxThrust = math.huge
            rkt.Parent = v
            rkt.ThrustP = math.huge
            rkt:Fire()
        end
    end
   
    local function Orbit()
        local rootpart = getPart("HumanoidRootPart")
        local hats = getHats()
        local ratio = math.rad(360 / #hats)
        for i,v in pairs(hats) do
            noMesh(v)
            zeroGrav(v)
            spinpos(v,rootpart,i%30,1,i%30,i%30,0)
        end
    end
    -- verm : Zeezy9892
    local function Ring()
        local rootpart = getPart("HumanoidRootPart")
        local hats = getHats()
        local ratio = math.rad(360 / #hats)
        for i,v in pairs(hats) do
            noMesh(v)
            zeroGrav(v)
            ringpos(v,rootpart,i,0.15,math.sin(i*ratio)*4,0,math.cos(i*ratio)*4)
        end
    end
   
    setButton("LongArms",LongArms)
    setButton("TPose",TPose)
    setButton("Swirl",Swirl)
    setButton("NoClothes",NoClothes)
    setButton("Sit",Sit)
    setButton("SwirlHats",SwirlHats)
    setButton("NoFace",NoFace)
    setButton("Helicopter",Helicopter)
    setButton("CrazyHats",CrazyHats)
    setButton("Orbit",Orbit)
    setButton("Ring",Ring)
end
coroutine.wrap(GQYAP_fake_script)()
end)
 
penisbutton.Name = "penisbutton"
penisbutton.Parent = mainframe
penisbutton.BackgroundColor3 = Color3.fromRGB(13, 13, 13)
penisbutton.BorderColor3 = Color3.fromRGB(59, 59, 59)
penisbutton.Position = UDim2.new(0.0409556329, 0, 0.717385173, 0)
penisbutton.Size = UDim2.new(0, 84, 0, 31)
penisbutton.Font = Enum.Font.SourceSans
penisbutton.Text = "Penis"
penisbutton.TextColor3 = Color3.fromRGB(255, 255, 255)
penisbutton.TextSize = 14.000
penisbutton.MouseButton1Down:connect(function()
 
 
 
 
 
--R6 dick  by diemiers
 
 
spawn(function()
local message = Instance.new("Message",workspace)
message.Text = "Fe penisito loaded"
wait(11)
message:Destroy()
end)
 
local name = "Torso"
if game.Players.LocalPlayer.Character:FindFirstChild("Humanoid").RigType == Enum.HumanoidRigType.R15 then
    name = "UpperTorso"
end
 
local ch = game.Players.LocalPlayer.Character
local prt=Instance.new("Model", workspace)
local z1 =  Instance.new("Part", prt)
z1.Name="Torso"
z1.CanCollide = false
z1.Anchored = true
local z2  =Instance.new("Part", prt)
z2.Name="Head"
z2.Anchored = true
z2.CanCollide = false
local z3 =Instance.new("Humanoid", prt)
z3.Name="Humanoid"
z1.Position = Vector3.new(0,9999,0)
z2.Position = Vector3.new(0,9991,0)
 game.Players.LocalPlayer.Character=prt
wait(5)
game.Players.LocalPlayer.Character=ch
wait(6)
game:GetService('RunService').Stepped:connect(function()
game.Players.LocalPlayer.Character.HumanoidRootPart.CanCollide = true
end)
game:GetService('RunService').RenderStepped:connect(function()
game.Players.LocalPlayer.Character.HumanoidRootPart.CanCollide = true
end)
plr = game.Players.LocalPlayer
mouse = plr:GetMouse()
 
game.Players.LocalPlayer.Character.HumanoidRootPart:Destroy()
 
local Hum = Instance.new("Humanoid")
   
 
 
Hum.Parent = game.Players.LocalPlayer.Character
game.Players.LocalPlayer.Character.Humanoid.Parent = game.Lighting
--game.Players.LocalPlayer.Character:FindFirstChild("Torso").Name = "Head"
--game.Players.LocalPlayer.Character:FindFirstChild("Head"):Destroy()
--game.Players.LocalPlayer.Character:FindFirstChild(name):Destroy()
--game.Players.LocalPlayer.Character.HumanoidRootPart.Name = "GaiPArt"
local root =game.Players.LocalPlayer.Character["Right Arm"] -- game.Players.LocalPlayer.Character["Left Leg"]
root.Name = "HumanoidRootPart"
 
Hum.HipHeight = 5
 
           
workspace.CurrentCamera.CameraSubject = game.Players.LocalPlayer.Character.HumanoidRootPart
 
 
 
 
for i,v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
   
    if v.Name ~=root.Name and v.Name ~="Humanoid" and v.Name ~= "Left Arm" and v.Name ~= "Left Leg" and v.Name ~= "Right Leg" then
       
        v:Destroy()
       
    elseif v.Name == "Left Arm" then
       
        local bp = Instance.new("BodyPosition",v)
        bp.MaxForce = Vector3.new(99999,99999,99999)
        local bg = Instance.new("BodyGyro",v)
        bg.MaxTorque = Vector3.new(9999999,9999999,999999)
         
        spawn(function()
            bp.D = 300
            while true do
                bp.Position = root.Position+Vector3.new(0,1.8+1.8+1.8-0.3,0)
                wait()
            end
           
        end)
       
            elseif v.Name == "Left Leg" then
       
        local bp = Instance.new("BodyPosition",v)
        bp.MaxForce = Vector3.new(99999,99999,99999)
                local bg = Instance.new("BodyGyro",v)
        bg.MaxTorque = Vector3.new(9999999,9999999,999999)
       
        spawn(function()
            bp.D = 300
            while true do
                bp.Position = root.Position+Vector3.new(0,1.8-0.3,0)
                wait()
            end
           
        end)
       
            elseif v.Name == "Right Leg" then
       
        local bp = Instance.new("BodyPosition",v)
        bp.MaxForce = Vector3.new(99999,99999,99999)
                local bg = Instance.new("BodyGyro",v)
        bg.MaxTorque = Vector3.new(9999999,9999999,999999)
        spawn(function()
         bp.D = 300
            while true do
                bp.Position = root.Position+Vector3.new(0,1.8+1.8-0.3,0)
                wait()
            end
           
        end)
    elseif v.Name == root.Name then
       
                    local bg = Instance.new("BodyGyro",v)
        bg.MaxTorque = Vector3.new(9999999,9999999,999999)
        bg.CFrame = CFrame.Angles(math.rad(0),math.rad(0),math.rad(90))
       
    end
   
   
end
 
--local se = Instance.new("SelectionBox",root)
--se.Adornee = root
 
 
power = 999999 -- change this to make it more or less powerful
 
power = power*10
 
---
wait(.1)
--local bambam = Instance.new("BodyThrust")
--bambam.Parent = game.Players.LocalPlayer.Character.HumanoidRootPart
--bambam.Force = Vector3.new(power,0,power)
--bambam.Location = game.Players.LocalPlayer.Character.HumanoidRootPart.Position
 
 
 
 
local mouse = game.Players.LocalPlayer:GetMouse()
 
 
local plr = game.Players.LocalPlayer
local torso = root
local flying = true
local deb = true
local ctrl = {f = 0, b = 0, l = 0, r = 0}
local lastctrl = {f = 0, b = 0, l = 0, r = 0}
local maxspeed = 120
local speed = 15
 
 
---local bambam = Instance.new("BodyThrust")
---bambam.Parent = torso
--bambam.Force = Vector3.new(9999999,0,9999999)
--bambam.Location = torso.Position
 
 
---
 
 
function Fly()
local bg = Instance.new("BodyGyro", torso)
bg.P = 9e4
bg.maxTorque = Vector3.new(0, 0, 0)
bg.cframe = torso.CFrame
local bv = Instance.new("BodyVelocity", torso)
bv.velocity = Vector3.new(0,0,0)
bv.maxForce = Vector3.new(9e9, 9e9, 9e9)
repeat wait()
 
if ctrl.l + ctrl.r ~= 0 or ctrl.f + ctrl.b ~= 0 then
speed = speed+.2
if speed > maxspeed then
speed = maxspeed
end
elseif not (ctrl.l + ctrl.r ~= 0 or ctrl.f + ctrl.b ~= 0) and speed ~= 0 then
speed = speed-1
if speed < 0 then
speed = 0
end
end
if (ctrl.l + ctrl.r) ~= 0 or (ctrl.f + ctrl.b) ~= 0 then
bv.velocity = ((game.Workspace.CurrentCamera.CoordinateFrame.lookVector * (ctrl.f+ctrl.b)) + ((game.Workspace.CurrentCamera.CoordinateFrame * CFrame.new(ctrl.l+ctrl.r,(ctrl.f+ctrl.b)*.2,0).p) - game.Workspace.CurrentCamera.CoordinateFrame.p))*speed
lastctrl = {f = ctrl.f, b = ctrl.b, l = ctrl.l, r = ctrl.r}
elseif (ctrl.l + ctrl.r) == 0 and (ctrl.f + ctrl.b) == 0 and speed ~= 0 then
bv.velocity = ((game.Workspace.CurrentCamera.CoordinateFrame.lookVector * (lastctrl.f+lastctrl.b)) + ((game.Workspace.CurrentCamera.CoordinateFrame * CFrame.new(lastctrl.l+lastctrl.r,(lastctrl.f+lastctrl.b)*.2,0).p) - game.Workspace.CurrentCamera.CoordinateFrame.p))*speed
else
bv.velocity = Vector3.new(0,0,0)
end
 
until not flying
ctrl = {f = 0, b = 0, l = 0, r = 0}
lastctrl = {f = 0, b = 0, l = 0, r = 0}
speed = 0
bg:Destroy()
bv:Destroy()
 
end
mouse.KeyDown:connect(function(key)
if key:lower() == "e" then
if flying then flying = false
else
flying = true
Fly()
end
elseif key:lower() == "w" then
ctrl.f = 1
elseif key:lower() == "s" then
ctrl.b = -1
elseif key:lower() == "a" then
ctrl.l = -1
elseif key:lower() == "d" then
ctrl.r = 1
end
end)
mouse.KeyUp:connect(function(key)
if key:lower() == "w" then
ctrl.f = 0
elseif key:lower() == "s" then
ctrl.b = 0
elseif key:lower() == "a" then
ctrl.l = 0
elseif key:lower() == "d" then
ctrl.r = 0
elseif key:lower() == "r" then
 
end
end)
Fly()
end)
 
aimbotespbutton.Name = "aimbotespbutton"
aimbotespbutton.Parent = mainframe
aimbotespbutton.BackgroundColor3 = Color3.fromRGB(13, 13, 13)
aimbotespbutton.BorderColor3 = Color3.fromRGB(59, 59, 59)
aimbotespbutton.Position = UDim2.new(0.354948819, 0, 0.716125429, 0)
aimbotespbutton.Size = UDim2.new(0, 84, 0, 31)
aimbotespbutton.Font = Enum.Font.SourceSans
aimbotespbutton.Text = "ESP & Aimbot"
aimbotespbutton.TextColor3 = Color3.fromRGB(255, 255, 255)
aimbotespbutton.TextSize = 14.000
aimbotespbutton.MouseButton1Down:connect(function()
loadstring(game:HttpGet("https://raw.githubusercontent.com/CriShoux/OwlHub/master/OwlHub.txt"))();
end)
 
invisflingbutton.Name = "invisflingbutton"
invisflingbutton.Parent = mainframe
invisflingbutton.BackgroundColor3 = Color3.fromRGB(13, 13, 13)
invisflingbutton.BorderColor3 = Color3.fromRGB(59, 59, 59)
invisflingbutton.Position = UDim2.new(0.668941975, 0, 0.716125429, 0)
invisflingbutton.Size = UDim2.new(0, 84, 0, 31)
invisflingbutton.Font = Enum.Font.SourceSans
invisflingbutton.Text = "Fling"
invisflingbutton.TextColor3 = Color3.fromRGB(255, 255, 255)
invisflingbutton.TextSize = 14.000
invisflingbutton.MouseButton1Down:connect(function()
 
 
 
spawn(function()
local message = Instance.new("Message",workspace)
message.Text = "Loaded press z to execute inviseble , press x to respawn)"
wait(0.5)
message:Destroy()
end)
 
 
 
 
 
 
 
 
local mouse = game.Players.LocalPlayer:GetMouse()
 
local groot = nil
 
mouse.KeyDown:connect(function(k)
   
    if k == "z" then
       
       
       
spawn(function()
local message = Instance.new("Message",workspace)
message.Text = "Fe Invisible Fling By Diemiers#4209 Loaded (wait 11 seconds to load)"
wait(11)
message:Destroy()
end)
 
 
local ch = game.Players.LocalPlayer.Character
local prt=Instance.new("Model", workspace)
local z1 =  Instance.new("Part", prt)
z1.Name="Torso"
z1.CanCollide = false
z1.Anchored = true
local z2  =Instance.new("Part", prt)
z2.Name="Head"
z2.Anchored = true
z2.CanCollide = false
local z3 =Instance.new("Humanoid", prt)
z3.Name="Humanoid"
z1.Position = Vector3.new(0,9999,0)
z2.Position = Vector3.new(0,9991,0)
 game.Players.LocalPlayer.Character=prt
wait(5)
game.Players.LocalPlayer.Character=ch
wait(6)
 
 
local plr = game.Players.LocalPlayer
mouse = plr:GetMouse()
 
local Hum = Instance.new("Humanoid")
Hum.Parent = game.Players.LocalPlayer.Character
 
 
local root =  game.Players.LocalPlayer.Character.HumanoidRootPart
 
 
for i,v in pairs(plr.Character:GetChildren()) do
   
    if v ~= root and  v.Name ~= "Humanoid" then
       
        v:Destroy()
       
    end
   
   
end
           
workspace.CurrentCamera.CameraSubject = root
 
local se = Instance.new("SelectionBox",root)
se.Adornee = root
 
 
game:GetService('RunService').Stepped:connect(function()
game.Players.LocalPlayer.Character.HumanoidRootPart.CanCollide = false
end)
game:GetService('RunService').RenderStepped:connect(function()
game.Players.LocalPlayer.Character.HumanoidRootPart.CanCollide = false
end)
 
 
power = 999999 -- change this to make it more or less powerful
 
power = power*10
 
---
wait(.1)
local bambam = Instance.new("BodyThrust")
bambam.Parent = game.Players.LocalPlayer.Character.HumanoidRootPart
bambam.Force = Vector3.new(power,0,power)
bambam.Location = game.Players.LocalPlayer.Character.HumanoidRootPart.Position
 
 
 
 
 
local plr = game.Players.LocalPlayer
local torso = root
local flying = true
local deb = true
local ctrl = {f = 0, b = 0, l = 0, r = 0}
local lastctrl = {f = 0, b = 0, l = 0, r = 0}
local maxspeed = 120
local speed = 15
 
 
---local bambam = Instance.new("BodyThrust")
---bambam.Parent = torso
--bambam.Force = Vector3.new(9999999,0,9999999)
--bambam.Location = torso.Position
 
 
---
groot = root
 
function Fly()
local bg = Instance.new("BodyGyro", torso)
bg.P = 9e4
bg.maxTorque = Vector3.new(0, 0, 0)
bg.cframe = torso.CFrame
local bv = Instance.new("BodyVelocity", torso)
bv.velocity = Vector3.new(0,0,0)
bv.maxForce = Vector3.new(9e9, 9e9, 9e9)
repeat wait()
 
if ctrl.l + ctrl.r ~= 0 or ctrl.f + ctrl.b ~= 0 then
speed = speed+.2
if speed > maxspeed then
speed = maxspeed
end
elseif not (ctrl.l + ctrl.r ~= 0 or ctrl.f + ctrl.b ~= 0) and speed ~= 0 then
speed = speed-1
if speed < 0 then
speed = 0
end
end
if (ctrl.l + ctrl.r) ~= 0 or (ctrl.f + ctrl.b) ~= 0 then
bv.velocity = ((game.Workspace.CurrentCamera.CoordinateFrame.lookVector * (ctrl.f+ctrl.b)) + ((game.Workspace.CurrentCamera.CoordinateFrame * CFrame.new(ctrl.l+ctrl.r,(ctrl.f+ctrl.b)*.2,0).p) - game.Workspace.CurrentCamera.CoordinateFrame.p))*speed
lastctrl = {f = ctrl.f, b = ctrl.b, l = ctrl.l, r = ctrl.r}
elseif (ctrl.l + ctrl.r) == 0 and (ctrl.f + ctrl.b) == 0 and speed ~= 0 then
bv.velocity = ((game.Workspace.CurrentCamera.CoordinateFrame.lookVector * (lastctrl.f+lastctrl.b)) + ((game.Workspace.CurrentCamera.CoordinateFrame * CFrame.new(lastctrl.l+lastctrl.r,(lastctrl.f+lastctrl.b)*.2,0).p) - game.Workspace.CurrentCamera.CoordinateFrame.p))*speed
else
bv.velocity = Vector3.new(0,0.1,0)
end
 
until not flying
ctrl = {f = 0, b = 0, l = 0, r = 0}
lastctrl = {f = 0, b = 0, l = 0, r = 0}
speed = 0
bg:Destroy()
bv:Destroy()
 
end
mouse.KeyDown:connect(function(key)
if key:lower() == "e" then
if flying then flying = false
else
flying = true
Fly()
end
elseif key:lower() == "w" then
ctrl.f = 1
elseif key:lower() == "s" then
ctrl.b = -1
elseif key:lower() == "a" then
ctrl.l = -1
elseif key:lower() == "d" then
ctrl.r = 1
end
end)
mouse.KeyUp:connect(function(key)
if key:lower() == "w" then
ctrl.f = 0
elseif key:lower() == "s" then
ctrl.b = 0
elseif key:lower() == "a" then
ctrl.l = 0
elseif key:lower() == "d" then
ctrl.r = 0
elseif key:lower() == "r" then
 
end
end)
Fly()
 
       
       
    elseif k == "x" then
       
       
        spawn(function()
local message = Instance.new("Message",workspace)
message.Text = "Respawning dont spam"
wait(1)
message:Destroy()
end)
       
        local saved = groot.Position
       
local ch = game.Players.LocalPlayer.Character
local prt=Instance.new("Model", workspace)
local z1 =  Instance.new("Part", prt)
z1.Name="Torso"
z1.CanCollide = false
z1.Anchored = true
local z2  =Instance.new("Part", prt)
z2.Name="Head"
z2.Anchored = true
z2.CanCollide = false
local z3 =Instance.new("Humanoid", prt)
z3.Name="Humanoid"
z1.Position = Vector3.new(0,9999,0)
z2.Position = Vector3.new(0,9991,0)
 game.Players.LocalPlayer.Character=prt
wait(5)
 game.Players.LocalPlayer.Character=ch
local poop = nil
        repeat wait() poop = game.Players.LocalPlayer.Character:FindFirstChild("Head") until poop ~= nil
        wait(1)
        game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(saved)
       
    end
   
   
end)
end)
 
servercrashbutton.Name = "servercrashbutton"
servercrashbutton.Parent = mainframe
servercrashbutton.BackgroundColor3 = Color3.fromRGB(13, 13, 13)
servercrashbutton.BorderColor3 = Color3.fromRGB(59, 59, 59)
servercrashbutton.Position = UDim2.new(0.0409556329, 0, 0.449986994, 0)
servercrashbutton.Size = UDim2.new(0, 268, 0, 31)
servercrashbutton.Font = Enum.Font.SourceSans
servercrashbutton.Text = "Server Crash"
servercrashbutton.TextColor3 = Color3.fromRGB(255, 255, 255)
servercrashbutton.TextSize = 14.000
servercrashbutton.MouseButton1Down:connect(function()
loadstring(game:HttpGet(('https://pastebin.com/raw/J4nmWQJA'),true))()
end)
 
closebutton.Name = "closebutton"
closebutton.Parent = mainframe
closebutton.BackgroundColor3 = Color3.fromRGB(13, 13, 13)
closebutton.BorderColor3 = Color3.fromRGB(59, 59, 59)
closebutton.Position = UDim2.new(0.955631375, 0, -0.000186622565, 0)
closebutton.Size = UDim2.new(0, 13, 0, 12)
closebutton.Font = Enum.Font.SourceSans
closebutton.Text = "X"
closebutton.TextColor3 = Color3.fromRGB(255, 255, 255)
closebutton.TextSize = 14.000
closebutton.MouseButton1Down:connect(function()
openbutton.Visible = true
mainframe.Visible = false
end)
 
openbutton.Name = "openbutton"
openbutton.Parent = spookyxrgui
openbutton.BackgroundColor3 = Color3.fromRGB(22, 22, 22)
openbutton.BorderColor3 = Color3.fromRGB(79, 79, 79)
openbutton.Position = UDim2.new(0, 0, 0.706632674, 0)
openbutton.Size = UDim2.new(0, 128, 0, 28)
openbutton.Font = Enum.Font.Arial
openbutton.Text = "OPEN"
openbutton.TextColor3 = Color3.fromRGB(255, 255, 255)
openbutton.TextSize = 14.000
openbutton.MouseButton1Down:connect(function()
mainframe.Visible = true
openbutton.Visible = false
end)
 
-- Scripts:
 
local function RDEGIN_fake_script() -- mainframe.LocalScript
    local script = Instance.new('LocalScript', mainframe)
 
    script.parent.Selectable = true
    script.Parent.Active = true
    script.parent.Draggable = true
end
coroutine.wrap(RDEGIN_fake_script)()