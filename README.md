Code
====
public class TokensEventHandlers implements Listener{
	
	@EventHandler
	public void onJoin(PlayerJoinEvent e) {
	Player p = e.getPlayer();
	if(!Tokens.config.contains(p.getName())){
		Tokens.config.set(p.getName() + ".Tokens", 0);
	}
		}
	
	@EventHandler
	public void onVote(VotifierEvent event){
		Vote vote = event.getVote();
		String p = vote.getUsername();
		Player player = Bukkit.getPlayer(p);
		Bukkit.getServer().broadcastMessage(vote.getUsername() + " has voted on " + vote.getServiceName());
		Bukkit.getServer().broadcastMessage(ChatColor.RED + "Remember To Vote By Typing" + ChatColor.GREEN + "/Vote" + ChatColor.RED + "!");
		player.sendMessage(ChatColor.GREEN + "Thanks For Voting " + player.getName() + ChatColor.GREEN + " !");
		player.sendMessage(ChatColor.GREEN + "Type " + ChatColor.RED + "/Shop" + ChatColor.GREEN + " To Spend Your Tokens!");
		player.sendMessage(ChatColor.GREEN + "Type " + ChatColor.RED + "/Tokens" + ChatColor.GREEN + " To See Your Current Balance!");
		TokensAPI.givetokens(player, 1);
	}
	
	@EventHandler
	public void onClick(InventoryClickEvent event) {
	Player p = (Player) event.getWhoClicked();
	
	//body
	if(event.getInventory().getName().equals(Tokens.Shop.getName())){
		event.setCancelled(true);
		if(event.getCurrentItem() == null){
			return;
		}
		if(!event.getCurrentItem().hasItemMeta()){
			return;
			}
		
		if(event.getCurrentItem().getType() == Material.DIAMOND_HELMET){
			if(TokensAPI.hasEnough(p, 10)){
				TokensAPI.taketokens(p, 10);
			ItemStack thelmet = new ItemStack(Material.DIAMOND_HELMET, 1);
			thelmet.addUnsafeEnchantment(Enchantment.PROTECTION_ENVIRONMENTAL, 4);
			p.getInventory().addItem(thelmet);
			}else{
				p.sendMessage(ChatColor.RED + "You`re To Poor!");
			}
		}
		if(event.getCurrentItem().getType() == Material.DIAMOND_CHESTPLATE){
			if(TokensAPI.hasEnough(p, 10)){
				TokensAPI.taketokens(p, 10);
			ItemStack thelmet1 = new ItemStack(Material.DIAMOND_CHESTPLATE, 1);
			thelmet1.addUnsafeEnchantment(Enchantment.PROTECTION_ENVIRONMENTAL, 4);
			p.getInventory().addItem(thelmet1);
		}else{
			p.sendMessage(ChatColor.RED + "You`re To Poor!");
		}
		}
		if(event.getCurrentItem().getType() == Material.DIAMOND_LEGGINGS){
			if(TokensAPI.hasEnough(p, 10)){
				TokensAPI.taketokens(p, 10);
			ItemStack thelmet2 = new ItemStack(Material.DIAMOND_LEGGINGS, 1);
			thelmet2.addUnsafeEnchantment(Enchantment.PROTECTION_ENVIRONMENTAL, 4);
			p.getInventory().addItem(thelmet2);
		}else{
			p.sendMessage(ChatColor.RED + "You`re To Poor!");
		}
		}
		if(event.getCurrentItem().getType() == Material.DIAMOND_BOOTS){
			if(TokensAPI.hasEnough(p, 10)){
				TokensAPI.taketokens(p, 10);
			ItemStack thelmet3 = new ItemStack(Material.DIAMOND_BOOTS, 1);
			thelmet3.addUnsafeEnchantment(Enchantment.PROTECTION_ENVIRONMENTAL, 4);
			p.getInventory().addItem(thelmet3);
		}else{
			p.sendMessage(ChatColor.RED + "You`re To Poor!");
		}
		}
		if(event.getCurrentItem().getType() == Material.DIAMOND_PICKAXE){
			if(TokensAPI.hasEnough(p, 50)){
				TokensAPI.taketokens(p, 50);
			ItemStack thelmet4 = new ItemStack(Material.DIAMOND_PICKAXE, 1);
			thelmet4.addUnsafeEnchantment(Enchantment.DIG_SPEED, 30);
			thelmet4.addUnsafeEnchantment(Enchantment.DURABILITY, 9999);
			thelmet4.addUnsafeEnchantment(Enchantment.LOOT_BONUS_BLOCKS, 6);
			p.getInventory().addItem(thelmet4);
		}else{
			p.sendMessage(ChatColor.RED + "You`re To Poor!");
		}
		}
		if(event.getCurrentItem().getType() == Material.DIAMOND_SWORD){
			if(TokensAPI.hasEnough(p, 20)){
				TokensAPI.taketokens(p, 20);
			ItemStack thelmet5 = new ItemStack(Material.DIAMOND_SWORD, 1);
			thelmet5.addUnsafeEnchantment(Enchantment.DAMAGE_ALL, 5);
			thelmet5.addUnsafeEnchantment(Enchantment.FIRE_ASPECT, 2);
			p.getInventory().addItem(thelmet5);
		}else{
			p.sendMessage(ChatColor.RED + "You`re To Poor!");
		}
		}
		if(event.getCurrentItem().getType() == Material.GOLDEN_APPLE){
			if(TokensAPI.hasEnough(p, 20)){
				TokensAPI.taketokens(p, 20);
			ItemStack thelmet6 = new ItemStack(Material.GOLDEN_APPLE, 5, (short) 1);
			p.getInventory().addItem(thelmet6);
		}else{
			p.sendMessage(ChatColor.RED + "You`re To Poor!");
		}
		}
	}
	}
}












