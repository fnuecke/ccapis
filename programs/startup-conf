--[[
    BS - Better Startup - 2013 Sangar

    This program is licensed under the MIT license.
    http://opensource.org/licenses/mit-license.php

    This script allows interacting with the startup API via the shell.
]]

assert(os.loadAPI("apis/startup"))

-------------------------------------------------------------------------------
-- Commands                                                                  --
-------------------------------------------------------------------------------

-- List of all commands of this program. Keep the variable declaration
-- separate, so that it can be referenced in the help callback.
local commands
commands = {
    help = {
        help = "Shows the help text for the specified command.",
        args = {{"command", "The command to get help on."}},
        call = function(name)
            local command = commands[name]
            if command == nil then
                print("No such command.")
            else
                print(command.help)
                if command.args and #command.args > 0 then
                    print("Parameters:")
                    for _, arg in ipairs(command.args) do
                        print(" " .. arg[1] .. " - " .. arg[2])
                    end
                end
            end
        end
    },
    add = {
        help = "Adds a startup script by copying a file.",
        args = {
            {"name", "The name of the script."},
            {"priority", "The priority of the script."},
            {"path", "The path to the file."}
        },
        call = function(name, priority, path)
            local success, reason =
                startup.addFile(name, tonumber(priority), path)
            if success then
                print("Successfully installed script.")
            else
                print("Failed installing script: " .. reason)
            end
        end
    },
    remove = {
        help = "Removes a startup script.",
        args = {{"name", "The name of the script."}},
        call = function(name)
            if startup.remove(name) then
                print("Successfully removed script '" .. name .. '".')
            else
                print("Could not remove script '" .. name .. "'.")
            end
        end
    },
    enable = {
        help = "Enables a startup script.",
        args = {{"name", "The name of the script."}},
        call = function(name)
            if startup.enable(name) then
                print("Script '" .. name .. "' is now enabled.")
            else
                print("Could not enable script '" .. name .. "'.")
            end
        end
    },
    disable = {
        help = "Disables a startup script.",
        args = {{"name", "The name of the script."}},
        call = function(name)
            if startup.disable(name) then
                print("Script '" .. name .. "' is now disabled.")
            else
                print("Could not disable script '" .. name .. "'.")
            end
        end
    },
    list = {
        help = "Lists all startup scripts.",
        call = function()
            for name in startup.iter() do
                print(string.format("%s (%2d, %s)",
                    name,
                    startup.getPriority(name),
                    startup.isEnabled(name) and "enabled" or "disabled"))
            end
        end
    },
    run = {
        help = "Runs all enabled startup scripts.",
        call = function()
            startup.run()
        end
    }
}

-------------------------------------------------------------------------------
-- Command logic                                                             --
-------------------------------------------------------------------------------

--[[
    Automatically generates a usage description, based on the command list.
]]
local function usage()
    local programName = fs.getName(shell.getRunningProgram())
    print("Usage: " .. programName .. " <command> <args...>")
    local names = {}
    for name, _ in pairs(commands) do
        table.insert(names, name)
    end
    table.sort(names)
    print("Commands: " .. table.concat(names, ", "))
    print("Use '" .. programName ..
          " help <command>' to get more information on a specific command.")
end

--[[
    Handles command line arguments and executes the corresponding command.
]]
local function run(...)
    local args = {...}
    local command = commands[args[1]]
    if #args == 0 or command == nil then
        usage()
    else
        table.remove(args, 1)
        command.call(unpack(args))
    end
end

-------------------------------------------------------------------------------
-- Initialization                                                            --
-------------------------------------------------------------------------------

run(...)