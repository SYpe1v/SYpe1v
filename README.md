# SYpe1vPlugin

This is a simple plugin for Minecraft that gives a special reward to a player with the username `SYpe1v`.

## Plugin Features

- **Special Reward Command**: When the player `SYpe1v` runs the `/specialreward` command, they receive a custom item (a Legendary Diamond Sword) as a special reward.
- **Broadcasting**: The server broadcasts a message to all players when `SYpe1v` claims their special reward.
- **Permission Check**: Only the player `SYpe1v` can use the `/specialreward` command.

## Installation

1. Download the plugin JAR file.
2. Place the JAR file in your server's `plugins` directory.
3. Restart or reload the server to enable the plugin.

## Commands

### `/specialreward`
- **Usage**: `/specialreward`
- **Permission**: Only available to the player with the username `SYpe1v`.
- **Effect**: Grants a Legendary Diamond Sword to the player `SYpe1v`.

## Code

```java
package com.unique.SYpe1v;

import org.bukkit.Bukkit;
import org.bukkit.ChatColor;
import org.bukkit.Material;
import org.bukkit.command.Command;
import org.bukkit.command.CommandSender;
import org.bukkit.entity.Player;
import org.bukkit.inventory.ItemStack;
import org.bukkit.inventory.meta.ItemMeta;
import org.bukkit.plugin.java.JavaPlugin;

public class SYpe1vPlugin extends JavaPlugin {

    private final String specialUsername = "SYpe1v"; // Username that receives the special reward

    @Override
    public void onEnable() {
        getLogger().info("SYpe1vPlugin has been enabled!");
    }

    @Override
    public void onDisable() {
        getLogger().info("SYpe1vPlugin has been disabled!");
    }

    @Override
    public boolean onCommand(CommandSender sender, Command command, String label, String[] args) {
        if (command.getName().equalsIgnoreCase("specialreward")) {
            if (sender instanceof Player) {
                Player player = (Player) sender;

                // Check if the player is "SYpe1v"
                if (player.getName().equalsIgnoreCase(specialUsername)) {
                    // Create a special item (diamond sword with custom name and enchantments)
                    ItemStack specialSword = new ItemStack(Material.DIAMOND_SWORD, 1);
                    ItemMeta meta = specialSword.getItemMeta();

                    if (meta != null) {
                        meta.setDisplayName(ChatColor.GOLD + "Legendary Sword of SYpe1v");
                        specialSword.setItemMeta(meta);
                    }

                    // Give the special item to the player
                    player.getInventory().addItem(specialSword);
                    player.sendMessage(ChatColor.GREEN + "You have received your special reward!");

                    // Broadcast message to the server
                    Bukkit.broadcastMessage(ChatColor.AQUA + "SYpe1v has claimed their special reward!");
                } else {
                    // Inform other players that only "SYpe1v" can use this command
                    player.sendMessage(ChatColor.RED + "Only SYpe1v can use this command!");
                }
                return true;
            }
        }
        return false;
    }
}
