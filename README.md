# hmod-plugin-base

Minimal base `Plugin` abstraction for hMod plugins.

Maven coordinates:

```xml
<dependency>
    <groupId>com.asbestosstar</groupId>
    <artifactId>hmod-plugin-base</artifactId>
    <version>0.0.1</version>
</dependency>
```

---

## Purpose

This project provides a minimal version of hMod's `Plugin` class containing only the essential functionality needed to create simple hMod plugins.

The original hMod software is old and difficult to compile against cleanly in modern environments. This artifact exists mainly as a lightweight bootstrap abstraction for plugin development.

It is intended for:

- Simple plugins
- Legacy plugin compatibility
- Compiling old plugins
- Minimal hMod bootstrap support
- Projects that only need the basic plugin structure

It is **not** intended to fully replace the complete hMod API.

---

## What It Includes

The base `Plugin` abstraction provides:

- `enable()`
- `disable()`
- `initialize()`
- plugin enabled state
- plugin name storage

Example:

```java
public abstract class Plugin {

    public abstract void enable();

    public abstract void disable();

    public void initialize() {
    }
}
```

---

## How hMod Loads Plugins

hMod loads plugins by:

1. Reading the `plugins=` entry from `server.properties`
2. Looking for:
   ```
   plugins/PluginName.jar
   ```
3. Loading a class named:
   ```java
   PluginName
   ```
4. Instantiating it
5. Calling:
   ```java
   enable();
   ```
6. Then calling:
   ```java
   initialize();
   ```

Plugins are explicitly listed in `server.properties`.

---

## Example Plugin

```java
public class MyPlugin extends Plugin {

    @Override
    public void enable() {
        System.out.println("Plugin enabled");
    }

    @Override
    public void disable() {
        System.out.println("Plugin disabled");
    }

    @Override
    public void initialize() {
        System.out.println("Plugin initialized");
    }
}
```

---

## Building a Plugin

1. Add this dependency
2. Create a class extending `Plugin`
3. Build your jar
4. Name the jar:
   ```
   MyPlugin.jar
   ```
5. Place it into:
   ```
   plugins/
   ```
6. Add to `server.properties`:
   ```properties
   plugins=MyPlugin
   ```

---

## Important Limitation

This project only provides the minimal `Plugin` base abstraction.

It does **not** include:

- full listener APIs
- server wrappers
- entity wrappers
- block APIs
- player APIs
- hook systems
- networking
- world APIs
- inventory APIs
- internal Minecraft server classes

Those systems depend heavily on old and obfuscated Minecraft server internals.

If your plugin needs deeper integration, you will still need the original hMod server/API environment.

---

## Why This Exists

Old Minecraft server ecosystems are difficult to compile against today because:

- many artifacts were never published to Maven Central
- original downloads are disappearing
- APIs depend on obfuscated internals
- repositories are incomplete or broken

This project provides a clean Maven Central artifact for the basic hMod plugin bootstrap structure.

---

## License

GNU General Public License v3.0
