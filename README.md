# TypingWipp
MSG Plugin Sourcecode

package command;

import org.bukkit.Bukkit;
import org.bukkit.command.Command;
import org.bukkit.command.CommandExecutor;
import org.bukkit.command.CommandSender;
import org.bukkit.entity.Player;
import storage.Data;

public class CMD_Msg implements CommandExecutor {
    public boolean onCommand(CommandSender sender, Command cmd, String label, String[] args) {
        if(cmd.getName().equalsIgnoreCase("msg")) {
            if(sender instanceof Player) {
                Player p = (Player) sender;
                String msg = "";

                for (int i = 1; i < args.length; i++) {
                    msg = msg + " " + args[i];
                }

                if (args.length == 1) {
                    p.sendMessage(Data.prefix + "§c Usage: /Msg «Player» «Message»!");
                    return true;
                }

                if (args.length >= 1) {
                    Player t = (Player) Bukkit.getPlayer(args[0]);
                    if (t == null) {
                        p.sendMessage(Data.prefix + "§c Player not found!");
                        return true;
                    }

                    if (t instanceof Player) {

                        p.sendMessage(Data.prefix + " §a" + p.getName() + "§7 --> §b" + t.getName() + " §8» §7" + msg);
                        t.sendMessage(Data.prefix + " §c" + p.getName() + "§7 --> §a" + t.getName() + " §8» §7" + msg);

                    } else {
                        p.sendMessage(Data.prefix + "§c The specified user is not even a player!");
                    }
                } else {
                    p.sendMessage(Data.prefix + "§c Usage: /Msg «Player» «Message»!");
                }
            } else {
                sender.sendMessage(Data.player);
            }
        }
        return false;
    }
}
