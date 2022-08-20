
if not _G.Key then
    repeat wait() until _G.Key
end
while wait() do
    success = pcall(function() 
        request = http_request or request or HttpPost or syn.request
        hwid = game:GetService("RbxAnalyticsService"):GetClientId()
        Payload = game:GetService("HttpService"):JSONEncode({key = _G.Key, hwid = hwid })
        response = request({
            Url = "https://maseieie.herokuapp.com/gpo/1",
            Method = "POST",
            Headers = {
                ["Content-Type"] = "application/json"
            },
            Body = Payload
        })
        local res = game:GetService("HttpService"):JSONDecode(response.Body)
        if res["success"] then
          print ("Hello World")
        else
            game.Players.LocalPlayer:Kick(res["message"])
        end
    end)
    if success then 
        break    
    end
end
