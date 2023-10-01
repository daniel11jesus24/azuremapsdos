## azuremapsdos

Este código HTML y JavaScript crea un mapa interactivo de Azure Maps centrado en Puebla, México, y muestra marcadores personalizados en lugares específicos en el mapa, utilizando la API de Azure Maps.

### Importación de la API de Azure Maps:

<script type="text/javascript" src="https://atlas.microsoft.com/sdk/javascript/mapcontrol/2/atlas.js"></script>

Esta línea de código importa la biblioteca JavaScript necesaria para trabajar con Azure Maps en la página web.


### Inicialización del mapa:

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

La GetMap se llama cuando se carga la página (window.onload). Crea un mapa en el elemento con el ID "mapDiv", centrado en Puebla, México, y establece un nivel de zoom inicial. Además, proporciona información de autenticación para utilizar Azure Maps.

### Evento 'ready' del mapa:

map.events.add('ready', function () {
    // Una vez que el mapa está listo, puedes agregar la fuente de datos.
    datasource = new atlas.source.DataSource();
    map.sources.add(datasource);

    // Luego, agrega marcadores u otras capas a la fuente de datos y renderízalos en el mapa.
    AddMarkers();
});

Este bloque de código escucha el evento 'ready' del mapa, que se desencadena cuando el mapa está listo para su uso. Cuando el mapa está listo, crea una fuente de datos (datasource) que se utilizará para agregar marcadores y otras capas.

### Añadir marcadores:

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

    La función AddMarkers agrega marcadores a ubicaciones específicas en el mapa. Utiliza un array de objetos nodes que contiene las coordenadas y los nombres de las ubicaciones. Cada marcador se crea como un objeto atlas.Shape y se agrega a la fuente de datos. También se puede personalizar el icono del marcador y agregar propiedades personalizadas (en este caso, el nombre de la ubicación). Finalmente, se renderizan los marcadores en el mapa.


### Estilo personalizado para el marcador:

.azure-maps-icon {
    width: 50px;
    height: 50px;
}

Este estilo CSS personalizado se aplica a los iconos de marcadores en el mapa, ajustando su tamaño a 50x50 píxeles.

### Contenedor del mapa en el cuerpo HTML:

Aquí se crea un contenedor con el ID "mapDiv" que se utilizará para mostrar el mapa. Se establece su ancho y alto.