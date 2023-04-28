# Variable Launcher - API Documentation

#### Functions
```
getContext();
print(String text);
preventDefault();
getScreenName();
```
---
#### Data
##### Static methods:
```
Data.getString(String key, String defaultValue);
Data.getNumber(String key, double defaultValue);
Data.getBoolean(String key, boolean defaultValue);

Data.saveString(String key, String value);
Data.saveNumber(String key, double value);
Data.saveBoolean(String key, boolean value);

Data.remove(String key);
Data.clear();
```
##### Example: ....
---

#### Module
##### Constructor: `Module(String name, boolean toggleable, boolean bindable, String category)`
##### Methods:
```
Module.getName();
Module.isToggleable();
Module.isBindable();
Module.getCategory();
Module.isActive();
Module.isBindActive();
Module.hasSettings();
Module.getSetting(String name);
Module.getSettings();
Module.addSetting(Setting setting);
Module.addSettings(Setting[] settings);

Module.setOnToggleListener(function(View view, boolean active));
Module.setOnClickListener(function(View view));
```
##### Static methods:
```
Module.isToggleable(String moduleName);
Module.isBindable(String moduleName);
Module.getCategory(String moduleName);
Module.isActive(String moduleName);
Module.isBindActive(String moduleName);
Module.hasSettings(String moduleName);
Module.getSettingNames(String moduleName);
Module.addSetting(String moduleName, Setting setting);
Module.addSettings(String moduleName, Setting[] settings);
```
##### Example: ...
---
#### ModuleManager
##### Static methods:<br/>
```
ModuleManager.addModule(Module module);
ModuleManager.addModules(Modules[] modules);
ModuleManager.removeModule(Module module);
ModuleManager.getModuleNames();
```
##### Example: ...
---
#### Setting
##### Static methods:
```
Setting.getType(String moduleName, String settingName);
Setting.isVisible(String moduleName, String settingName);
Setting.setVisibility(String moduleName, String settingName, boolean visibility);
Setting.getCurrentMode(String moduleName, String settingName); // Для настроек типа "mode"
Setting.getCurrentValue(String moduleName, String settingName); // Для настроек типа "slider"
Setting.isActive(String moduleName, String settingName); // Для настроек типа "state"
Setting.getText(String moduleName, String settingName); // Для настроек типа "text-field"
```
##### Example: ...
---
#### ButtonSetting
##### Constructor: `ButtonSetting(String name, function(View view));`
##### Methods:
```
ButtonSetting.getName();
ButtonSetting.getType();
ButtonSetting.isVisible();
ButtonSetting.setVisibility(boolean visibility);
```
##### Example: ...
---
#### ModeSetting
##### Constructor: `ModeSetting(String name, String[] modes);`
##### Methods:
```
ModeSetting.getName();
ModeSetting.getType();
ModeSetting.isVisible();
ModeSetting.setVisibility(boolean visibility);

ModeSetting.getCurrentMode();
ModeSetting.setOnModeSelectedListener(function(String mode));
```
##### Example: ...
---
#### SliderSetting
##### Constructor: `SliderSetting(String name, [double default, double min, double max, double step]);`
##### Methods:
```
SliderSetting.getName();
SliderSetting.getType();
SliderSetting.isVisible();
SliderSetting.setVisibility(boolean visibility);

SliderSetting.getCurrentValue();
SliderSetting.setOnCurrentValueChangedListener(function(double currentValue));
```
##### Example: ...
---
#### StateSetting
##### Constructor: `StateSetting(String name, boolean state);`
##### Methods:
```
StateSetting.getName();
StateSetting.getType();
StateSetting.isVisible();
StateSetting.setVisibility(boolean visibility);

StateSetting.isActive();
StateSetting.setOnStateToggleListener(function(boolean state));
```
##### Example: ...
---
#### TextFieldSetting
##### Constructor: `TextFieldSetting(String name, String hint, String text);`
##### Methods:
```
TextFieldSetting.getName();
TextFieldSetting.getType();
TextFieldSetting.isVisible();
TextFieldSetting.setVisibility(boolean visibility);

TextFieldSetting.getText();
TextFieldSetting.setOnTextChangedListener(function(String text));
```
##### Example: ...
---
#### Level
##### Static methods:
```
Level.getAddress();
Level.getPort();
Level.getAllPlayers();
Level.getTime();
Level.getGameSpeed();

Level.setTime(int time);
Level.setGameSpeed(double speed);

Level.setTitle(String text);
Level.setSubtitle(String text);
Level.displayClientMessage(String text);
Level.showTipMessage(String text);
```
##### Example: ...
---
#### LocalPlayer
##### Static methods:
```
LocalPlayer.getUniqueID();
LocalPlayer.getPointedPlayer();
LocalPlayer.getPointedVector();
LocalPlayer.attack(int playerID);
LocalPlayer.attackTp(int playerID);
LocalPlayer.click(boolean rightClick);
LocalPlayer.longClick();
LocalPlayer.buildBlock(int x, int y, int z, int side);
LocalPlayer.destroyBlock(int x, int y, int z);
LocalPlayer.openContainer(int x, int y, int z);
LocalPlayer.openInventory();
LocalPlayer.closeScreen(); // опасно, может "закрыть" даже рендер всей игры
LocalPlayer.sendChatMessage(String text);
LocalPlayer.isMoveButtonPressed(int id);
LocalPlayer.setStepHeight(double height);
LocalPlayer.setOnGround(boolean onGround);
LocalPlayer.setSprinting(boolean sprinting);
LocalPlayer.setStatusFlag(int flag, boolean status);
LocalPlayer.addEffect(int id, int duration, int amplifier, boolean showParticles);
LocalPlayer.removeEffect(int id);
LocalPlayer.setRot(double yaw, double pitch);

LocalPlayer.setPosition(double x, double y, double z);
LocalPlayer.setPositionX(double x);
LocalPlayer.setPositionY(double y);
LocalPlayer.setPositionZ(double z);
LocalPlayer.setPositionRelative(double x, double y, double z);
LocalPlayer.setPositionRelativeX(double x);
LocalPlayer.setPositionRelativeY(double y);
LocalPlayer.setPositionRelativeZ(double z);

LocalPlayer.setMotion(double x, double y, double z);
LocalPlayer.setMotionX(double x);
LocalPlayer.setMotionY(double y);
LocalPlayer.setMotionZ(double z);

LocalPlayer.isInGame();
LocalPlayer.getViewPerspective();
LocalPlayer.setViewPerspective(int view);
LocalPlayer.getDistanceTo(int playerID);
LocalPlayer.getDistanceToCoords(double x, double y, double z);
LocalPlayer.getNearestPlayer(double radius);
LocalPlayer.lookAt(int playerID);
LocalPlayer.smoothLookAt(int playerID, double smooth);

LocalPlayer.getNameTag();
LocalPlayer.getHealth();
LocalPlayer.getYaw();
LocalPlayer.getPitch();
LocalPlayer.getPositionX();
LocalPlayer.getPositoinY();
LocalPlayer.getPositionZ();
LocalPlayer.getMotionX();
LocalPlayer.getMotionY();
LocalPlayer.getMotionZ();
LocalPlayer.getCollisionSize();
LocalPlayer.getStatusFlag(int flag);
LocalPlayer.getFallDistance();
LocalPlayer.isInCreativeMode();
LocalPlayer.isInLava();
LocalPlayer.isInvisible();
LocalPlayer.isInWall();
LocalPlayer.isInWater();
LocalPlayer.isInWorld();
LocalPlayer.isOnFire();
LocalPlayer.isOnGround();
LocalPlayer.isFalling();
LocalPlayer.isImmobile();
LocalPlayer.isSitting();
LocalPlayer.isSneaking();
LocalPlayer.isMoving();
LocalPlayer.isAlive();
LocalPlayer.isOnLadder();
LocalPlayer.canFly();
LocalPlayer.canShowNameTag();
```
##### Example: ...
---
#### Inventory (of LocalPlayer)
##### Static methods:
```
Inventory.swapSlots(int fromSlot, int toSlot);
Inventory.dropSlot(int slot, boolean dropAll, boolean deleteDrop);
Inventory.clearSlot(int slot);
Inventory.getSelectedSlot();
Inventory.getOffhandSlot();
Inventory.getArmor(int armorSlot);
Inventory.setSelectedSlot(int slot);
Inventory.setArmor(int slot, int armorSlot);
```
##### Example: ...
---
#### Item (from Inventory)
##### Static methods:
```
Item.getID(int slot);
Item.getData(int slot);
Item.getName(int slot);
Item.getUseDuration(int slot);
Item.getMaxStackSize(int slot);
Item.getMaxDamage(int slot);
Item.getDamage(int slot);
Item.getCount(int slot);
Item.isArmor(int slot);
Item.isBlock(int slot);
Item.isDamageable(int slot);
Item.isStackable(int slot);
Item.isFullStack(int slot);
Item.isThrowable(int slot);
Item.isDamaged(int slot);
Item.isEnchantingBook(int slot);
Item.isPotion(int slot);
Item.isEnchanted(int slot);
Item.setUseDuration(int slot, int duration);
Item.setCount(int slot, int count);
```
##### Example: ...
---
#### Player
##### Static methods:
```
Player.isLocalPlayer(int playerID);
Player.getNameTag(int playerID);
Player.getHealth(int playerID);
Player.getYaw(int playerID);
Player.getPitch(int playerID);
Player.getPositionX(int playerID);
Player.getPositoinY(int playerID);
Player.getPositionZ(int playerID);
Player.getMotionX(int playerID);
Player.getMotionY(int playerID);
Player.getMotionZ(int playerID);
Player.getCollisionSize(int playerID);
Player.setCollisionSize(int playerID, double horizontal, double vertical);
Player.setShadowRadius(int playerID, double radius);
Player.getStatusFlag(int playerID, int flag);
Player.getFallDistance(int playerID);
Player.isInCreativeMode(int playerID);
Player.isInLava(int playerID);
Player.isInvisible(int playerID);
Player.isInWall(int playerID);
Player.isInWater(int playerID);
Player.isInWorld(int playerID);
Player.isOnFire(int playerID);
Player.isOnGround(int playerID);
Player.isFalling(int playerID);
Player.isImmobile(int playerID);
Player.isSitting(int playerID);
Player.isSneaking(int playerID);
Player.isMoving(int playerID);
Player.isAlive(int playerID);
Player.isOnLadder(int playerID);
Player.canFly(int playerID);
Player.canShowNameTag(int playerID);
```
##### Example: ...
---
#### Block
##### Static methods:
```
Block.getID(int x, int y, int z);
Block.getBrightness(int x, int y, int z);
Block.getFriction(int x, int y, int z);
Block.isSolid(int x, int y, int z);
Block.isContainer(int x, int y, int z);
Block.isInteractive(int x, int y, int z);
Block.setFriction(int x, int y, int z);
Block.setDestroyTime(int x, int y, int z, double time);
```
##### Example: ...
---
#### Memory (ТОЛЬКО ДЛЯ ОСОБО УМНЫХ)
##### Static methods:
```
Memory.patch(int address, int[] patch);
Memory.getLibrary();
Memory.getSymbol(String symbol);
Memory.getPlayer(int playerID);
Memory.getLocalPlayer();
Memory.getGameMode();
Memory.getHitResult();
Memory.getLevel();
Memory.getDimension();
Memory.getLevelRenderer();
Memory.getOptions();
Memory.getTimer();

Memory.getString(int address, int offset);
Memory.getBoolean(int address, int offset);
Memory.getInt(int address, int offset);
Memory.getFloat(int address, int offset);
Memory.getChar(int address, int offset);

Memory.setString(int address, int offset, String value);
Memory.setBoolean(int address, int offset, boolean value);
Memory.setInt(int address, int offset, int value);
Memory.setFloat(int address, int offset, float value);
Memory.setChar(int address, int offset, char value);
```
##### Example: ...
---
### Constant classes
#### ModuleCategory
```
ModuleCategory.COMBAT
ModuleCategory.MOVEMENT
ModuleCategory.PLAYER
ModuleCategory.MISC
ModuleCategory.OTHER
```
---
#### BlockSide
```
BlockSide.DOWN
BlockSide.UP
BlockSide.NORTH
BlockSide.SOUTH
BlockSide.WEST
BlockSide.EAST
```
---
#### PacketType
```
PacketType.ADD_BEHAVIOR_TREE_PACKET
PacketType.ADD_ENTITY_PACKET
PacketType.ADD_ITEM_ENTITY_PACKET
PacketType.ADD_ITEM_PACKET
PacketType.ADD_PAINTING_PACKET
PacketType.ADD_PLAYER_PACKET
PacketType.ADVENTURE_SETTINGS_PACKET
PacketType.ANIMATE_PACKET
PacketType.AVAILABLE_COMMANDS_PACKET
PacketType.BLOCK_ENTITY_DATA_PACKET
PacketType.BLOCK_EVENT_PACKET
PacketType.BLOCK_PICK_REQUEST_PACKET
PacketType.BOSS_EVENT_PACKET
PacketType.CAMERA_PACKET
PacketType.CHANGE_DIMENSION_PACKET
PacketType.CHUNK_RADIUS_UPDATED_PACKET
PacketType.CLIENT_TO_SERVER_HANDSHAKE_PACKET 
PacketType.COMMAND_BLOCK_UPDATE_PACKET
PacketType.CONTAINER_CLOSE_PACKET
PacketType.CONTAINER_OPEN_PACKET
PacketType.CONTAINER_SET_CONTENT_PACKET
PacketType.CONTAINER_SET_DATA_PACKET
PacketType.CONTAINER_SET_SLOT_PACKET
PacketType.CRAFTING_DATA_PACKET
PacketType.CRAFTING_EVENT_PACKET
PacketType.DISCONNECT_PACKET
PacketType.DROP_ITEM_PACKET
PacketType.ENTITY_EVENT_PACKET
PacketType.ENTITY_FALL_PACKET
PacketType.EXPLODE_PACKET
PacketType.FULL_CHUNK_DATA_PACKET
PacketType.GAME_RULES_CHANGED_PACKET
PacketType.HURT_ARMOR_PACKET
PacketType.INVENTORY_ACTION_PACKET
PacketType.INTERACT_PACKET
PacketType.ITEM_FRAME_DROP_ITEM_PACKET
PacketType.LEVEL_EVENT_PACKET
PacketType.LEVEL_SOUND_EVENT_PACKET
PacketType.LOGIN_PACKET
PacketType.MAP_INFO_REQUEST_PACKET
PacketType.MINING_FATIGUE_PARTICLE
PacketType.MOB_ARMOR_EQUIPMENT_PACKET
PacketType.MOB_EFFECT_PACKET
PacketType.MOB_EQUIPMENT_PACKET
PacketType.MOVE_ENTITY_PACKET
PacketType.MOVE_PLAYER_PACKET
PacketType.PLAYER_ACTION_PACKET
PacketType.PLAYER_INPUT_PACKET
PacketType.PLAYER_LIST_PACKET
PacketType.PLAY_SOUND_PACKET
PacketType.PLAY_STATUS_PACKET
PacketType.PURCHASE_RECEIPT_PACKET
PacketType.REMOVE_BLOCK_PACKET
PacketType.REMOVE_ENTITY_PACKET
PacketType.REPLACE_ITEM_IN_SLOT_PACKET
PacketType.REQUEST_CHUNK_RADIUS_PACKET
PacketType.RESPAWN_PACKET
PacketType.RESOURCE_PACK_CHUNK_DATA_PACKET
PacketType.RESOURCE_PACK_CHUNK_REQUEST_PACKET
PacketType.RESOURCE_PACK_DATA_INFO_PACKET
PacketType.RESOURCE_PACK_STACK_PACKET
PacketType.RESOURCE_PACKS_INFO_PACKET
PacketType.RIDER_JUMP_PACKET
PacketType.SERVER_TO_CLIENT_HANDSHAKE_PACKET 
PacketType.SET_COMMANDS_ENABLED_PACKET
PacketType.SET_DIFFICULTY_PACKET
PacketType.SET_ENTITY_DATA_PACKET
PacketType.SET_ENTITY_LINK_PACKET
PacketType.SET_ENTITY_MOTION_PACKET
PacketType.SET_HEALTH_PACKET
PacketType.SET_PLAYER_GAME_TYPE_PACKET
PacketType.SET_TIME_PACKET
PacketType.SET_TITLE_PACKET
PacketType.SHOW_CREDITS_PACKET
PacketType.SHOW_STORE_OFFER_PACKET
PacketType.SIMPLE_EVENT_PACKET
PacketType.SPAWN_EXPERIENCE_ORB_PACKET
PacketType.START_GAME_PACKET
PacketType.STOP_SOUND_PACKET
PacketType.STRUCTURE_BLOCK_UPDATE_PACKET
PacketType.TAKE_ITEM_ENTITY_PACKET
PacketType.TEXT_PACKET
PacketType.TRANSFER_PACKET
PacketType.UPDATE_ATTRIBUTES_PACKET
PacketType.UPDATE_BLOCK_PACKET
PacketType.UPDATE_EQUIP_PACKET
PacketType.UPDATE_TRADE_PACKET
PacketType.USE_ITEM_PACKET
```
---
#### Hooks
```
onFastTick();
onLevelTick();
onAttack(int playerID);
onPlayerAdded(int playerID);
onUseItem(int x, int y, int z, int side);
onTeleport(int playerID, int x, int y, int z);
onChat(String text);
onScreenChange(String screen);
onServerConnect(String address, int port);
onServerDisconnect();
onSendPacket(String name, int address);
```
##### Example: ...
