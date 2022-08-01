local LocalPlayer = game:GetService("Players").LocalPlayer
local Client = getsenv(game.Players.LocalPlayer.PlayerGui.Client)
local ReplicatedStorage = game:GetService("ReplicatedStorage")

local allSkins = {
   {'AK47_BloxFun'},
   {'AK47_Kenzie'},
   {'AK47_EVOLVe Committee'},
   {'AK47_Cat'},
   {'AK47_Hallows'},
   {'AK47_Neonline'},
   {'AK47_Shooting Star'},
   {'AK47_Halo'},
   {'AK47_Outrunner'},
   {'M4A4_Jester'},
   {'M4A4_Flashy Ride'},
   {'SG_Yltude'},
   {'SG_Knighthood'},
   {'AWP_Chan'},
   {'AWP_Nerf'},
   {'AWP_Retroactive'},
   {'AWP_Hika'},
   {'AWP_DEVILL'},
   {'AWP_Mxlu'},
   {'AWP_Nikitos Games'},
   {'DesertEagle_Mxlu'},
   {'DesertEagle_Xmas'},
   {'DesertEagle_Dark'},
   

   {'ButterflyGod_Stock'},
   {'TrueGold_Stock'},
   

   {'BananaDev_Stock'}, 
   {'BanHammer_Moderator'},
   {'Darkheart_Tiredness'},
   {'Illumina_Princess'},
   

   {'ReaverKnife_Reaver'},
   
   
   {'Pillow_Cute'},
   {'FishKnife_Mackerel'},   
   

   {'Bayonet_RSL'},
   {'Bayonet_Berserk'},
   {'Bayonet_Drain'},
   {'Bayonet_Gems Fade'},
   {'Bayonet_Handprint'},
   {'Bayonet_Haunted'},
   

   {'KarambitKnife_Cat'},
   {'KarambitKnife_Gold'},
   {'KarambitKnife_Stock'},
   {'KarambitKnife_Weeb'},
   

   {'RealButterfly_Cat'},
   {'Pickaxe_Cat'},
   

   {'Classic Knife_Stock'},
   {'Classic Knife_Future'},
   

   {'Dot_Skin1'},
   {'Dot_Skin2'},
   {'Dot_Skin3'},
   

   {'Sports Glove_Weeb'},
   {'Handwraps_Guts'},
   {'Fingerless Glove_Spookiness'},
   {'Handwraps_Microbes'},
}

local isUnlocked

local mt = getrawmetatable(game)
local oldNamecall = mt.__namecall
setreadonly(mt, false)

local isUnlocked

mt.__namecall = newcclosure(function(self, ...)
   local args = {...}
   if getnamecallmethod() == "InvokeServer" and tostring(self) == "Hugh" then
       return
   end
   if getnamecallmethod() == "FireServer" then
       if args[1] == LocalPlayer.UserId then
           return
       end
       if string.len(tostring(self)) == 38 then
           if not isUnlocked then
               isUnlocked = true
               for i,v in pairs(allSkins) do
                   local doSkip
                   for i2,v2 in pairs(args[1]) do
                       if v[1] == v2[1] then
                           doSkip = true
                       end
                   end
                   if not doSkip then
                       table.insert(args[1], v)
                   end
               end
           end
           return
       end
       if tostring(self) == "DataEvent" and args[1][4] then
           local currentSkin = string.split(args[1][4][1], "_")[2]
           if args[1][2] == "Both" then
               LocalPlayer["SkinFolder"]["CTFolder"][args[1][3]].Value = currentSkin
               LocalPlayer["SkinFolder"]["TFolder"][args[1][3]].Value = currentSkin
           else
               LocalPlayer["SkinFolder"][args[1][2] .. "Folder"][args[1][3]].Value = currentSkin
           end
       end
   end
   return oldNamecall(self, ...)
end)
   
setreadonly(mt, true)

Client.CurrentInventory = allSkins

local TClone, CTClone = LocalPlayer.SkinFolder.TFolder:Clone(), game.Players.LocalPlayer.SkinFolder.CTFolder:Clone()
LocalPlayer.SkinFolder.TFolder:Destroy()
LocalPlayer.SkinFolder.CTFolder:Destroy()
TClone.Parent = LocalPlayer.SkinFolder
CTClone.Parent = LocalPlayer.SkinFolder
