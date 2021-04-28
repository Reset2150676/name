-- CONFIGURATIONS:

local secphaseblock = false -- change to false if you want auto block to be disabled in second phase

-- Main Script:

local phase = 1
local inv = false
local autoblock = false
local dead = false
local holdbone = false
local CAS = game:GetService("ContextActionService")
local FREEZE_COMMAND  = "Stunned"
CAS:UnbindAction(FREEZE_COMMAND)
local pass = getrenv()._G.Pass
game.StarterGui:SetCoreGuiEnabled(Enum.CoreGuiType.Chat, true)
local Players = game:GetService("Players")
local localPlayer = Players.LocalPlayer
local mouse = localPlayer:GetMouse()

-- anti ban idkkk

spawn(function()
    for i,v in pairs(game:GetService("Lighting"):GetChildren()) do 
    v:Destroy() 
    end
    game:GetService("Lighting").DescendantAdded:Connect(function(t) 
    wait() 
    t:Destroy() 
    end)
    game:GetService("ReplicatedStorage")["Ban Remote"]:Destroy()
end)

-- main stuff

game.Players.LocalPlayer.PlayerGui.CharacterSelection.Character.Value = "Sans"
if not localPlayer.Character then
	localPlayer.CharacterAdded:Wait()
end
wait(0.5)
local root = localPlayer.Character.HumanoidRootPart
wait(2)
print("running main thingy idk")

local humanoid = localPlayer.Character:WaitForChild("Humanoid")

humanoid.Died:Connect(function()
print("died")
for i,v in pairs(game.Players.LocalPlayer:WaitForChild("StarterPlaylist"):GetChildren()) do
v:Destroy()
end
dead = true
inv = false
end)

spawn(function()
while wait(1) do
if dead == true then break end
local A_1 = 
{
	[1] = pass, 
	[2] = "ChangeSetting", 
	[3] = "DeathScene", 
	[4] = false
}
local Event = game:GetService("ReplicatedStorage").Remotes.Functions
Event:InvokeServer(A_1)
end
end)

spawn(function()
while wait() do
if dead == true then break end
if holdbone == true then
if game.Players.LocalPlayer.Character.Bone.Transparency ~= 0 then
local A_1 = 
{
	[1] = getrenv()._G.Pass, 
	[2] = "SpawnBone", 
	[3] = true, 
	[4] = true
}
local Event = game:GetService("ReplicatedStorage").Remotes.SansMoves
Event:InvokeServer(A_1)
end
end
end
end)

function hidebone()
local A_1 = 
{
	[1] = getrenv()._G.Pass, 
	[2] = "SpawnBone", 
	[3] = false, 
}
local Event = game:GetService("ReplicatedStorage").Remotes.SansMoves
Event:InvokeServer(A_1)
end

function bone(v)
spawn(function()
local A_1 = 
{
	[1] = getrenv()._G.Pass, 
	[2] = "SpawnBone", 
	[3] = v, 
}
local Event = game:GetService("ReplicatedStorage").Remotes.SansMoves
Event:InvokeServer(A_1)
end)
end

function stun(val)
if val == true then
game.Players.LocalPlayer.Character.HumanoidRootPart.Anchored = true
CAS:BindActionAtPriority(
    FREEZE_COMMAND,
    function() 
        return Enum.ContextActionResult.Sink
    end,
    false,
    Enum.ContextActionPriority.High.Value,
    Enum.KeyCode.W,
    Enum.KeyCode.S,
    Enum.KeyCode.A,
    Enum.KeyCode.D,
    Enum.KeyCode.F,
    Enum.KeyCode.R,
    Enum.KeyCode.One,
    Enum.KeyCode.Two,
    Enum.KeyCode.Three,
    Enum.KeyCode.Four,
    Enum.KeyCode.Five,
    Enum.KeyCode.Six,
    Enum.KeyCode.Seven,
    Enum.KeyCode.Eight,
    Enum.KeyCode.Nine,
    Enum.KeyCode.Zero
    )
elseif val == false then
game.Players.LocalPlayer.Character.HumanoidRootPart.Anchored = false
CAS:UnbindAction(FREEZE_COMMAND)
end
end

function unblock()
spawn(function()
for i = 1,5 do
wait()
local A_1 = 
{
	[1] = pass, 
	[2] = "Blocking", 
	[3] = false
}
local Event = game:GetService("ReplicatedStorage").Remotes.Functions
Event:InvokeServer(A_1)
end
end)
end

spawn(function()
while wait() do
if secphaseblock == false then return end
if autoblock == true then
if dead == true then break end
local A_1 = 
	{
		[1] = pass, 
		[2] = "Blocking", 
		[3] = true
	}
local Event = game:GetService("ReplicatedStorage").Remotes.Functions
Event:InvokeServer(A_1)
end
end
end)

spawn(function()
while true do
if dead == true then break end
wait()
if inv == true then
spawn(function()
local A_1 = 
				{
					[1] = pass, 
					[2] = "InvFrames", 
					[3] = 0.5
				}
			local Event = game:GetService("ReplicatedStorage").Remotes.Events
			Event:FireServer(A_1)
end)
end
end
end)