public class Voting implements VoteListener{

	public void voteMade(Vote vote) {
		Player p = Bukkit.getServer().getPlayer(vote.getUsername());
		 System.out.println("Received: " + vote);
		 Bukkit.getServer().dispatchCommand(Bukkit.getServer().getConsoleSender(), "tokensgive " + p + " ");
		
	}











public class Tokens extends JavaPlugin implements Listener{
	
	public static FileConfiguration config;

	public static Tokens plugin = null;
	
	public void onEnable(){
		getLogger().info("Tokens has been Enabled!");
		getLogger().info("Author Badboy123101!!");
		getServer().getPluginManager().registerEvents(new TokensEventHandlers(), this);
		config = getConfig();
		plugin = this;
	}
	public void onDisable(){
		getLogger().info("Tokens has been Disabled!");
	}
	public static void saveFile(){
		plugin.saveConfig();
		}
	//items for inventories
	ItemStack dhel = new ItemStack(Material.DIAMOND_HELMET);
	{
	ItemMeta itemmeta = dhel.getItemMeta();
	ArrayList<String> im = new ArrayList<String>();
	itemmeta.setDisplayName("§4§lTokens Helmet!");
	im.add("§a§l10 Tokens!");
	itemmeta.addEnchant(Enchantment.PROTECTION_ENVIRONMENTAL, 4, true);
	im.add(ChatColor.LIGHT_PURPLE + "Mc" + ChatColor.GREEN + "Prison" + ChatColor.GOLD + "Break" + ChatColor.RED + "!");;
	itemmeta.setLore(im);
	dhel.setItemMeta(itemmeta);
	}
	ItemStack dchest = new ItemStack(Material.DIAMOND_CHESTPLATE);
	{
	ItemMeta itemmeta = dchest.getItemMeta();
	ArrayList<String> im = new ArrayList<String>();
	itemmeta.setDisplayName("§4§lTokens ChestPlate!");
	im.add("§a§l10 Tokens!");
	itemmeta.addEnchant(Enchantment.PROTECTION_ENVIRONMENTAL, 4, true);
	im.add(ChatColor.LIGHT_PURPLE + "Mc" + ChatColor.GREEN + "Prison" + ChatColor.GOLD + "Break" + ChatColor.RED + "!");;
	itemmeta.setLore(im);
	dchest.setItemMeta(itemmeta);
	}
	ItemStack dleg = new ItemStack(Material.DIAMOND_LEGGINGS);
	{
	ItemMeta itemmeta = dleg.getItemMeta();
	ArrayList<String> im = new ArrayList<String>();
	itemmeta.setDisplayName("§4§lTokens Leggings!");
	im.add("§a§l10 Tokens!");
	itemmeta.addEnchant(Enchantment.PROTECTION_ENVIRONMENTAL, 4, true);
	im.add(ChatColor.LIGHT_PURPLE + "Mc" + ChatColor.GREEN + "Prison" + ChatColor.GOLD + "Break" + ChatColor.RED + "!");;
	itemmeta.setLore(im);
	dleg.setItemMeta(itemmeta);
	}
	ItemStack dboot = new ItemStack(Material.DIAMOND_BOOTS);
	{
	ItemMeta itemmeta = dboot.getItemMeta();
	ArrayList<String> im = new ArrayList<String>();
	itemmeta.setDisplayName("§4§lTokens Boots!");
	im.add("§a§l10 Tokens!");
	itemmeta.addEnchant(Enchantment.PROTECTION_ENVIRONMENTAL, 4, true);
	im.add(ChatColor.LIGHT_PURPLE + "Mc" + ChatColor.GREEN + "Prison" + ChatColor.GOLD + "Break" + ChatColor.RED + "!");;
	itemmeta.setLore(im);
	dboot.setItemMeta(itemmeta);
	}
	ItemStack dpick = new ItemStack(Material.DIAMOND_PICKAXE);
	{
	ItemMeta itemmeta = dpick.getItemMeta();
	ArrayList<String> im = new ArrayList<String>();
	itemmeta.setDisplayName("§4§lTokens Pickaxe!");
	im.add("§a§l50 Tokens!");
	itemmeta.addEnchant(Enchantment.DIG_SPEED, 30, true);
	itemmeta.addEnchant(Enchantment.DURABILITY, 9999, true);
	itemmeta.addEnchant(Enchantment.LOOT_BONUS_BLOCKS, 6, true);
	im.add(ChatColor.LIGHT_PURPLE + "Mc" + ChatColor.GREEN + "Prison" + ChatColor.GOLD + "Break" + ChatColor.RED + "!");;
	itemmeta.setLore(im);
	dpick.setItemMeta(itemmeta);
	}
	ItemStack dsword = new ItemStack(Material.DIAMOND_SWORD);
	{
	ItemMeta itemmeta = dsword.getItemMeta();
	ArrayList<String> im = new ArrayList<String>();
	itemmeta.setDisplayName("§4§lTokens Sword!");
	im.add("§a§l20 Tokens!");
	itemmeta.addEnchant(Enchantment.DAMAGE_ALL, 5, true);
	itemmeta.addEnchant(Enchantment.FIRE_ASPECT, 2, true);
	im.add(ChatColor.LIGHT_PURPLE + "Mc" + ChatColor.GREEN + "Prison" + ChatColor.GOLD + "Break" + ChatColor.RED + "!");;
	itemmeta.setLore(im);
	dsword.setItemMeta(itemmeta);
	}
	ItemStack apple = new ItemStack(Material.GOLDEN_APPLE, 5, (short) 1);
	{
	ItemMeta itemmeta = apple.getItemMeta();
	ArrayList<String> im = new ArrayList<String>();
	itemmeta.setDisplayName("§4§lTokens Apples!");
	im.add("§a§l20 Tokens!");
	im.add(ChatColor.LIGHT_PURPLE + "Mc" + ChatColor.GREEN + "Prison" + ChatColor.GOLD + "Break" + ChatColor.RED + "!");;
	itemmeta.setLore(im);
	apple.setItemMeta(itemmeta);
	}
	//Inventories
	public static Inventory Shop;
	{
		Shop = Bukkit.createInventory(null, 9, "§a§nTokens Shop!");
		Shop.addItem(dhel);
		Shop.addItem(dchest);
		Shop.addItem(dleg);
		Shop.addItem(dboot);
		Shop.addItem(dpick);
		Shop.addItem(dsword);
		Shop.addItem(apple);
	}
	//Commands
	public boolean onCommand(CommandSender sender, Command cmd, String label,String[] args) {
		Player p = (Player) sender;
		if(cmd.getName().equalsIgnoreCase("shop")){
			p.sendMessage(ChatColor.GREEN + "You Have Now Opened The Token Shop!");
			p.openInventory(Shop);
			return true;
		}
		if(cmd.getName().equalsIgnoreCase("tokensgiveop")){
			if(p.hasPermission("tokens.giveop")){
				if(args.length == 1){
					Player player = Bukkit.getServer().getPlayer(args[0]);
					TokensAPI.givetokens(player, 1000);
			 }else{
				 p.sendMessage(ChatColor.RED + "Incorrect Aruguments!");
			 }
				return true;
			}
		}
		if(cmd.getName().equalsIgnoreCase("tokensgive")){
			if(p.hasPermission("tokens.give")){
				if(args.length == 1){
					Player player = Bukkit.getServer().getPlayer(args[0]);
					TokensAPI.givetokens(player, 1);
			 }else{
				 p.sendMessage(ChatColor.RED + "Incorrect Aruguments!");
			 }
				return true;
			}
		}
		if(label.equalsIgnoreCase("tokens")){
			p.sendMessage("§aYour Current Balance Is:§2 " + getConfig().getInt(p.getName() + ".Tokens"));
			
			return true;
		}
		if(cmd.getName().equalsIgnoreCase("pl")){
			p.sendMessage(ChatColor.WHITE + "Plugin (1): " + ChatColor.GREEN + "McPrisonBreak");
			return true;
		}
		if(cmd.getName().equalsIgnoreCase("plugins")){
			p.sendMessage(ChatColor.WHITE + "Plugin (1): " + ChatColor.GREEN + "McPrisonBreak");
			return true;
		}
		
		
		
	return false;	
	}
	
}









public class TokensAPI {
	public static void givetokens(Player p, int i) {
		Tokens.config.set(p.getName() + ".Tokens",
		Tokens.config.getInt(p.getName() + ".Tokens", 0) + i);
		Tokens.saveFile();
p.sendMessage("§2§l$" + i + " Tokens received!");
}

public static void taketokens(Player p, int i) {
	Tokens.config.set(p.getName() + ".Tokens",
Tokens.config.getInt(p.getName() + ".Tokens", 0) - i);
Tokens.saveFile();
p.sendMessage("§c§l$" + i + " Tokens taken!");
}


public static boolean hasEnough(Player p, int i) {
if (Tokens.config.getInt(p.getName() + ".Tokens") >= i)
return true;
return false;
}
}













