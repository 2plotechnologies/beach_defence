# Beach Defense: Crab's Revenge

## Descripción general
**Beach Defense** es un juego arcade 2D hecho en un único archivo `index.html` (HTML + CSS + JavaScript con Canvas API).

El jugador controla un cangrejo que defiende la playa de oleadas de enemigos humanos y maquinaria pesada. El objetivo es sobrevivir, sumar puntos y derrotar al jefe final (un acorazado).

---

## Dinámica del juego

### Objetivo
- Proteger la salud de la playa (`beachHealth`) evitando que los enemigos lleguen al fondo.
- Acumular puntuación eliminando enemigos.
- Al llegar a **1000 puntos**, aparece el jefe final.
- Derrotar al jefe para ganar la partida.

### Controles
- **Flecha izquierda / derecha**: mover el cangrejo.
- **Espacio o Flecha arriba**: disparar.

### Flujo de partida
1. Pantalla inicial con botón **JUGAR**.
2. Durante la partida se muestra:
   - Puntos.
   - Barra de salud de la playa.
3. Se generan enemigos normales y aliados según el tiempo (`frame`) y la puntuación.
4. Si la salud llega a 0, derrota.
5. Si el jefe cae a 0 de vida, victoria.

---

## Entidades principales

### Jugador (`Crab`)
- Se mueve horizontalmente.
- Dispara proyectiles azules con un pequeño tiempo de recarga.

### Aliados (`Lobster`)
- Aparecen periódicamente por izquierda o derecha.
- Se colocan en posición de guardia y disparan proyectiles púrpuras en apoyo.

### Proyectiles (`Bullet`)
- Clase reutilizada para disparos del jugador, aliados y jefe.
- Se eliminan al salir del canvas o tras una colisión.

### Enemigos
- **`Soldier`**:
  - Enemigo básico.
  - Vida baja y daño moderado a la playa si atraviesa.
- **`Bulldozer`**:
  - Enemigo más resistente.
  - Más daño y mayor puntuación al destruirlo.

### Jefe final (`BossShip`)
- Se activa al llegar a 1000 puntos.
- Limpia enemigos menores al aparecer.
- Dispara ráfagas dirigidas al jugador.
- Tiene barra de vida propia.

### Power-up (`HealthKit`)
- Botiquín que restaura salud de la playa.
- Solo aparece cuando la salud está por debajo de 50.

### Efectos (`Particle`)
- Fragmentos visuales para explosiones y feedback de impactos.

---

## Lógica y estado del juego

### Estado global
Variables de estado relevantes:
- `score`: puntuación actual.
- `beachHealth`: salud de la playa (0–100).
- `gameActive`: controla si el loop está corriendo.
- `bossSpawned`, `boss`, `bossDefeated` (esta última está declarada pero no usada actualmente).
- Arreglos de objetos: `enemies`, `bullets`, `enemyBullets`, `particles`, `powerups`, `allies`.
- `frame`: contador para temporización de spawns.

### Funciones clave
- `startGame()`: oculta menú inicial, muestra UI y arranca el loop.
- `takeDamage(amount)`: reduce salud de playa y valida derrota.
- `spawnManagers()`: gestiona aparición de soldados, bulldozers, aliados y botiquines; dispara evento de jefe.
- `triggerBoss()`: muestra alerta de jefe y crea el acorazado tras 3 segundos.
- `checkCollisions()`: resuelve impactos entre balas/enemigos/jefe y recogida de botiquines.
- `endGame(victory)`: detiene juego y muestra pantalla final.
- `animate()`: loop principal (`requestAnimationFrame`) con update/draw de todas las entidades.

---

## Estructura del archivo único

`index.html` contiene tres capas:
1. **HTML**: contenedor, HUD, menús, canvas.
2. **CSS**: estilo retro, overlays y barra de vida.
3. **JavaScript**: estado, clases de entidades y loop de juego.

---

## Posibles mejoras (documentación técnica rápida)
- Usar módulos JS para separar entidades y lógica.
- Ajustar dificultad con curvas por tiempo en lugar de depender solo de `score` y `frame`.
- Eliminar/usar variables no utilizadas (`bossDefeated`).
- Añadir sistema de sonido, pausa y niveles.
- Persistir récord en `localStorage`.