function hitnear()
spawn(function()
		for i,v in pairs(workspace:GetChildren()) do
			if v:FindFirstChild("Torso") then
				if v.Name ~= game.Players.LocalPlayer.Name then
					if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character["Right Leg"].Position).Magnitude <= 10 then
						local A_1 = pass
						local A_2 = v
						local A_3 = 
							{
								["Type"] = "Knockback", 
								["HitEffect"] = "BoneHitEffect", 
								["HurtAnimation"] = game:GetService("ReplicatedStorage").Animations.HurtAnimations.Knockback2, 
								["Velocity"] = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.lookVector * 100, 
								["CameraShake"] = "Bump", 
								["HitTime"] = 1, 
								["VictimCFrame"] = v.HumanoidRootPart.CFrame, 
								["Sound"] = nil, 
								["Damage"] = 0
							}
						local Event = game:GetService("ReplicatedStorage").Remotes.Damage
						Event:InvokeServer(A_1, A_2, A_3)
					end
				end
			end
		end
	end)
end

function talk(text,color)
if dead == true then return end
local A_1 = 
{
	[1] = getrenv()._G.Pass, 
	[2] = "Chatted", 
	[3] = text, 
	[4] = color
}
local Event = game:GetService("ReplicatedStorage").Remotes.Events
Event:FireServer(A_1)
end

function getlockchar()
local char = game.Players.LocalPlayer.Backpack.Main.LockOnScript.LockOn.Value
return char
end

function getlock()
local pos = mouse.Hit.p
if game.Players.LocalPlayer.Backpack.Main.LockOnScript.LockOn.Value ~= nil then
pos = workspace:FindFirstChild(game.Players.LocalPlayer.Backpack.Main.LockOnScript.LockOn.Value.Name).Torso.Position
end
warn(pos)
return pos
end


-- AMIMATIONS:

local PunchAnim = Instance.new("Animation")
PunchAnim.AnimationId = "rbxassetid://4357851278"
local PunchAnimTrack = humanoid:LoadAnimation(PunchAnim)
PunchAnimTrack.Priority = Enum.AnimationPriority.Action
PunchAnimTrack.Looped = false

local PunchAnim2 = Instance.new("Animation")
PunchAnim2.AnimationId = "rbxassetid://4357872409"
local PunchAnim2Track = humanoid:LoadAnimation(PunchAnim2)
PunchAnim2Track.Priority = Enum.AnimationPriority.Action
PunchAnim2Track.Looped = false

local PunchAnim3 = Instance.new("Animation")
PunchAnim3.AnimationId = "rbxassetid://4357890370"
local PunchAnim3Track = humanoid:LoadAnimation(PunchAnim3)
PunchAnim3Track.Priority = Enum.AnimationPriority.Action
PunchAnim3Track.Looped = false

local LastPunchAnim = Instance.new("Animation")
LastPunchAnim.AnimationId = "rbxassetid://4357907686"
local LastPunchAnimTrack = humanoid:LoadAnimation(LastPunchAnim)
LastPunchAnimTrack.Priority = Enum.AnimationPriority.Action
LastPunchAnimTrack.Looped = false

local SleepAnim = Instance.new("Animation")
SleepAnim.AnimationId = "rbxassetid://3877055653"
local SleepAnimTrack = humanoid:LoadAnimation(SleepAnim)
SleepAnimTrack.Priority = Enum.AnimationPriority.Action
SleepAnimTrack.Looped = true
--SleepAnimTrack:Play()

local HurtAnim = Instance.new("Animation")
HurtAnim.AnimationId = "rbxassetid://4460182501"
local HurtAnimTrack = humanoid:LoadAnimation(HurtAnim)
HurtAnimTrack.Priority = Enum.AnimationPriority.Action
HurtAnimTrack.Looped = false
--HurtAnimTrack:Play()

local HurtGroundAnim = Instance.new("Animation")
HurtGroundAnim.AnimationId = "rbxassetid://4416715001"
local HurtGroundAnimTrack = humanoid:LoadAnimation(HurtGroundAnim)
HurtGroundAnimTrack.Priority = Enum.AnimationPriority.Action
HurtGroundAnimTrack.Looped = true
--HurtGroundAnimTrack:Play()

-- ATTACKS:
function punch()
PunchAnimTrack:Play()
bone(true)
spawn(function()
		for i,v in pairs(workspace:GetChildren()) do
			if v:FindFirstChild("Torso") then
				if v.Name ~= game.Players.LocalPlayer.Name then
					if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character["Right Leg"].Position).Magnitude <= 10 then
						local A_1 = pass
						local A_2 = v
						local A_3 = 
							{
								["Type"] = "Normal", 
								["HitEffect"] = "BoneHitEffect", 
								["HurtAnimation"] = game:GetService("ReplicatedStorage").Animations.HurtAnimations.Stunned, 
								["Velocity"] = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.lookVector * 0.001,
								["CameraShake"] = "Bump", 
                                ["Karma"] = 50,
								["HitTime"] = 1, 
								["VictimCFrame"] = v.HumanoidRootPart.CFrame, 
								["Sound"] = game:GetService("ReplicatedStorage").Sounds.Knockback, 
								["Damage"] = 10
							}
						local Event = game:GetService("ReplicatedStorage").Remotes.Damage
						Event:InvokeServer(A_1, A_2, A_3)
					end
				end
			end
		end
wait(0.5)
bone(false)
	end)
end

