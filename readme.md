# Lemoncode - Master XVII
## De Figma a CSS
## Autora: Mónica del Corral. WILDÔOM.
___

## Pug to HTML

Este proyecto utiliza Pug como template engine para HTML. Esto lo suelo usar sólo en proyectos de maquetación sin integración, es decir, cuando el resultado final debe ser un HTML estático (bien porque lo integra otro equipo o porque es un sitio tan pequeño que no tiene CMS). Es muy útil para ahorrar tiempo en loops y condicionales, pero mi consejo es que para empezar os acostumbréis al HTML estándar.
https://www.npmjs.com/package/pug


## Cuestiones a plantearse en este proyecto

### Variables de texto

¿Merece la pena crear y pasar las variables de texto desde config.scss a text.scss? Y así crear un text.scss más reutilizable.
Pasar de esto:

```
@mixin text-hierarchy--1() {
  font-weight: 900;
  font-size: 3rem;
  line-height: 1.1667em;
  margin: 0 0 1rem 0;
  color: var(--color-title);
}
```

a esto:

```
@mixin text-hierarchy--1() {
  font-weight: var(--text-hierarchy-1-font-weight);
  font-size: var(--text-hierarchy-1-font-size);
  line-height: var(--text-hierarchy-1-line-height);
  margin: var(--text-hierarchy-1-margin);
  color: var(--color-title);
}
```
Y dichas variables añadirlas a config.scss

### Jerarquías de texto de un proyecto

No todos los proyectos tienen las mismas jerarquías pero casi todos los proyectos se pueden resolver con:
- 5 jerarquías de título
- 1 jerarquía de body
- 1 jerarquía de body pequeño
- 1 jerarquía de body grande
- 1 jerarquía de navegación
- 1 jerarquía de botón

Aunque puede haber otras como:
- 1 jerarquía de input
- 1 jerarquía de tag, badge, etc. (Muchas vecces es la jerarquía de body pequeño pero no tiene por qué)

Esto significa que hay que tener en cuenta que text.scss puede ser mucho más flexbile con variables pero no será infalible para cualquier proyecto y tendremos que editarlo y adecuarlo a las necesidades.


### Uso de variables SASS

¿A estas alturas merece la pena el uso de variables SASS si vamos a utilizar variables CSS? 
Si el proyecto es pequeño, seguramente nos valgan las variables SASS, que se compilan en un CSS que lee el navegador (el navegador no llega a saber si eso eran o no variables SASS). Pero si el proyecto requiere por ejemplo un light/dark mode, entonces por muy pequeño que sea, nos será útil tener variables CSS (ojo, se puede hacer con SASS también pero requiere más código y será menos escalable).

Si queremos usar un loop dentro del código, por ejemplo, darle un background-color más claro a partir del color base según el index del elemento, nos será útil tenerlo en variable SASS:

```
$base-color: #036;

ul {
  @for $i from 1 through 5 {
    li:nth-child(#{$i}) {
      background-color: lighten($base-color, $i * 5%);
    }
  }
}
```

