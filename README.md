# ⚡ Defensa Estelar — Godot 4

Tower defense de ciencia ficción construido completamente con código GDScript.
No requiere assets externos — todo se genera por código en tiempo de ejecución.

## Cómo abrir el proyecto

1. Abrí **Godot 4.3+**
2. Hacé clic en **Importar** y seleccioná la carpeta del proyecto
3. Abrí la escena `res://scenes/Main.tscn`
4. Presioná **F5** para jugar

## Estructura del proyecto

```
stellar_defense/
├── scenes/
│   ├── Main.tscn              ← Escena raíz
│   ├── enemies/               ← Escenas de enemigos
│   └── towers/                ← Escenas de torres
├── scripts/
│   ├── Main.gd                ← Controlador principal
│   ├── GameManager.gd         ← Singleton: estado global
│   ├── Localization.gd        ← Singleton: textos ES/EN
│   ├── MapBuilder.gd          ← Singleton: generación de mapas
│   ├── ObjectPool.gd          ← Singleton: pool de proyectiles
│   ├── MapBase.gd             ← Base de mapas
│   ├── TowerSlot.gd           ← Slots de colocación
│   ├── enemies/
│   │   ├── Enemy.gd           ← Clase base de enemigos
│   │   ├── AlienFlyer.gd      ← Volador (camino directo)
│   │   └── ColossalBoss.gd    ← Jefe (regenera, spawnea secuaces)
│   ├── managers/
│   │   ├── WaveManager.gd     ← Control de oleadas y spawn
│   │   ├── TowerManager.gd    ← Construcción y selección de torres
│   │   ├── Projectile.gd      ← Proyectil base (pooleable)
│   │   ├── CryoProjectile.gd  ← Proyectil con ralentización
│   │   └── MissileProjectile.gd ← Proyectil con explosión en área
│   ├── systems/
│   │   └── UpgradeSystem.gd   ← Árbol tecnológico (Autoload)
│   └── towers/
│       ├── Tower.gd           ← Clase base de torres
│       ├── LaserTower.gd      ← Rápida, daño medio
│       ├── PlasmaTower.gd     ← Lenta, daño muy alto
│       ├── CryoTower.gd       ← Ralentiza enemigos
│       └── MissileTower.gd    ← Explosión en área
```

## Torres disponibles

| Torre   | Costo | Daño | Alcance | Cadencia | Especial              |
|---------|-------|------|---------|----------|-----------------------|
| Láser   | 80⚡  | Bajo | Medio   | Alta     | Instantáneo           |
| Plasma  | 150⚡ | Alto | Largo   | Baja     | Proyectil lento       |
| Cryo    | 100⚡ | Bajo | Corto   | Media    | Ralentiza 50%         |
| Misil   | 130⚡ | Alto | Largo   | Media    | Daño en área (radio)  |

Todas las torres tienen **3 niveles de mejora** y se pueden vender por el 60% de lo gastado.

## Tipos de enemigos

| Enemigo        | Vida  | Velocidad | Especial                          |
|----------------|-------|-----------|-----------------------------------|
| Explorador     | Baja  | Alta      | —                                 |
| Guerrero       | Media | Media     | —                                 |
| Blindado       | Alta  | Lenta     | Armadura 30% reducción de daño    |
| Volador        | Media | Alta      | Ignora el camino, va en línea recta |
| Jefe Colosal   | 2000  | Muy lenta | Regenera vida, spawnea secuaces   |

## Mecánicas principales

- **20 oleadas** en modo normal (oleada de jefe cada 5)
- **Árbol tecnológico**: gastá puntos técnicos entre oleadas
- **Modo infinito**: se desbloquea al completar las 20 oleadas
- **3 dificultades**: Fácil / Normal / Difícil
- **5 mapas** con diseños distintos
- **8 logros** desbloqueables
- **Idiomas**: Español / Inglés (botón en el menú)

## Autoloads requeridos

Configurar en **Proyecto → Configuración del Proyecto → Autoload**:

| Nombre         | Ruta                                    |
|----------------|-----------------------------------------|
| GameManager    | res://scripts/GameManager.gd            |
| Localization   | res://scripts/Localization.gd           |
| MapBuilder     | res://scripts/MapBuilder.gd             |
| ObjectPool     | res://scripts/ObjectPool.gd             |
| UpgradeSystem  | res://scripts/systems/UpgradeSystem.gd  |

## Controles

| Acción              | Tecla / Botón               |
|---------------------|-----------------------------|
| Pausar              | `Esc` o botón Pausa         |
| Velocidad x2        | `Tab` o botón Velocidad     |
| Construir torre     | Clic en botón → clic en slot|
| Seleccionar torre   | Clic sobre la torre         |
| Mejorar / Vender    | Panel lateral derecho       |
| Volver al menú      | Botón "⌂ Menú" en el HUD   |
| Enviar oleada       | Botón inferior derecho      |