function dunk()
local anim = Instance.new("Animation")
anim.AnimationId = "rbxassetid://6122095988"
local animmTrack = game.Players.LocalPlayer.Character.Humanoid:LoadAnimation(anim)
animmTrack.Priority = Enum.AnimationPriority.Action
animmTrack.Looped = false
animmTrack:Play()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = getlockchar().HumanoidRootPart.CFrame * CFrame.new(0,0,3)
talk("get dunked on.",Color3.new(1,1,1))
for i = 1,7 do
spawn(function()
for i = 1,2 do
local A_1 = pass
local A_3 = 
{
	["Type"] = "Normal", 
	["HitEffect"] = "SansLineBones", 
	["HurtAnimation"] = game:GetService("ReplicatedStorage").Animations.HurtAnimations.Hurt1, 
	["Velocity"] = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.lookVector +  Vector3.new(0.001,0.001,0.001), 
	["Karma"] = 2, 
	["HitTime"] = 1, 
	["VictimCFrame"] = CFrame.new(0,0,0), 
	["Sound"] = game:GetService("ReplicatedStorage").Sounds.Hurt, 
	["Damage"] = 10
}
local Event = game:GetService("ReplicatedStorage").Remotes.Damage
Event:InvokeServer(A_1,getlockchar(), A_3)
end
end)
wait(0.17)
end
spawn(function()
local A_1 = pass
local A_2 = game:GetService("Workspace").NoStaminaDummy
local A_3 = 
{
	["Type"] = "Knockback", 
	["HitEffect"] = "BoneHitEffect", 
	["HurtAnimation"] = game:GetService("ReplicatedStorage").Animations.HurtAnimations.Hurt1, 
	["Velocity"] = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.lookVector +  Vector3.new(0.001,25,0.001), 
	["Karma"] = 10, 
	["HitTime"] = 1, 
	["VictimCFrame"] = CFrame.new(0,0,0), 
	["Sound"] = game:GetService("ReplicatedStorage").Sounds.Kick, 
	["Damage"] = 10
}
local Event = game:GetService("ReplicatedStorage").Remotes.Damage
Event:InvokeServer(A_1,getlockchar(), A_3)
end)
end

function infkr()
stun(true)
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = getlockchar().HumanoidRootPart.CFrame * CFrame.new(0,0,3)
local target = getlockchar()
holdbone = true
local A_1 = pass
local A_2 = target
local A_3 = 
    {
        ["Type"] = "Normal", 
        ["HitEffect"] = "BoneHitEffect", 
        ["HurtAnimation"] = game:GetService("ReplicatedStorage").Animations.HurtAnimations.Stunned, 
        ["Velocity"] = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.lookVector * 0.01, 
        ["CameraShake"] = "Bump", 
        ["HitTime"] = 5, 
        ["Karma"] = 0,
        ["VictimCFrame"] = nil, 
        ["Sound"] = game:GetService("ReplicatedStorage").Sounds.Break, 
        ["Damage"] = 10
    }
local Event = game:GetService("ReplicatedStorage").Remotes.Damage
Event:InvokeServer(A_1, A_2, A_3)
wait(1)
for i = 1,8 do 
spawn(function()
local A_1 = pass
local A_2 = target
local A_3 = 
    {
        ["Type"] = "Normal", 
        ["HitEffect"] = "BoneHitEffect", 
        ["HurtAnimation"] = game:GetService("ReplicatedStorage").Animations.HurtAnimations.Stunned, 
        ["Velocity"] = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.lookVector * 0.01, 
        ["CameraShake"] = "Bump", 
        ["HitTime"] = 5, 
        ["Karma"] = 0,
        ["VictimCFrame"] = nil, 
        ["Sound"] = game:GetService("ReplicatedStorage").Sounds.Punch, 
        ["Damage"] = 10
    }
local Event = game:GetService("ReplicatedStorage").Remotes.Damage
Event:InvokeServer(A_1, A_2, A_3)
end)
local anim = math.random(1,3)
if anim == 1 then
PunchAnimTrack:Play()
elseif anim == 2 then
PunchAnim2Track:Play()
elseif anim == 3 then
PunchAnim3Track:Play()
end
wait(0.5)
end
LastPunchAnimTrack:Play()
holdbone = false
wait(0.3)
stun(false)
bone(false)
local A_1 = pass
local A_2 = target
local A_3 = 
    {
        ["Type"] = "Knockback", 
        ["HitEffect"] = "BoneHitEffect", 
        ["HurtAnimation"] = game:GetService("ReplicatedStorage").Animations.HurtAnimations.Knockback2, 
        ["Velocity"] = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.lookVector * 100, 
        ["CameraShake"] = "Bump", 
        ["HitTime"] = 2, 
        ["Karma"] = math.huge,
        ["VictimCFrame"] = nil, 
        ["Sound"] = game:GetService("ReplicatedStorage").Sounds.Knockback, 
        ["Damage"] = 10
    }
local Event = game:GetService("ReplicatedStorage").Remotes.Damage
Event:InvokeServer(A_1, A_2, A_3)
end

