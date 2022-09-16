pcall(function()
--esp(av(),dw()) (curtime,reqtime)
pool = {}
pool.new = function()
    local base = {}
    base.global = {}
    base.class = function(name) base[name] = {} end
    base.add = function(class, name, func) base[class][name] = func end
    base.define = function(class, name, val) base[class][name] = val end
    base.get = function(class, name) return base[class][name] end
    base.call = function(class, name) base[class][name]() end
    return base
end

 
--- init base ---
 
local kek = {}
kek.pool = pool.new(); pool = kek.pool; player = game.Players.LocalPlayer;
 
 
CreateObject = function(properties)
    local object = Instance.new(properties.Class)
    for i, v in pairs(properties) do
        pcall(function()
            if v ~= "Class" then
                object[i] = v
            end
        end)
    end 
    return object
end
 
 
-- t.menus will now define pre-created objects instead of just '0xf'
kek.menus = {
    ["Main"] = {},
    ["LocalPlayer"] = {Links = {}, Auto = {}, ReqBar = false},
    ["Server"] = {Links = {"Destruction"}, Auto = {}, ReqBar = false},
    ["Scripts"] = {Links = {}, Auto = {
        CreateObject {
            Class = "TextBox",
            Name = "search",
            BackgroundColor3 = Color3.new(14/255, 60/255, 66/255),
            BorderColor3 = Color3.new(3/255, 53/255, 49/255),
            Position = UDim2.new(0, 13, 0, 10),
            Size = UDim2.new(1, -26, 0, 27),
            Font = Enum.Font.SourceSans,
            FontSize = Enum.FontSize.Size14,
            Text = "Search for a script",
            TextColor3 = Color3.new(204/255, 204/255, 204/255)
        },
        CreateObject {
            Class = "ScrollingFrame",
            Name = "list",
            BackgroundColor3 = Color3.new(3/255, 39/255, 40/255),
            BorderSizePixel = 0,
            Position = UDim2.new(0, 13, 0, 50),
            Size = UDim2.new(1, -26, 1, -60),
            CanvasSize = UDim2.new(0, 0, 0, 0)
        },
    }, ReqBar = false},
    ["Players"] = {Links = {}, Auto = {}, ReqBar = true},
    ["Miscellaneous"] = {Links = {}, Auto = {}, ReqBar = false},
    ["Explorer"] = {Links = {}, Auto = {}, ReqBar = false, DoNotInclude = true},
    ["Destruction"] = {Links = {}, Auto = {}, ReqBar = false, DoNotInclude = true},
    ["Music"] = {Links = {}, Auto = {}, ReqBar = false, DoNotInclude = true},
    ["Gear"] = {Links = {}, Auto = {}, ReqBar = true, DoNotInclude = true},
    ["FilterMyAss"] = {Links = {}, Auto = {}, ReqBar = true, DoNotInclude = true},
    ["Memes"] = {Links = {}, Auto = {}, ReqBar = true, DoNotInclude = true},
    ["Hats"] = {Links = {}, Auto = {}, ReqBar = true, DoNotInclude = true},
    ["Credits"] = {Links = {}, Auto = {}, ReqBar = false, DoNotInclude = true},
    ["Chatbox"] = {Links = {}, Auto = {}, ReqBar = false, DoNotInclude = true}
}
 
 
--- global definitions ---
pool.define("global","gui", game:GetObjects("rbxassetid://388041033")[1]); local gui = pool.get("global", "gui");
 local expl = pool.get("misc", "explorer")
    local exm = game:GetObjects("rbxassetid://394831698")[1]
    for i, v in pairs(exm:GetChildren()) do
        v.Parent = expl.inner.min
    end
  localexplorer = expl.inner.min.ExplorerPanel 
  localprop = expl.inner.min.PropertiesPanel
  loadstring(localexplorer.LocalScript.Source)()
  loadstring(localprop.Properties.Source)()
