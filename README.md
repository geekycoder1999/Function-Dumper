-- Made by Green_Sharpies

local function isLuaFunction(value)
    return type(value) == "function" and islclosure(value) and not is_synapse_function(value)
end

local function grabFunctionsByConstants(...)
    local functions = {}
    local constantsToFind = {...}
    
    for _, func in pairs(getgc()) do
        if isLuaFunction(func) then
            local constants = getconstants(func)
            local foundAllConstants = true
            
            for _, const in pairs(constantsToFind) do
                if not table.find(constants, const) then
                    foundAllConstants = false
                    break
                end
            end
            
            if foundAllConstants then
                table.insert(functions, func)
            end
        end
    end
    
    return functions
end


local chatFuncs = grabFunctionsByConstants("", "Filtered", "Clan")

for i, func in ipairs(chatFuncs) do
    print("Chat Function #" .. i)
    print(func)
end