function rainbowattack()
spawn(function()
		for i,v in pairs(workspace:GetChildren()) do
			if v:FindFirstChild("Torso") then
				if v.Name ~= game.Players.LocalPlayer.Name then
					if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character["Right Leg"].Position).Magnitude <= 10 then
						local A_1 = pass
						local A_2 = v
						local A_3 = 
							{
								["Type"] = "Knockback", 
								["HitEffect"] = "RainbowExplosion", 
								["HurtAnimation"] = game:GetService("ReplicatedStorage").Animations.HurtAnimations.Knockback2, 
								["Velocity"] = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.lookVector * 100, 
								["CameraShake"] = "Bump", 
								["HitTime"] = 1, 
								["VictimCFrame"] = v.HumanoidRootPart.CFrame, 
								["Sound"] = game:GetService("ReplicatedStorage").Objects.Moves.Kamehameha.Sound.Fire, 
								["Damage"] = 10
							}
						local Event = game:GetService("ReplicatedStorage").Remotes.Damage
						Event:InvokeServer(A_1, A_2, A_3)
					end
				end
			end
		end
	end)
end

function idkattack()
for i = 1,20 do
wait()
spawn(function()
local A_1 = getrenv()._G.Pass
local A_2 = game:GetService("Players").LocalPlayer.Backpack.Main.LockOnScript.LockOn.Value
local A_3 = 
    {
    ["HitTime"] = 2, 
    ["Type"] = "Knockback", 
    ["HitEffect"] = "SansLineBones",  
    ["HurtAnimation"] = game:GetService("ReplicatedStorage").Animations.HurtAnimations.SlideOnGround,  
    ["Sound"] = game:GetService("ReplicatedStorage").Sounds.Kick,
    ["Velocity"] = Vector3.new(0.001,0.001,0.001), 
    ["CombatInv"] = true,
    ["Karma"] = 10,
    ["Damage"] = 35
    }
local Event = game:GetService("ReplicatedStorage").Remotes.Damage
Event:InvokeServer(A_1, A_2, A_3)
end)
end
end

function finalattack()
local A_1 = 
{
	[1] = pass, 
	[2] = "Telekinesis", 
	[3] = "Special2", 
	[4] = game:GetService("Players").LocalPlayer.Backpack.Main.LockOnScript.LockOn.Value
}
local Event = game:GetService("ReplicatedStorage").Remotes.SansMoves
Event:InvokeServer(A_1)
talk("Heres your ticket to the pain train",Color3.new(1,0.8,0.8))
wait(1)
local A_1 = 
{
	[1] = pass, 
	[2] = "Telekinesis", 
	[3] = "Special", 
	[4] = game:GetService("Players").LocalPlayer.Backpack.Main.LockOnScript.LockOn.Value
}
local Event = game:GetService("ReplicatedStorage").Remotes.SansMoves
Event:InvokeServer(A_1)
end
-- COOLDOWNS
local finalcd = false
local punchcd = false
local dunkcd = false
local rainbowcd = false
local infkrcd = false
local idkcd = false

mouse.KeyDown:Connect(function(k)
if dead == true then return end
if game.Players.LocalPlayer.Character.HumanoidRootPart.Anchored == true then return end
 if k == "z" then
local A_1 = 
{
	[1] = getrenv()._G.Pass, 
	[2] = "GasterBlasters", 
	[3] = "SummonSpecial", 
	[4] = getlock()
}
local Event = game:GetService("ReplicatedStorage").Remotes.SansMoves
Event:InvokeServer(A_1)
elseif k == "x" then
local A_1 = 
{
	[1] = getrenv()._G.Pass, 
	[2] = "GasterBlasters", 
	[3] = "SummonEight", 
	[4] = getlock()
}
local Event = game:GetService("ReplicatedStorage").Remotes.SansMoves
Event:InvokeServer(A_1)
elseif k == "c" then
if dunkcd == true then return end
spawn(function()
dunkcd = true
wait(5)
dunkcd = false
end)
print("dunk")
dunk()
elseif k == "v" then
if punchcd == true then return end
spawn(function()
punchcd = true
wait(1)
punchcd = false
end)
print("punch")
punch()
elseif k == "b" then
if rainbowcd == true then return end
spawn(function()
rainbowcd = true
wait(1)
rainbowcd = false
end)
print("rainbowattack")
rainbowattack()
elseif k == "n" then
if infkrcd == true then return end
spawn(function()
infkrcd = true
wait(8)
infkrcd = false
end)
print("inf kr")
infkr()
elseif k == "m" then
if idkcd == true then return end
spawn(function()
idkcd = true
wait(5)
idkcd = false
end)
print("idk thing")
idkattack()
elseif k == "g" then
if finalcd == true then return end
spawn(function()
finalcd = true
wait(45)
finalcd = false
end)
print("final ae")
finalattack()
end
end)


-- Music:
for i,v in pairs(game.Players.LocalPlayer:WaitForChild("StarterPlaylist"):GetChildren()) do
v:Destroy()
end
local music = Instance.new("Sound",game.Players.LocalPlayer:WaitForChild("StarterPlaylist"))
music.Volume = 0.7
music.SoundId = "rbxassetid://4628607656"
music.Looped = true
music:Play()
print("musik gone")



warn("Waiting For Phase 2")
repeat wait()

