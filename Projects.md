# Masterzz Portfolio ( Lua Side Only )

## Lua APIs

<details>
<summary> 
    A stock tracking API that would track multiple sites to get stock value ( has dynamic support for indexs and crypto aswell )
</summary>

![Api's data response](https://i.imgur.com/BKTpzdT.png)
<p> Api's data response <\p>

![Api's data response into a UI](https://i.imgur.com/kHHuwzg.png)
<p> Api's data response into a UI using price map<\p>

![Api's data response using multiple at onace](https://i.imgur.com/Rqut7Lg.png)
<p> Api's data response using multiple at onace <\p>

</details>

## Script fixing

<details>
<summary> 
    I had a friend which created a function to sub out a player's currency value and would convert to it's true number ( E.g. "10.5m" -> "1000000" ) 
</summary>

<p> 

Friends code.
```lua
function getAmt(value)
local b = ''
if tonumber(value) then
    return  tonumber(value)
end
if (string.lower(value):match('m') or string.lower(value):match('k') or string.lower(value):match('b')) then
    local a = string.lower(value):split('')
    for i=1, #a do
        if (a[i] ~= 'm' or a[i] ~= 'M') and a[i] ~= nil and a[i] ~= '' then
            b = ''..b..a[i]
        elseif (a[i] ~= 'm' or a[i] ~= 'M') and tonumber(b) then
            return tonumber(b) * 1000000
        end
        if (a[i] ~= 'b' or a[i] ~= 'B') and a[i] ~= nil and a[i] ~= '' then
            b = ''..b..a[i]
        elseif (a[i] ~= 'b' or a[i] ~= 'B') and tonumber(b) then
            return tonumber(b) * 1000000000
        end
        if (a[i] ~= 'k' or a[i] ~= 'K') and a[i] ~= nil and a[i] ~= '' then
            b = ''..b..a[i]
        elseif (a[i] ~= 'k' or a[i] ~= 'K') and tonumber(b) then
            return tonumber(b) * 1000
        end
    end
end
```

My fix for his code.
```lua
function getAmt(value)
    for i,v in pairs(string.split(string.lower(value),'')) do 
        if v == 'm' then
            return tonumber(string.match(value, "([+-]?%d*%.?%d+)%.?")) * 10^6
        elseif v == 'k' then
            return tonumber(string.match(value, "([+-]?%d*%.?%d+)%.?")) * 10^3
        elseif v == 'b' then
            return tonumber(string.match(value, "([+-]?%d*%.?%d+)%.?")) * 10^9
        end
    end
end
```
</p>
</details>
