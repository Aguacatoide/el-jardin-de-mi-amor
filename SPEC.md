# El Jardín de Mi Amor - Especificación Creativa

## 1. Concepto y Visión

Un mapa de jardín mágico flotante dedicado a Krismar Morguillo, donde cada margarita collected revela un fragmento de amor en forma de poema. La experiencia evoca la calidez de un jardín secreto en un reino de hadas, combinando la dulzura de Heartopia, la nobleza mística de Ravenclaw y la conexión etérea con la naturaleza que transmite Aurora. El usuario debe sentir que camina por un jardín iluminado por estrellas donde cada flor guarda un secreto.

## 2. Lenguaje de Diseño

### Dirección Estética
**Referencia:** Jardín secreto medieval flotante - combine la paleta de Heartopia (pasteles suaves) con elementos místicos de Ravenclaw (bronce, estrellas doradas) y la fragilidad etérea de Aurora.

### Paleta de Colores
```
--azul-noche:      #1a1a2e    (fondo principal - cielo nocturno)
--azul-profundo:   #16213e    (capas de jardín)
--azul-acento:     #0f3460    (elementos UI)
--bronce:          #c9a227    (detalles dorados/bronce)
--bronce-claro:    #e8d5a3    (bronce iluminado)
--rosa-pastel:     #f8b4c4    (pétalos de margarita)
--blanco-crema:    #fff8e7    (centro margarita, pergamino)
--verde-menta:     #a8e6cf    (vegetación suave)
--verde-sauge:     #88d8b0    (vegetación深)
--oro-estelar:     #ffd700    (estrellas, chispas mágicas)
--lavanda:         #e6e6fa    (acento suave)
```

### Tipografía
- **Títulos:** "Cinzel Decorative" - elegancia medieval
- **Subtítulos:** "Cormorant Garamond" - serif refinada
- **Cuerpo/Poemas:** "EB Garamond" - legible, clásico
- **Fallback:** Georgia, serif

### Sistema Espacial
- Jardín principal: viewport completo con scroll suave
- Elementos flotantes: uso de CSS transforms para efecto 3D sutil
- Margen base: 8px (1 unidad = 8px)
- Zona de toque móvil: mínimo 48px

### Filosofía de Movimiento
- **Entrada de elementos:** fade-in + scale desde 0.8 a 1, 600ms ease-out, staggered 100ms
- **Hover margaritas:** wobble suave (rotate ±5deg), 300ms
- **Colección:** sparkle burst + scale up antes de desvanecerse, 400ms
- **Modal:** slide-up desde bottom + backdrop blur, 350ms spring
- **Partículas finales:** física de gravedad simulada, 200+ partículas doradas/lavanda
- **Estrellas de fondo:** twinkle animation, opacity 0.3-1, random duration 2-5s

### Activos Visuales
- **Iconos:** SVG inline para margaritas, estrellas, cœur (decorativo)
- **Daisy SVG:** pétalos blancos/rosa pastel, centro amarillo dorado
- **Estrellas:** mezcla de tamaños, brillo animado
- **Pergamino:** textura CSS con gradientes y sombras
- **Galería:** polaroid frames con sombra suave

## 3. Layout y Estructura

### Arquitectura de Página
```
┌─────────────────────────────────────────┐
│  Header: Título "El Jardín de Mi Amor"  │
│  + Counter Daisy (0/28) top-right       │
├─────────────────────────────────────────┤
│                                         │
│         JARDÍN INTERACTIVO              │
│    (Vista aérea de jardín flotante)     │
│                                         │
│   🌸  🌸      🏛️        🌸              │
│      🌸   GALERÍA   🌸    🌸            │
│   🌸      🌸   🌸      🌸   🌸          │
│        🌸      🌸    🌸                 │
│   🌸    🌸  🌸     🌸      🌸           │
│                                         │
│  (28 margaritas distribuidas)           │
│                                         │
├─────────────────────────────────────────┤
│        GALERÍA DE DIBUJOS               │
│   ┌────┐ ┌────┐ ┌────┐ ┌────┐          │
│   │img1│ │img2│ │img3│ │img4│          │
│   └────┘ └────┘ └────┘ └────┘          │
└─────────────────────────────────────────┘
```

### Estrategia Responsive
- **Desktop (>1024px):** jardín amplio, margaritas más espaciadas
- **Tablet (768-1024px):** jardín compacto, 2 columnas en galería
- **Mobile (<768px):** scroll vertical optimizado, margaritas reorganizadas, galería 1 columna

### Flujo Visual
1. Cargando → Estrellas aparecen gradualmente (1s)
2. Título entra con fade + slide (0.5s delay)
3. Jardín "crece" desde el centro (0.8s delay)
4. Margaritas aparecen staggered desde el centro hacia afuera (1s+ delay)

## 4. Features e Interacciones

