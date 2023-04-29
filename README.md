# Variable Launcher - API Documentation

#### Здесь описаны все функции, классы с их методами и хуки которые предоставляет API лаунчера Variable.
###### Я знаю что это трудно назвать документацией. Буду приводить эту хуйню в порядок до тех пор, пока сам не буду доволен.

- [Глобальные функции](#глобальные-функции)
- [Data](#data)
- [Module](#module)
- [ModuleManager](#modulemanager)
- [Setting](#setting)
- [ButtonSetting](#buttonsetting)
- [ModeSetting](#modesetting)
- [SliderSetting](#slidersetting)
- [StateSetting](#statesetting)
- [TextFieldSetting](#textfieldsetting)
- [Level](#level)
- [LocalPlayer](#localplayer)
- [Inventory](#inventory)
- [Item](#item)
- [Player](#player)
- [Block](#block)
- [Memory](#memory)
- [Константые классы](#константные-классы)
  - [ModuleCategory](#modulecategory)
  - [BlockSide](#blockside)
  - [PacketType](#packettype)
- [Hooks](#hooks)

## Глобальные функции
- `getContext();` - возвращает контекст приложения.
- `print(String text);` - выводит контекстное сообщение.
- `preventDefault();` - в зависимости от места вызова, отменяет вызов [хука](#hooks).
- `getScreenName();` - возвращает название игрового экрана.

## Data
###### Класс для сохранения любых данных скрипта в корневой папке приложения
##### Статические методы

- `Data.getString(String key, String defaultValue);` - ищет строку с ключом `key` и возвращает `defaultValue` если не находит его.
- `Data.getNumber(String key, double defaultValue);` - ищет число с ключом `key` и возвращает `defaultValue` если не находит его.
- `Data.getBoolean(String key, boolean defaultValue);` - ищет логическое значение (true/false) с ключом `key` и возвращает `defaultValue` если не находит его

- `Data.saveString(String key, String value);` - сохраняет строку с ключом `key` и значением `defaultValue`.
- `Data.saveNumber(String key, double value);` - сохраняет число с ключом `key` и значением `defaultValue`.
- `Data.saveBoolean(String key, boolean value);` - сохраняет логическое значение (true/false) с ключом `key` и значением `defaultValue`.

- `Data.remove(String key);` - удаляет значение с ключом `key`
- `Data.clear();` - удаляет все значения скрипта.

##### Примеры: нема

## Module
###### Класс для создания кастомных модулей (функции)
##### Конструктор: `Module(String name, boolean toggleable, boolean bindable, String category)`
##### Методы

- `Module.getName();` - возвращает имя кастомного модуля.
- `Module.isToggleable();` - возвращает `true` если модуль можно переключать, и `false` если нет.
- `Module.isBindable();` - возвращает `true` если модуль можно биндить, и `false` если нет.
- `Module.getCategory();` - возвращает строку с названием категории в которой находится модуль.
- `Module.isActive();` - возвращает текущее состояние модуля (true/false). (*всегда возвращает `false` если модуль нельзя переключать*)
- `Module.isBindActive();` - возвращает `true` или `false` в зависимости от того, стоит ли бинд на модуле. (*всегда возвращает `false` если модуль нельзя биндить*)
- `Module.hasSettings();` - возвращает `true` если модуль имеет настройки, и `false` если нет.
- `Module.getSetting(String name);` - ищет среди настроек модуля настройку с названием `name` и возвращает объект `Setting`. Бросает `RuntimeException` если не находит настройку.
- `Module.getSettings();` - возвращает массив объектов `Setting`.
- `Module.addSetting(Setting setting);` - добавляет настройку к модулю.
- `Module.addSettings(Setting[] settings);` - тоже самое что и `Module.addSetting(Setting setting);`, просто позволяет одной строкой добавить сразу несколько настроек.

- `Module.setOnToggleListener(function(View view, boolean active));` - добавляет действие `function(View view, boolean active)` вызываемое при переключении модуля.
- `Module.setOnClickListener(function(View view));` - добавляет действие `function(View view)` вызываемое при клике по кнопке модуля.

##### Статические методы
###### Эти методы предназначены для работы с дефолтными модулями, они делают тоже самое, что и методы выше, просто первым аргументом требуют имя метода. Бросает `RuntimeException` если модуль не найден. Пока что только так.

- `Module.isToggleable(String moduleName);`
- `Module.isBindable(String moduleName);`
- `Module.getCategory(String moduleName);`
- `Module.isActive(String moduleName);`
- `Module.isBindActive(String moduleName);`
- `Module.hasSettings(String moduleName);`
- `Module.getSettingNames(String moduleName);`
- `Module.addSetting(String moduleName, Setting setting);`
- `Module.addSettings(String moduleName, Setting[] settings);`

##### Примеры: нема

## ModuleManager
###### Класс для добавления/удаления кастомных модулей
##### Статические методы

- `ModuleManager.addModule(Module module);` - добавляет модуль в одну из пяти [категорий](#modulecategory) меню.
- `ModuleManager.addModules(Modules[] modules);` - тоже самое, просто позволяет добавить сразу несколько модулей одной строкой.
- `ModuleManager.removeModule(Module module);` - удаляет модуль.
- `ModuleManager.getModuleNames();` - возвращает массив с именами всех модулей (имена кастомных модулей тоже).

##### Примеры: нема

## Setting
###### Класс для получения какой-либо информации о настройках дефолтных модулей (ситуация та же что и с Module)
##### Статические методы

- `Setting.getType(String moduleName, String settingName);` - ищет настройку `settingName` у модуля `moduleName` и возвращает его тип.
- `Setting.isVisible(String moduleName, String settingName);` - ищет настройку `settingName` у модуля `moduleName` и возвращает логическое значение (`true` если настройка видима и `false` если нет).
- `Setting.setVisibility(String moduleName, String settingName, boolean visibility);` - ищет настройку `settingName` у модуля `moduleName` и устанавливает ей видимость `visibility` (true/false).
- `Setting.getCurrentMode(String moduleName, String settingName);` - ищет настройку `settingName` у модуля `moduleName` и возвращает текущий выбранный режим. **Бросит `RuntimeException` если тип настройки окажется не `mode`**.
- `Setting.getCurrentValue(String moduleName, String settingName);` - ищет настройку `settingName` у модуля `moduleName` и возвращает текущее значение ползунка. **Бросит `RuntimeException` если тип настройки окажется не `slider`**.
- `Setting.isActive(String moduleName, String settingName);` - ищет настройку `settingName` у модуля `moduleName` и возвращает текущее состояние. **Бросит `RuntimeException` если тип настройки окажется не `state`**.
- `Setting.getText(String moduleName, String settingName);` - ищет настройку `settingName` у модуля `moduleName` и возвращает текущий текст. **Бросит `RuntimeException` если тип настройки окажется не `text-field`**.

***Обратите внимание, что каждый из этих методов может бросить `RuntimeException` если вы ошибетесь в названии модуля или настройки.***

##### Примеры: нема

## ButtonSetting
###### Класс для создания настройки кнопки. Можно добавлять не только к кастомным модулям, но и к дефолтным
##### Конструктор: `ButtonSetting(String name, function(View view));`
##### Методы

- `ButtonSetting.getName();` - возвращает имя настройки.
- `ButtonSetting.getType();` - возвращает `"button"`.
- `ButtonSetting.isVisible();` - возвращает `true` если настройка видима и `false` если нет.
- `ButtonSetting.setVisibility(boolean visibility);` - устанавливает настройке видимость `visibility` (true/false).

##### Примеры: нема

## ModeSetting
###### Класс для создания настройки режима. Можно добавлять не только к кастомным модулям, но и к дефолтным
##### Конструктор: `ModeSetting(String name, String[] modes);`
##### Методы

- `ModeSetting.getName();` - возвращает имя настройки.
- `ModeSetting.getType();` - возвращает `"mode"`.
- `ModeSetting.isVisible();` - возвращает `true` если настройка видима и `false` если нет.
- `ModeSetting.setVisibility(boolean visibility);` - устанавливает настройке видимость `visibility` (true/false).

- `ModeSetting.getCurrentMode();` - возвращает текущий выбранный режим.
- `ModeSetting.setOnModeSelectedListener(function(String mode));` - устанавливает действие `function(String mode)` выполняемое после выбора режима.

##### Примеры: нема

## SliderSetting
###### Класс для создания настройки ползунка. Можно добавлять не только к кастомным модулям, но и к дефолтным
##### Конструктор: `SliderSetting(String name, [double default, double min, double max, double step]);`
##### Методы

- `SliderSetting.getName();` - возвращает имя настройки.
- `SliderSetting.getType();` - возвращает `"slider"`.
- `SliderSetting.isVisible();` - возвращает `true` если настройка видима и `false` если нет.
- `SliderSetting.setVisibility(boolean visibility);` - устанавливает настройке видимость `visibility` (true/false).

- `SliderSetting.getCurrentValue();` - возвращает текущее значение.
- `SliderSetting.setOnCurrentValueChangedListener(function(double currentValue));` - устанавливает действие `function(double currentValue)` выполняемое после любого изменения значения.

##### Нема: примеры

## StateSetting
###### Класс для создания настройки состояния. Можно добавлять не только к кастомным модулям, но и к дефолтным
##### Конструктор: `StateSetting(String name, boolean state);`
##### Методы

- `StateSetting.getName();` - возвращает имя настройки.
- `StateSetting.getType();` - возвращает `"state"`.
- `StateSetting.isVisible();` - возвращает `true` если настройка видима и `false` если нет.
- `StateSetting.setVisibility(boolean visibility);` - устанавливает настройке видимость `visibility` (true/false).

- `StateSetting.isActive();` - возвращает `true` если настройка активна и `false` если нет.
- `StateSetting.setOnStateToggleListener(function(boolean state));` - устанавливает действие `function(boolean state)` выполняемое при переключении настройки.

##### Примеры: нема

## TextFieldSetting
###### Класс для создания настройки текстового поля. Можно добавлять не только к кастомным модулям, но и к дефолтным
##### Конструктор: `TextFieldSetting(String name, String hint, String text);`
##### Методы

- `TextFieldSetting.getName();` - возвращает имя настройки.
- `TextFieldSetting.getType();` - возвращает `"text-field"`.
- `TextFieldSetting.isVisible();` - возвращает `true` если настройка видима и `false` если нет.
- `TextFieldSetting.setVisibility(boolean visibility);` - устанавливает настройке видимость `visibility` (true/false).

- `TextFieldSetting.getText();` - возвращает текущий текст.
- `TextFieldSetting.setOnTextChangedListener(function(String text));` - устанавливает действие `function(String text)` выполняемое при изменении текста.

##### Примеры: нема

## Level
###### Класс для работы с уровнем/сервером
##### Статические методы
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
##### Примеры: 1 + 2

## LocalPlayer
###### Класс для работы с твоим игроком
##### Статические методы
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
LocalPlayer.smoothLookAt(int playerID, double smoothness);

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
LocalPlayer.isAlive();
LocalPlayer.isOnLadder();
LocalPlayer.canFly();
LocalPlayer.canShowNameTag();
```
##### Примеры: нема

## Inventory
###### Класс для работы с твоим инвентарем
##### Статические методы
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
##### Примеры: нема

## Item
###### Класс для работы с предметами из твоего инвентаря
##### Статические методы
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
##### Примеры: нема

## Player
###### Класс для работы с игроками на сервере
##### Статические методы
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
##### Примеры: нема

## Block
###### Класс для работы с блоками
##### Статические методы
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
##### Примеры: нема

## Memory
###### Класс для работы с памятью (ТОЛЬКО ДЛЯ ОСОБО УМНЫХ)
##### Статические методы
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
##### Примеры: нема

## Константные классы
### ModuleCategory
###### Категории для кастомных модулей
```
ModuleCategory.COMBAT
ModuleCategory.MOVEMENT
ModuleCategory.PLAYER
ModuleCategory.MISC
ModuleCategory.OTHER
```

### BlockSide
###### В основном нужно для LocalPlayer.buildBlock(x, y, z, side) в качестве аргумента side
```
BlockSide.DOWN
BlockSide.UP
BlockSide.NORTH
BlockSide.SOUTH
BlockSide.WEST
BlockSide.EAST
```

### PacketType
###### Тип отправляемого пакета, нужно для onSendPacket (ЭТО ТОЖЕ ТОЛЬКО ДЛЯ ОСОБО УМНЫХ)
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

## Hooks
###### Все игровые хуки на данный момент
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
onSendPacket(String name, int address); (ТОЖЕ ДЛЯ ОСОБО УМНЫХ)
```
##### Примеры: не
