<script>
  import mapboxgl from "mapbox-gl";
  
  import { onMount } from "svelte";
  let mapEl;
  let map;
  mapboxgl.accessToken =
    "pk.eyJ1IjoiaWx0aW1hc2QiLCJhIjoiY2tubWVoZjF6MHB2MDJucnl4dXJzOTdnNSJ9.XpxDSSPOBZbaZ_kmXr9JGg";
  onMount(runOnMount);
  
  function runOnMount() {
    console.log(mapEl);
    map = new mapboxgl.Map({
      container: "mapEl", // container ID
      style: "mapbox://styles/iltimasd/cknl97kef155i17o1yidwbuoo",
    });
    map.on("click", function (e) {
      var features = map.queryRenderedFeatures(e.point, {
        layers: ["420nyc"], // replace this with the name of the layer
      });

      if (!features.length) {
        return;
      }

      var feature = features[0];

      var popup = new mapboxgl.Popup({ offset: [0, -15] })
        .setLngLat(feature.geometry.coordinates)
        .setHTML(`<h3>${feature.properties.title}</h3>`)
        .addTo(map);
    });
  }
</script>

<div id="mapEl" />

<style>
  #mapEl {
    position: absolute;
    top: 0;
    bottom: 0;
    width: 100%;
  }
</style>
