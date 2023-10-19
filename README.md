# azuremapsdos

Este código HTML y JavaScript crea un mapa interactivo de Azure Maps centrado en Puebla, México, y muestra marcadores personalizados en lugares específicos en el mapa, utilizando la API de Azure Maps.

### Importación de la API de Azure Maps:

```ruby
<script type="text/javascript" src="https://atlas.microsoft.com/sdk/javascript/mapcontrol/2/atlas.js"></script>
```

Esta línea de código importa la biblioteca JavaScript necesaria para trabajar con Azure Maps en la página web.


### Inicialización del mapa:

```ruby
var map, datasource;

function GetMap() {
    // Crea un mapa en el elemento "mapDiv" y lo centra en una ubicación específica.
    map = new atlas.Map('mapDiv', {
        center: [-98.193042, 19.046026], // Coordenadas de Puebla, México
        zoom: 13,
        view: 'Auto',
        authOptions: {
            authType: 'subscriptionKey',
            subscriptionKey: 'CWfOCbYY2R3bV8CDeqD9biMVp4nqztcIixNYAe1Olxw'
        }
    });
}
```

La GetMap se llama cuando se carga la página (window.onload). Crea un mapa en el elemento con el ID "mapDiv", centrado en Puebla, México, y establece un nivel de zoom inicial. Además, proporciona información de autenticación para utilizar Azure Maps.

### Evento 'ready' del mapa:

```ruby
map.events.add('ready', function () {
    // Una vez que el mapa está listo, puedes agregar la fuente de datos.
    datasource = new atlas.source.DataSource();
    map.sources.add(datasource);

    // Luego, agrega marcadores u otras capas a la fuente de datos y renderízalos en el mapa.
    AddMarkers();
});
```

Este bloque de código escucha el evento 'ready' del mapa, que se desencadena cuando el mapa está listo para su uso. Cuando el mapa está listo, crea una fuente de datos (datasource) que se utilizará para agregar marcadores y otras capas.

### Añadir marcadores:

```ruby
function AddMarkers() {
    // Agrega marcadores para los nodos por defecto.
    var nodes = [
        // ... Lista de objetos con coordenadas y nombres de ubicaciones
    ];

    nodes.forEach(function (node) {
        var marker = new atlas.Shape(new atlas.data.Point(node.coordinates), {
            iconOptions: {
                image: 'pin-round-blue.png', // Personaliza el icono del marcador
                allowOverlap: true
            }
        });

        // Agrega una propiedad personalizada para mostrar información adicional.
        marker.setProperties({
            name: node.name
        });

        datasource.add([marker]);
    });

    // Renderiza el mapa.
    map.layers.add(new atlas.layer.SymbolLayer(datasource));
}
```

La función AddMarkers agrega marcadores a ubicaciones específicas en el mapa. Utiliza un array de objetos nodes que contiene las coordenadas y los nombres de las ubicaciones. Cada marcador se crea como un objeto atlas.Shape y se agrega a la fuente de datos. También se puede personalizar el icono del marcador y agregar propiedades personalizadas (en este caso, el nombre de la ubicación). Finalmente, se renderizan los marcadores en el mapa.


### Estilo personalizado para el marcador:

```ruby
.azure-maps-icon {
    width: 50px;
    height: 50px;
}
```

Este estilo CSS personalizado se aplica a los iconos de marcadores en el mapa, ajustando su tamaño a 50x50 píxeles.

### Contenedor del mapa en el cuerpo HTML:

Aquí se crea un contenedor con el ID "mapDiv" que se utilizará para mostrar el mapa. Se establece su ancho y alto.

# Geolocalizacion

Este código HTML y JavaScript está diseñado para crear una aplicación web de demostración que utiliza Azure Maps para calcular rutas entre ubicaciones seleccionadas por el usuario

#### Metaetiquetas: 
En el encabezado HTML, se definen algunas metaetiquetas, como la codificación de caracteres y la configuración de la escala inicial para dispositivos móviles.

#### Referencias a archivos JavaScript y CSS:
Se incluyen referencias a archivos JavaScript y CSS proporcionados por Azure Maps. Estos archivos son necesarios para utilizar el servicio de mapas y calcular rutas.

#### Script: 
Se incluye una sección de script que contiene varias funciones y configuraciones.

    InitMap(): Esta función se llama cuando se carga el cuerpo del HTML. Crea una instancia de un mapa de Azure Maps, configura la ubicación inicial y la clave de suscripción, y agrega un controlador de eventos para esperar a que los recursos del mapa estén listos.

    GetMap(): Se llama cuando el usuario hace clic en el botón "Vamos". Esta función agrega capas al mapa para mostrar rutas y puntos de interés. Luego, realiza solicitudes de rutas para varios modos de transporte (camión, carro y bicicleta) y muestra la distancia y el tiempo de viaje en la interfaz.

#### Estilos CSS: 
Se definen estilos CSS para dar formato a la página web, incluyendo colores, tamaños de fuente, y diseños de botones.

#### Cuerpo del HTML:
El cuerpo del HTML incluye un formulario y una tabla que contiene la interfaz de usuario. Los usuarios pueden seleccionar ubicaciones de inicio y destino, así como el modo de transporte. También pueden hacer clic en el botón "Vamos" para calcular y mostrar rutas en el mapa. La información de la ruta, como la distancia y el tiempo de viaje, se muestra en la parte inferior de la tabla.

#### Div para el mapa: 
Se incluye un div con el ID "myMap" donde se muestra el mapa de Azure Maps.

## Conclusion

Luego de una exhaustiva investigación y el desarrollo de nuestro código, hemos llegado a la conclusión de que para llevar a cabo la traza de rutas y la visualización de puntos en el mapa, es imperativo activar funciones específicas de la API de AzureMaps, especialmente la característica de "Routing". Esta funcionalidad nos proporciona los servicios necesarios para trazar rutas y exhibir información detallada de cada coordenada, como el nombre y la dirección. Es fundamental destacar que el uso de estas características de la API conlleva un costo económico.