### Sistema de Colección de Margaritas
- **Estado inicial:** 28 margaritas visibles, botón brillante sutil
- **Hover:** wobble animation + glow aumenta + tooltip "Toca para descubrir"
- **Click:**
  1. Daisy scale up 1.2x (100ms)
  2. Burst de chispas doradas (8-12 partículas)
  3. Daisy se desvanece con scale down
  4. Counter incrementa con bounce animation
  5. Modal de poema se abre
- **Ya collectada:** no visible (o visible como "fantasma" suave)

### Modal de Poema
- **Apertura:** slide-up desde bottom, backdrop blur 8px
- **Diseño:** pergamino antiguo con bordes irregulares (clip-path o border-image)
- **Contenido:**
  - Decoración de margarita en header
  - Número de poema (ej: "Poema VII de XXVIII")
  - Texto del poema (espacio reservado para 28 poemas)
  - Botón "Cerrar" estilizado
- **Cierre:** click fuera, botón, o ESC key

### Galería de Dibujos "Galería de Krismar"
- **Ubicación:** edificio/estructura en el jardín (derecha o centro)
- **Diseño:** estructura tipo torre o cottage con letrero
- **Interacción:** hover muestra glow, click expande/cambia vista
- **Vista expandida:** grid de imágenes tipo polaroid
- **Imágenes:** placeholder con instruction para替换

### Evento Final (28/28)
- **Trigger:** cuando counter === 28
- **Secuencia:**
  1. Jardín se oscurece levemente (1s)
  2. Partículas doradas empiezan a caer desde arriba (2s)
  3. Texto aparece con typewriter effect: "Feliz cumpleaños Krismar"
  4. Segunda línea: "te amo con mis 7 vidas"
  5. Partículas continúan, confetti sutil
  6. Música opcional (sin implementar, placeholder)

### Estados de Error/Edge Cases
- **Doble click en daisy:** ignore si ya está en proceso de collection
- **Modal ya abierto:** cerrar primero, luego abrir nuevo
- **Counter fuera de rango:** clamp 0-28
- **Galería vacía:** mensaje "Próximamente..." con imagen placeholder

## 5. Inventario de Componentes

### Daisy (Margarita)
- **Default:** pétalos visibles, centro brillante, sombra suave
- **Hover:** wobble, glow aumenta, scale 1.05
- **Active:** scale 0.95
- **Collected:** fade out + scale down
- **Disabled:** n/a

### Counter Badge
- **Default:** icono daisy + "0/28", fondo semi-transparente
- **Update:** bounce animation en número
- **Complete (28/28):** glow dorado, celebración sutil

### Poem Modal
- **Container:** centrado, max-width 500px, border-radius 8px
- **Backdrop:** rgba(0,0,0,0.6), blur
- **Parchment:** gradiente crema, textura sutil, shadow
- **Close button:** X en esquina, hover glow

### Gallery Card
- **Default:** polaroid style, sombra suave, margen
- **Hover:** lift up (translateY -4px), sombra más pronunciada
- **Image:** aspect-ratio 1:1, object-fit cover

### Particle
- **Shape:** círculo pequeño (2-6px)
- **Colors:** oro, bronce claro, lavanda
- **Animation:** caída con drift horizontal, fade out al final

### Star (decorativo)
- **Shape:** 4-point o 6-point star SVG
- **Animation:** twinkle (opacity), algunos con rotate lento

## 6. Enfoque Técnico

### Stack
- **HTML5:** semántico, accessibility
- **CSS3:** custom properties, flexbox, grid, animations
- **Tailwind CSS:** mediante CDN para utilidades
- **JavaScript Vanilla:** ES6+, sin bundler

### Arquitectura JS
```
- Estado global: { collected: Set, isModalOpen: boolean }
- Const: POEMS array (28 elementos, placeholder strings)
- Funciones:
  - initGarden(): posiciona daisies
  - collectDaisy(id): maneja colección
  - openModal(poemIndex): muestra poema
  - closeModal(): cierra modal
  - updateCounter(): actualiza UI
  - triggerCelebration(): evento final
  - createParticles(): sistema de partículas
```

### Posicionamiento de Daisies
- Coordenadas predefinidas en array (x%, y%)
- Z-index variado para profundidad
- Rotation sutil variado

### Performance
- requestAnimationFrame para partículas
- IntersectionObserver para lazy animations
- CSS transforms sobre position para animaciones
- will-change en elementos animados

### Accesibilidad
- focus-visible en elementos interactivos
- aria-labels en daisies
- keyboard navigation para modal
- prefers-reduced-motion respectado

## 7. Contenido Placeholder

### Poemas (Espacio Reservado)
```javascript
const POEMS = [
  "Poema 1 - Personaliza aquí...",
  "Poema 2 - Personaliza aquí...",
  // ... hasta 28
];
```

### Imágenes de Galería
- Usar placeholder service: https://via.placeholder.com/400x400
- Instruction clara para reemplazar con dibujos reales

### Texto Final
```javascript
const CELEBRATION_TEXT = {
  main: "Feliz cumpleaños Krismar",
  secondary: "te amo con mis 7 vidas"
};
```