until game.Players.LocalPlayer.Character.Data.Stamina.Value <= 700
inv = true
hitnear()
spawn(function()
wait()
local oldcf = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = oldcf * CFrame.new(0,-40,0)
wait(0.3)
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = oldcf
end)
wait(0.4)
stun(true)
HurtAnimTrack:Play()
phase = 2
print("phase "..phase)
music:Stop()
wait(2)
HurtGroundAnimTrack:Play()
wait(1)
talk("!?",Color3.new(0.5,0.5,0.5))
wait(3)
talk("heh.",Color3.new(0.5,0.5,0.5))
wait(3)
HurtGroundAnimTrack:Stop()
wait()
SleepAnimTrack:Play()
talk("guess i have another shot at you, huh?",Color3.new(1,0,0))
wait(3)
talk("there's no point in giving up at this point.",Color3.new(0.5,0.5,0.5))
wait(3)
talk("and i can't screw up this last chance i've been given.",Color3.new(1,0,0))
wait(5)
talk("no matter what it takes...",Color3.new(0.5,0.5,0.5))
wait(3)
talk("i'll bring you to justice.",Color3.new(0.5,0.5,0.5))
wait(3)
talk("and i will make you suffer what we felt.",Color3.new(1,0,0))
wait(4)
talk("so, kiddo, get ready...",Color3.new(0.5,0.5,0.5))
wait(4)
talk("because you're about to get dunked on much harder than before.",Color3.new(1,0,0))
wait(4)
talk("Sans is dead serious now*",Color3.new(1,0,0))
wait(6)
autoblock = true
holdbone = true
SleepAnimTrack:Stop()
music.SoundId = "rbxassetid://4686555781"
music.TimePosition = 0
music:Play()
inv = false
unblock()
stun(false)
warn("Waiting For Phase 3")
repeat wait()
until game.Players.LocalPlayer.Character.Data.Stamina.Value <= 500
music:Stop()
autoblock = false
inv = true
hitnear()
spawn(function()
wait()
local oldcf = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = oldcf * CFrame.new(0,-40,0)
wait(0.3)
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = oldcf
end)
wait(0.4)
stun(true)
holdbone = false
wait()
hidebone()
wait(2)
talk("what just happened?",Color3.new(1,0,0))
wait(3)
talk("..?",Color3.new(0.5,0.5,0.5))
wait(3)
talk("oh hey there!",Color3.new(1,0,0))
wait(2)
talk("i see that you have finally arrived huh?",Color3.new(0.5,0.5,0.5))
wait(3)
talk("oh well, kid.",Color3.new(0.5,0.5,0.5))
wait(2)
talk("you will now face something that you will hardly forget.",Color3.new(1,0,0))
wait(5)
talk("i have told you from many genocide routes before...",Color3.new(0.5,0.5,0.5))
wait(5)
talk("reset.",Color3.new(1,0,0))
wait(1)
talk("but you didn't listen to me.",Color3.new(0.5,0.5,0.5))
wait(3)
talk("you could have fixed all this in only a press of a button.",Color3.new(1,0,0))
wait(5)
talk("but now, it's too late.",Color3.new(0.5,0.5,0.5))
wait(3)
talk("now you will face our your consequences...",Color3.new(1,0,0))
wait(4)
talk("that driven you into this.",Color3.new(1,0,0))
SleepAnimTrack:Play()
music.SoundId = "rbxassetid://4739499225"
music.TimePosition = 0
music.Looped = false
music:Play()
wait(47)
stun(false)
SleepAnimTrack:Stop()
wait(10)
stun(true)
wait(10)
warn("Waiting For Phase 4")
wait(1)
talk("I..",Color3.new(0.5,0.5,0.5))
wait(3)
talk("I cant..",Color3.new(0.5,0.5,0.5))
wait(3)
HurtGroundAnimTrack:Stop()
wait()
SleepAnimTrack:Play()
talk("I could not defeat you..",Color3.new(1,0,0))
wait(3)
talk("Sigh.",Color3.new(0.5,0.5,0.5))
wait(3)
talk("?!.",Color3.new(1,0,0))
wait(5)
talk("Heh.",Color3.new(0.5,0.5,0.5))
wait(3)
talk("Seems like I have another shot at you dont I?",Color3.new(0.5,0.5,0.5))
wait(3)
talk("Oh well kid, Get ready..",Color3.new(1,0,0))
wait(4)
talk("Because..",Color3.new(0.5,0.5,0.5))
wait(4)
talk("THIS WILL BE YOUR DEMISE.",Color3.new(1,0,0))
wait(4)
talk("This is Sans' final chance*",Color3.new(1,0,0))
wait(6)
SleepAnimTrack:Play()
music.SoundId = "rbxassetid://1127771065"
music.TimePosition = 0
music.Looped = false
music:Play()
wait(3)
stun(false)
SleepAnimTrack:Stop()
wait(147)
stun(true)
wait(5)
warn("Waiting For Phase 5")
wait(1)
talk("Heh..",Color3.new(0.5,0.5,0.5))
wait(3)
talk("I got hit again.. eh?.",Color3.new(0.5,0.5,0.5))
wait(3)
HurtGroundAnimTrack:Stop()
wait()
SleepAnimTrack:Play()
talk("Oh well.",Color3.new(1,0,0))
wait(3)
talk("You have just made a BIGGER mistake..",Color3.new(0.5,0.5,0.5))
wait(3)
talk("Well.",Color3.new(1,0,0))
wait(5)
talk("Dont say I didnt warn ya..",Color3.new(0.5,0.5,0.5))
wait(3)
talk("Kid prepare as always.",Color3.new(0.5,0.5,0.5))
wait(3)
talk("Because.",Color3.new(1,0,0))
wait(4)
talk("Im going all out.",Color3.new(0.5,0.5,0.5))
SleepAnimTrack:Play()
music.SoundId = "rbxassetid://5848113195"
music.TimePosition = 0
music.Looped = false
music:Play()
wait(3)
stun(false)
SleepAnimTrack:Stop()
wait(147)
stun(true)
wait(5)
warn("Waiting For Phase 6")
wait(1)
talk("...",Color3.new(0.5,0.5,0.5))
wait(3)
talk("You've got me this time..",Color3.new(0.5,0.5,0.5))
wait(3)
HurtGroundAnimTrack:Stop()
wait()
SleepAnimTrack:Play()
talk("I cant take it anymore.",Color3.new(1,0,0))
wait(3)
talk("This is too hard..",Color3.new(0.5,0.5,0.5))
wait(3)
talk("I-.",Color3.new(1,0,0))
wait(5)
talk("I just wanna see my brother again..",Color3.new(0.5,0.5,0.5))
wait(3)
talk("Papyrus...",Color3.new(0.5,0.5,0.5))
wait(3)
talk("heh heh...",Color3.new(1,0,0))
wait(4)
talk("I WONT GIVE UP FOR YOU!.",Color3.new(0.5,0.5,0.5))
SleepAnimTrack:Play()
music.SoundId = "rbxassetid://5938181440"
music.TimePosition = 0
music.Looped = false
music:Play()
wait(2)
stun(false)
SleepAnimTrack:Stop()
wait(147)
stun(true)
wait(5)
wait(1)
talk("...",Color3.new(0.5,0.5,0.5))
wait(3)
talk("This is it...",Color3.new(0.5,0.5,0.5))
wait(3)
HurtGroundAnimTrack:Stop()
wait()
SleepAnimTrack:Play()
talk("Sorry paps...",Color3.new(1,0,0))
wait(3)
talk("I failed you.",Color3.new(0.5,0.5,0.5))
wait(3)
talk("I-.",Color3.new(1,0,0))
wait(5)
talk("I'll see you there.. paps.",Color3.new(0.5,0.5,0.5))
wait(10)
talk("I'm joking.",Color3.new(1,0,0))
wait(2)
talk("Do you think I can do down just like that?",Color3.new(0.5,0.5,0.5))
wait(4)
talk("We have JUST gotten started kid.",Color3.new(0.5,0.5,0.5))
wait(3)
talk("I'm done messing around with you.",Color3.new(0.5,0.5,0.5))
wait(3)
talk("DIE",Color3.new(0.5,0.5,0.5))
wait(1)
talk("YOU LITTLE",Color3.new(0.5,0.5,0.5))
wait(1)
talk("S#(I)T",Color3.new(0.5,0.5,0.5))
music.SoundId = "rbxassetid://6534888188"
music.TimePosition = 0
music:Play()
inv = false
unblock()
stun(false)
repeat wait()
until game.Players.LocalPlayer.Character.Data.Stamina.Value <= 500
music:Stop()
autoblock = true
inv = true
hitnear()
spawn(function()
wait()
local oldcf = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = oldcf * CFrame.new(0,-40,0)
wait(0.3)
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = oldcf
end)
wait(0.4)
stun(true)
holdbone = false
wait()
hidebone()
SleepAnimTrack:Play()
talk("Tis but a scratch.",Color3.new(0.5,0.5,0.5))
wait(3)
talk("I still have 10 phases to go through.",Color3.new(0.5,0.5,0.5))
wait(3)
talk("Ima make u go to funny brazil and make ur neck go brr.",Color3.new(0.5,0.5,0.5))
wait(5)
music.SoundId = "rbxassetid://4587005692"
music.TimePosition = 0
music:Play()
inv = false
unblock()
stun(false)
repeat wait()

