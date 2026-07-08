--[[
    SH Hub - Roblox UI Script
    Tabs: نسخ (Copy) | تحكم (Control)
]]

local Players = game:GetService("Players")
local CoreGui = game:GetService("CoreGui")
local TweenService = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")

local LocalPlayer = Players.LocalPlayer
local PlayerGui = LocalPlayer:WaitForChild("PlayerGui")

-- helper: choose best parent for executor GUIs (Delta/Synapse/etc)
local function getGuiParent()
    local ok, hidden = pcall(function() return gethui() end)
    if ok and hidden then return hidden end
    local ok2, cg = pcall(function() return CoreGui end)
    if ok2 and cg then return cg end
    return PlayerGui
end
local guiParent = getGuiParent()

-- cleanup old
pcall(function()
    for _, n in ipairs({"SHHub","SHMini","SHSplash"}) do
        local old = guiParent:FindFirstChild(n)
        if old then old:Destroy() end
        local old2 = PlayerGui:FindFirstChild(n)
        if old2 then old2:Destroy() end
    end
end)

----------------------------------------------------------------
-- إشعار فريق SH Hub – يظهر بعد دقيقتين من تشغيل السكربت
