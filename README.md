-- Plato configuration
local accountId = 10157; -- Plato account id [IMPORTANT]
local allowPassThrough = false; -- Allow user through if error occurs, may reduce security
local allowKeyRedeeming = false; -- Automatically check keys to redeem if valid
local useDataModel = false;

-- Plato callbacks
local onMessage = function(message)
    print(message) -- You can customize this to display messages in your UI/console
end;

-- Plato internals [START]
local fRequest, fStringFormat, fSpawn, fWait = request or http.request or http_request or syn.request, string.format, task.spawn, task.wait;
local localPlayerId = game:GetService("Players").LocalPlayer.UserId;
local rateLimit, rateLimitCountdown, errorWait = false, 0, false;
-- Plato internals [END]

-- Plato global functions [START]
function getLink()
    return fStringFormat("https://gateway.platoboost.com/a/%i?id=%i", accountId, localPlayerId);
end;

function verify(key)
    -- ... (existing code)
end;
-- Plato global functions [END]

-- Add the following code to check the key when _G.Key is set
if _G.Key then
    local isValidKey = verify(_G.Key)
    if isValidKey then
        -- Key is valid, you can perform additional actions or logic here
        print("Key is valid!")
    else
        -- Key is invalid, handle accordingly
        print("Key is invalid!")
    end
end