until game.Players.LocalPlayer.Character.Data.Stamina.Value <= 500
music:Stop()
autoblock = false
inv = true
hitnear()
spawn(function()
wait()
local oldcf = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = oldcf * CFrame.new(0,-40,0)
wait(0.3)
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = oldcf
end)
wait(0.4)
stun(true)
holdbone = false
wait()
hidebone()
wait(2)
talk("This pain...",Color3.new(0.5,0.5,0.5))
wait(3)
talk("Is nothing.",Color3.new(0.5,0.5,0.5))
wait(3)
talk("It's nothing compared to the ammount of times I died.",Color3.new(0.5,0.5,0.5))
wait(6)
talk("It's nothing compared to the pain I felt when you killed my brother in cold blood.",Color3.new(0.5,0.5,0.5))
wait(6)
talk("We will fight until the end of time.",Color3.new(0.5,0.5,0.5))
wait(3)
talk("I won't lose no matter what.",Color3.new(0.5,0.5,0.5))
wait(3)
talk("Die.",Color3.new(0.5,0.5,0.5))
wait(5)
music.SoundId = "rbxassetid://5617223140"
music.Looped = false
music:Play()
wait(3)
stun(false)
SleepAnimTrack:Stop()
wait(228)
stun(true)
wait(5)
wait(3)
talk("I thought I made this pretty clear.",Color3.new(0.5,0.5,0.5))
wait(4)
talk("I told you I WON'T lose.",Color3.new(0.5,0.5,0.5))
wait(3)
talk("Clearly, you fail to understand such simple things.",Color3.new(0.5,0.5,0.5))
wait(4)
talk("I'll make sure you die this time.",Color3.new(0.5,0.5,0.5))
wait(2)
music.SoundId = "rbxassetid://6246969810"
music.Looped = false
music:Play()
wait(3)
stun(false)
SleepAnimTrack:Stop()
wait(220)
stun(true)
wait(5)
wait(3)
talk("WHY.",Color3.new(0.5,0.5,0.5))
wait(1)
talk("WON'T.",Color3.new(0.5,0.5,0.5))
wait(1)
talk("YOU.",Color3.new(0.5,0.5,0.5))
wait(1)
talk("DIE!!!.",Color3.new(0.5,0.5,0.5))
wait(5)
music.SoundId = "rbxassetid://2878329200"
music.TimePosition = 0
music:Play()
inv = false
unblock()
stun(false)
repeat wait()

