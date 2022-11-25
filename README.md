_G.FastAttack = true
_G.SelectWeapon = "Combat"
_G.Auto_Farm = true

    if game.PlaceId == 2753915549 then
        W = true
    elseif game.PlaceId == 4442272183 then
        W2 = true
    elseif game.PlaceId == 7449423635 then
        W3 = true
    end

loadstring(game:HttpGet("https://pastebin.com/raw/2Je11ayP")();

function topos(Pos)
    Distance = (Pos.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
    if game.Players.LocalPlayer.Character.Humanoid.Sit == true then game.Players.LocalPlayer.Character.Humanoid.Sit = false end
    pcall(function() tween = game:GetService("TweenService"):Create(game.Players.LocalPlayer.Character.HumanoidRootPart,TweenInfo.new(Distance/210, Enum.EasingStyle.Linear),{CFrame = Pos}) end)
    tween:Play()
    if Distance <= 250 then
        tween:Cancel()
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Pos
    end
    if _G.StopTween == true then
        tween:Cancel()
        _G.Clip = false
    end
  end

function Click()
    game:GetService'VirtualUser':CaptureController()
    game:GetService'VirtualUser':Button1Down(Vector2.new(1280, 672))
  end
  
  function AutoHaki()
    if not game:GetService("Players").LocalPlayer.Character:FindFirstChild("HasBuso") then
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Buso")
    end
  end
  
  function EquipWeapon(ToolSe)
    if game.Players.LocalPlayer.Backpack:FindFirstChild(ToolSe) then
    local tool = game.Players.LocalPlayer.Backpack:FindFirstChild(ToolSe)
    wait(.4)
    game.Players.LocalPlayer.Character.Humanoid:EquipTool(tool)
  end
  end

coroutine.wrap(function()
local StopCamera = require(game.ReplicatedStorage.Util.CameraShaker)StopCamera:Stop()
    for v,v in pairs(getreg()) do
        if typeof(v) == "function" and getfenv(v).script == game:GetService("Players").LocalPlayer.PlayerScripts.CombatFramework then
             for v,v in pairs(debug.getupvalues(v)) do
                if typeof(v) == "table" then
                    spawn(function()
                        game:GetService("RunService").RenderStepped:Connect(function()
                            if _G.FastAttack then
                                 pcall(function()
                                     v.activeController.timeToNextAttack = -(math.huge^math.huge^math.huge)
                                     v.activeController.attacking = false
                                     v.activeController.increment = 4
                                     v.activeController.blocking = false   
                                     v.activeController.hitboxMagnitude = 150
                                     v.activeController.humanoid.AutoRotate = true
                                       v.activeController.focusStart = 0
                                       v.activeController.currentAttackTrack = 0
                                     sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRaxNerous", math.huge)
                                 end)
                             end
                         end)
                    end)
                end
            end
        end
    end
end)();

spawn(function()
    while wait() do
        if _G.Auto_Farm then
                pcall(function()
                    if not string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameMon) then
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
                    end
                    if game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == false then
                        CheckQuest()
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StartQuest",NameQuest,LevelQuest)
                        end
                    if game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == true then
                        CheckQuest()
                        if game:GetService("Workspace").Enemies:FindFirstChild(Mon) then
                            for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                if v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 then
                                    if v.Name == Mon then
                                        repeat wait()
                                            if string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameMon) then
                                                EquipWeapon(_G.SelectWeapon)
                                                AutoHaki()
                                                StartMagnet = true
                                                topos(game:GetService("Workspace").Enemies[Mon].HumanoidRootPart.CFrame * CFrame.new(0, 30, 1))
                                                game:GetService'VirtualUser':CaptureController()
                                                game:GetService'VirtualUser':Button1Down(Vector2.new(1280, 672))
                                            else
                                                StartMagnet = false
                                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("AbandonQuest")
                                            end
                                        until not _G.Auto_Farm or v.Humanoid.Health <= 0 or not v.Parent or game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == false
                                    end
                                end
                            end
                        else
                            StartMagnet = false
                            if game:GetService("ReplicatedStorage"):FindFirstChild(Mon) then
                                topos(game:GetService("ReplicatedStorage"):FindFirstChild(Mon).HumanoidRootPart.CFrame * CFrame.new(0,20,0))
                            else	
                                topos(CFrameMon)
                            end
                        end
                    end
                end)
            end
        end
    end)

    spawn(function()
        game:GetService("RunService").RenderStepped:Connect(function()
         pcall(function()
             if _G.Auto_Farm then
                 CheckQuest()
     for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                         for i2,v2 in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                             if v.Name == Mon and v2.Name == Mon then
                                 v2.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame
                                 v2.HumanoidRootPart.CanCollide = false
                                 v2.HumanoidRootPart.CanCollide = false
                                 v2.Head.CanCollide = false
                                 v.Head.CanCollide = false
                                 v2.Humanoid.WalkSpeed = 0
                                 v.Humanoid.WalkSpeed = 0
                                 if v.Humanoid:FindFirstChild("Animator") then
                                     v.Humanoid.Animator:Destroy()
                                 end
                                 sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius", math.huge)
     v.Humanoid:ChangeState(11)
                             end
                         end
                     end
                 end
             end)
         end)
     end)
     
     
     spawn(function()
         game:GetService("RunService").Heartbeat:Connect(function()
             if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Humanoid") and _G.Auto_Farm then
                 setfflag("HumanoidParallelRemoveNoPhysics", "False")
                 setfflag("HumanoidParallelRemoveNoPhysicsNoSimulate2", "False")
                 game:GetService("Players").LocalPlayer.Character.Humanoid:ChangeState(11)
             end
         end)
     end)
