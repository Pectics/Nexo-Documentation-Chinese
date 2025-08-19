---
cover: >-
  https://www.techyon.es/media/news/full-stack-developer-cu%C3%81les-son-las-principales-competencias_1637600851_21.jpg
coverY: 0
---

# API

### 仓库与依赖

```kotlin
repositories {
    maven("https://repo.nexomc.com/releases")
}

dependencies {
    compileOnly("com.nexomc:nexo:<version>") //Nexo 1.X -> 1.X.0
}
```

## JavaDocs

Nexo 的 JavaDocs 发布在 [https://jd.nexomc.com](https://jd.nexomc.com/)。
这些文档会在 API 发生变更时更新，但更新频率不算高。

## 自定义物品

Nexo 提供了自己的 `ItemBuilder` 类来处理自定义物品的构建。
[NexoItems](https://jd.nexomc.com/1.8/com/nexomc/nexo/api/NexoItems.html) 类包含了处理物品所需的大部分方法。

```java
ItemBuilder itemBuilder = NexoItems.itemFromId(itemID);
ItemStack itemStack = itemBuilder.build();
String itemId = NexoItems.idFromItem(itemStack);
```

{% hint style="info" %}
Nexo 会在异步任务中加载物品，因此在插件的 `onEnable` 中获取它们可能会失败。
你可以监听 **NexoItemsLoadedEvent** 来确保物品已经完成注册。
{% endhint %}

## 自定义方块

[NexoBlocks](https://jd.nexomc.com/1.8/com/nexomc/nexo/api/NexoBlocks.html) 类包含了在 Nexo 中放置、移除和检查自定义方块的所有方法。

```java
NexoBlocks.place(itemID, location)
```

### 家具

[NexoFurniture](https://jd.nexomc.com/1.8/com/nexomc/nexo/api/NexoFurniture.html) 类包含了在 Nexo 中放置、移除和检查家具的所有方法。
此外，你还可以获取家具的 [FurnitureMechanic](https://jd.nexomc.com/1.8/com/nexomc/nexo/mechanics/furniture/FurnitureMechanic.html)，以便在需要时获取它的具体属性。

```java
NexoFurniture.place(itemID, location, @Nullable player)
```

## 自定义机制

Nexo 允许你为插件添加自己的机制，可以是新的机制，也可以是扩展已有的机制。
示例仓库可在 [这里](https://github.com/Nexo-MC/NexoExampleMechanic) 查看，其中包含 Java 与 Kotlin 的示例。
你可以在 `onEnable` 或任意需要的地方注册机制。
这会在 Nexo 注册其自身机制时一并注册，并为物品解析。

机制由一个带有属性和方法的 Mechanic 类组成。
MechanicFactory 则包含了解析全局 Mechanic 属性的方法，以及物品与机制的绑定。

* **NexoMechanicsRegisteredEvent** —— 当 Nexo 加载/重载机制时调用
* **NexoItemsLoadedEvent** —— 当 Nexo 完成加载/重载物品时调用

## 自定义 PackServer

如果你需要的 PackServer 类型 Nexo 没有提供，可以通过编写拓展来注册一个。
只需创建一个继承 `NexoPackServer` 的类，并重写你需要的方法。

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
class MyPackServer : NexoPackServer {
    override fun uploadPack(): CompletableFuture<Void>
    override fun sendPack(player: Player)
    override fun start()
    override fun stop()
    override fun packUrl(): String
    override fun packInfo(): ResourcePackInfo?
}
```
{% endtab %}

{% tab title="Java" %}
```java
public class PackServer extends NexoPackServer {
    @Override
    public CompletableFuture<Void> uploadPack()
    
    @Override
    public void sendPack(Player player)
    
    @Override
    public void start()
    
    @Override
    public void stop()
    
    @Override
    public String packUrl()
    
    @Override
    @Nullable
    public ResourcePackInfo packInfo()
}
```
{% endtab %}
{% endtabs %}

要将其注册到 Nexo，只需调用：
`PackServerRegistry.register(type, packServer)`