until game.Players.LocalPlayer.Character.Data.Stamina.Value <= 500
music:Stop()
autoblock = false
inv = true
hitnear()
spawn(function()
wait()
local oldcf = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = oldcf * CFrame.new(0,-40,0)
wait(0.3)
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = oldcf
end)
wait(0.4)
stun(true)
holdbone = false
wait()
hidebone()
wait(2)
talk("This is taking longer than I thought.",Color3.new(0.5,0.5,0.5))
wait(4)
talk("Oh well, I can wait.",Color3.new(0.5,0.5,0.5))
wait(1)
music.SoundId = "rbxassetid://2878329200"
music.Looped = false
music:Play()
wait(2)
stun(false)
SleepAnimTrack:Stop()
wait(185)
stun(true)
wait(5)
wait(3)
talk("...",Color3.new(0.5,0.5,0.5))
wait(3)
talk("Don't you have anything better to do?",Color3.new(0.5,0.5,0.5))
wait(4)
talk("Yes, im talking to you behind the computer screen.",Color3.new(0.5,0.5,0.5))
wait(5)
talk("Go play something else.",Color3.new(0.5,0.5,0.5))
wait(3)
talk("I can do this ALL day.",Color3.new(0.5,0.5,0.5))
wait(5)
music.SoundId = "rbxassetid://6164618172"
music.Looped = false
music:Play()
SleepAnimTrack:Play()
wait(47)
stun(false)
SleepAnimTrack:Stop()
wait(261)
stun(true)
wait(5)
wait(3)
SleepAnimTrack:Play()
talk("...",Color3.new(1,0,0))
wait(3)
talk("You're really determined to beat me, aren't you?",Color3.new(1,0,0))
wait(5)
talk("Well face it.",Color3.new(1,0,0))
wait(2)
SleepAnimTrack:Stop()
wait(2)
talk("YOU WILL NEVER BE ABLE TO DEFEAT ME!",Color3.new(0.5,0.5,0.5))
music.SoundId = "rbxassetid://5282871055"
music.Looped = false
music:Play()
wait(13)
stun(false)
wait(204)
stun(true)
HurtAnimTrack:Play()
wait(3)
wait(1)
talk("...",Color3.new(1,0,0))
wait(3)
talk("You.......",Color3.new(0.5,0.5,0.5))
wait(6)
talk("Hit...",Color3.new(0.5,0.5,0.5))
wait(5)
talk("Me...",Color3.new(0.5,0.5,0.5))
wait(5)
music.SoundId = "rbxassetid://5718191326"
music.Looped = false
music:Play()
wait(13)
talk("ARE YOU READY TO DIE?",Color3.new(0.5,0.5,0.5))
wait(5)
HurtGroundAnimTrack:Stop()
stun(false)
wait(211)
stun(true)
wait(2)
wait(3)
HurtAnimTrack:Play()
talk("You know what this feeling is, right?",Color3.new(1,0,0))
wait(4)
talk("You've felt this more than once.",Color3.new(1,0,0))
wait(4)
talk("...",Color3.new(1,0,0))
wait(3)
talk("Wait am I-",Color3.new(1,0,0))
wait(3)
talk("Oh no...",Color3.new(1,0,0))
wait(2)
SleepAnimTrack:Play()
talk("No...",Color3.new(1,0,0))
wait(3)
talk("My body feels like its breaking apart...",Color3.new(1,0,0))
wait(4)
talk("But something deep inside WON'T LET ME DIE.",Color3.new(1,0,0))
wait(4)
talk("I got to be honest with you kiddo.",Color3.new(1,0,0))
wait(4)
talk("Dying sounds like WAY too much effort.",Color3.new(1,0,0))
wait(4)
talk("So i'm not gonna die, and won't, EVER.",Color3.new(1,0,0))
wait(4)
talk("I came here to do one thing and one thing only.",Color3.new(1,0,0))
wait(4)
talk("Kill you.",Color3.new(1,0,0))
wait(3)
talk("Nice meeting ya kiddo.",Color3.new(1,0,0))
wait(3)
talk("Goodbye.",Color3.new(1,0,0))
wait(2)
wait(1)
autoblock = false
holdbone = true
SleepAnimTrack:Stop()
music.SoundId = "rbxassetid://6511111835"
music.TimePosition = 0
music:Play()
inv = false
unblock()
stun(false)
repeat wait()
until game.Players.LocalPlayer.Character.Data.Stamina.Value <= 500
music:Stop()
autoblock = false
inv = true
hitnear()
spawn(function()
wait()
local oldcf = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = oldcf * CFrame.new(0,-40,0)
wait(0.3)
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = oldcf
end)
wait(0.4)
stun(true)
holdbone = false
wait()
hidebone()
SleepAnimTrack:Play()
wait(2)
talk("That hurt a bit.",Color3.new(0.5,0.5,0.5))
wait(3)
talk("Mind if I ask for some HELP?",Color3.new(1,0,0))
wait(3)
talk("Sans has gotten a power boost! Attack raised to 50!",Color3.new(0.5,0.5,0.5))
wait(7)
autoblock = false
holdbone = true
SleepAnimTrack:Stop()
music.SoundId = "rbxassetid://5762248184"
music.TimePosition = 0
music:Play()
inv = false
unblock()
stun(false)
repeat wait()

