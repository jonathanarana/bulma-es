# Bulma-ES: Localización de Bulma al Español

## 📘 Resumen del Proyecto

Bulma-ES es un proyecto de localización del framework CSS Bulma para desarrolladores hispanohablantes. Este proyecto permite el uso de clases y modificadores en español, manteniendo total compatibilidad con el framework original.

**Objetivo principal:** Ofrecer una experiencia de desarrollo más natural para la comunidad hispanohablante, permitiendo utilizar una nomenclatura de clases en español sin sacrificar la potencia y flexibilidad de Bulma.

## 🛠️ Arquitectura y Estrategia

### Sistema Centralizado de Traducciones

Utilizamos un sistema centralizado de traducciones en `sass/utilities/translations.scss` que incluye:

1. **Mapas de traducción centralizados:**
   ```scss
   $color-translations: (
     "primary": "primario",
     "link": "enlace",
     "success": "exito",
     // etc.
   );
   ```

2. **Funciones de traducción:**
   ```scss
   @function translate-color($name) {
     @if map.has-key($color-translations, $name) {
       @return map.get($color-translations, $name);
     }
     @return $name;
   }
   ```

3. **Generación dinámica de clases:**
   ```scss
   @each $name, $color in dv.$colors {
     $spanish-name: trans.translate-color($name);
     .es-#{$spanish-name} {
       @extend .is-#{$name};
     }
   }
   ```

### Principios de implementación

1. **No duplicación:** Uso de `@extend` para heredar estilos de las clases originales
2. **Integración:** Las traducciones se añaden al final del archivo original de cada componente
3. **Consistencia:** Todas las traducciones siguen el mismo patrón y nomenclatura
4. **Compatibilidad:** 100% compatible con el framework original

## 📋 Guía de Implementación

### Método correcto

1. ✅ Agregar alias al **final del archivo SCSS original** de cada componente
2. ✅ Usar `@extend` para heredar estilos existentes
3. ✅ Utilizar el sistema centralizado de traducciones
4. ✅ Actualizar la tabla de avance en `traduccion.html` cuando complete un componente

### Errores comunes a evitar

1. ❌ Crear archivos separados para traducciones
2. ❌ Usar `@extend` con selectores compuestos (Sass moderno no lo permite)
3. ❌ Implementar traducciones inconsistentes
4. ❌ Codificar traducciones directamente en vez de usar el sistema centralizado

## 🧩 Componentes Implementados

### 1. Botones (`button` → `boton`)

**Colores y estados**
```scss
// Botón individual
.boton {
  @extend .button;
  
  // Colores
  &.es-primario { @extend .is-primary; }
  &.es-enlace { @extend .is-link; }
  &.es-info { @extend .is-info; }
  // etc.
}
```

### 2. Sistema de Columnas (`columns` → `columnas`)

**Clases base**
```scss
.columnas { @extend .columns; }
.columna { @extend .column; }
```

**Modificadores responsivos**
```scss
.columna {
  &.es-tres-cuartos { @extend .is-three-quarters; }
  &.es-tres-cuartos-celular { @extend .is-three-quarters-mobile; }
  // etc.
}
```

### 3. Componente Caja (`box` → `caja`)

```scss
.caja {
  @extend .box;
}

// Enlaces con la clase caja
a.caja {
  &:hover, &:focus { box-shadow: cv.getVar("box-link-hover-shadow"); }
  &:active { box-shadow: cv.getVar("box-link-active-shadow"); }
}
```

### 4. Componente Contenido (`content` → `contenido`)

```scss
.contenido {
  @extend .content;
  
  &.es-pequeno { @extend .is-small; }
  &.es-mediano { @extend .is-medium; }
  &.es-grande { @extend .is-large; }
}
```

### 5. Helpers de Color

```scss
.tiene-texto-primario { @extend .has-text-primary; }
.tiene-fondo-primario { @extend .has-background-primary; }
// También con variaciones
.tiene-texto-primario-claro { @extend .has-text-primary-light; }
```

## 🔍 Comprobación y Validación

1. **Compilación:** Ejecutar `npm run deploy` desde la carpeta `docs` para verificar que no hay errores
2. **Pruebas visuales:** Revisar `docs/documentation/traduccion.html` para confirmar funcionalidad
3. **Actualización de estado:** Modificar la tabla de avance cuando se complete un componente

## 📊 Tabla de traducciones comunes

### Prefijos y modificadores
- `is-` → `es-` (prefijo para modificadores)
- `has-` → `tiene-` (prefijo para helpers)

### Colores
- `primary` → `primario`
- `link` → `enlace`
- `info` → `info`
- `success` → `exito` 
- `warning` → `advertencia`
- `danger` → `peligro`
- `light` → `claro`
- `dark` → `oscuro`

### Tamaños
- `small` → `pequeno`
- `medium` → `mediano`
- `large` → `grande`

### Modificadores comunes
- `centered` → `centrado`/`centrada`
- `rounded` → `redondeado`
- `outlined` → `delineado`
- `fullwidth` → `anchocompleto`
- `multiline` → `multilinea`

## 🚀 Flujo de trabajo para implementar nuevos componentes

1. **Analizar componente:** Identificar clases y modificadores a traducir
2. **Implementar traducción:** Seguir el patrón establecido usando `@extend`
3. **Verificar:** Compilar y probar visualmente el resultado
4. **Documentar:** Actualizar tabla de avance y ejemplos en `traduccion.html`

## 💻 Entorno de desarrollo

Para iniciar el servidor de documentación y ver los cambios en tiempo real:

```bash
cd docs
npm run deploy        # Para compilar SCSS
jekyll serve --incremental --config _config.local.yml   # Para servir documentación
```

Acceder a http://127.0.0.1:4000/documentation/traduccion.html para ver los resultados.