until game.Players.LocalPlayer.Character.Data.Stamina.Value <= 500
music:Stop()
autoblock = true
inv = true
hitnear()
spawn(function()
wait()
local oldcf = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = oldcf * CFrame.new(0,-40,0)
wait(0.3)
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = oldcf
end)
wait(0.4)
stun(true)
holdbone = false
wait()
hidebone()
SleepAnimTrack:Play()
talk("You know what this feeling is, right?",Color3.new(0.5,0.5,0.5))
wait(4)
talk("I think im-",Color3.new(0.5,0.5,0.5))
wait(3)
talk("Oh no...",Color3.new(0.5,0.5,0.5))
wait(4)
talk("I'm melting, aren't I?",Color3.new(0.5,0.5,0.5))
wait(3)
talk("Well congrats kid.",Color3.new(0.5,0.5,0.5))
wait(5)
SleepAnimTrack:Stop()
talk("You failed.",Color3.new(0.5,0.5,0.5))
wait(3)
talk("I'm not going away that easily",Color3.new(0.5,0.5,0.5))
wait(4)
talk("You'll have to do a LOT more than hit me with that knife of yours.",Color3.new(0.5,0.5,0.5))
wait(6)
autoblock = false
holdbone = false
SleepAnimTrack:Stop()
music.SoundId = "rbxassetid://5728357518"
music.TimePosition = 0
music:Play()
inv = false
unblock()
stun(false)
repeat wait()

until game.Players.LocalPlayer.Character.Data.Stamina.Value <= 500
music:Stop()
autoblock = true
inv = true
hitnear()
spawn(function()
wait()
local oldcf = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = oldcf * CFrame.new(0,-40,0)
wait(0.3)
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = oldcf
end)
wait(0.4)
stun(true)
holdbone = false
wait()
hidebone()
SleepAnimTrack:Play()
talk("It hurts so much...",Color3.new(0.5,0.5,0.5))
wait(4)
talk("Please...stop...",Color3.new(0.5,0.5,0.5))
wait(6)
talk("I can't take this anymore...",Color3.new(0.5,0.5,0.5))
wait(4)
talk("...",Color3.new(0.5,0.5,0.5))
wait(4)
music.SoundId = "rbxassetid://2878329200"
music.Looped = false
music:Play()
wait(4)
talk("No...",Color3.new(0.5,0.5,0.5))
wait(3)
talk("I won't die like this.",Color3.new(0.5,0.5,0.5))
wait(4)
talk("Hehe...",Color3.new(0.5,0.5,0.5))
wait(2)
talk("Welcome back brother",Color3.new(0.5,0.5,0.5))
wait(4)
talk("Hi sans",Color3.new(249,222,47))
wait(6)
SleepAnimTrack:Stop()
talk("Feels good to be back after so long!",Color3.new(249,222,47))
wait(4)
talk("It's good to have you here again paps.",Color3.new(1,0,0))
wait(4)
talk("Is that the human?",Color3.new(249,222,47))
wait(3)
talk("Yes.",Color3.new(1,0,0))
wait(1)
talk("OH MY GOD SANS.",Color3.new(249,222,47))
wait(1)
talk("WE MUST CAPTURE THEM!",Color3.new(249,222,47))
wait(1)
talk("Whatever you say bro.",Color3.new(1,0,0))
wait(3)
stun(false)
wait(234)
talk("This is taking longer than I thought.",Color3.new(249,222,47))
wait(4)
talk("That's the power of humans bro.",Color3.new(1,0,0))
wait(4)
talk("Ugh! Fish lady would've captured them by now!.",Color3.new(249,222,47))
wait(4)
talk("Wait, actually, let me try this out.",Color3.new(249,222,47))
wait(7)
stun(true)
wait(3)
talk("HEYA PUNK",Color3.new(199,255,0))
wait(3)
talk("ITS BEEN A WHILE, LET'S SEE WHAT YOU GOT THIS TIME",Color3.new(199,255,0))
wait(3)
talk("Actually, it would be fair if I let you take your turn before mine",Color3.new(199,255,0))
wait(4)
talk("*You feel SCARED",Color3.new(0.5,0.5,0.5))
wait(5)
talk("Pathetic.",Color3.new(199,255,0))
wait(2)
talk("Welp, my turn!",Color3.new(199,255,0))
wait(3)
stun(false)
wait(20)
wait(15)
stun(true)
talk("Is this what you wanted human?",Color3.new(249,222,47))
wait(5)
talk("Look, I don't think you plan on giving up.",Color3.new(249,222,47))
wait(5)
talk("It's a shame, really. Papyrus would've LOVED to see a good ending for once.",Color3.new(249,222,47))
wait(7)
talk("What, we both know i haven't been alive as I have been",Color3.new(249,222,47))
wait(3)
talk("I'm sorry human",Color3.new(249,222,47))
wait(3)
SleepAnimTrack:Play()
talk("dev got super lazy so no dialog for 76 seconds lol.",Color3.new(1,0,0))
wait(76)
