<template>
  <div id="app">
    <l-map
      :center="[-23.752961, -57.854357]"
      :zoom="6"
      style="height: 500px"
    >
      <l-tile-layer
        class="leaflet-tile-pane"
        :url="url"
        :attribution="attribution"
        :opacity="0.5"
      />
      <l-choropleth-layer
        :data="pyDepartmentsData"
        titleKey="department_name"
        idKey="department_id"
        :value="value"
        :extraValues="extraValues"
        geojsonIdKey="dpto"
        :geojson="paraguayGeojson"
        :colorScale="colorScale"
      >
      </l-choropleth-layer>
    </l-map>
  </div>
</template>

<script>
import { LMap, LTileLayer } from "@vue-leaflet/vue-leaflet";
import ChoroplethLayer from "./ChoroplethLayer.vue";

import { geojson } from "../data/py-departments-geojson";
import paraguayGeojson from "../data/paraguay.json";
import { pyDepartmentsData } from "../data/py-departments-data";

export default {
  components: {
    LMap,
    LTileLayer,
    "l-choropleth-layer": ChoroplethLayer,
  },
  data() {
    return {
      pyDepartmentsData,
      paraguayGeojson,
      colorScale: ["e7d090", "e9ae7b", "de7062"],
      value: {
        key: "amount_w",
        metric: "% girls",
      },
      extraValues: [
        {
          key: "amount_m",
          metric: "% boys",
        },
      ],
      currentStrokeColor: "3d3213",
      url: "https://api.mapbox.com/styles/v1/mapbox/streets-v11/tiles/{z}/{x}/{y}?access_token=pk.eyJ1IjoiampzYW5jaGV6IiwiYSI6ImNra25jdDhweDE0ZXgyb29jeHRkaW10Z3AifQ.5sV_IKha4TaUpoOBt79H7g",
      attribution:
        '© <a href="https://www.mapbox.com/feedback/">Mapbox</a> © <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>',
    };
  },
};
</script>

<style>
@import "/node_modules/leaflet/dist/leaflet.css";
body {
  background-color: #e7d090;
  margin-left: 100px;
  margin-right: 100px;
}
#map {
  background-color: #eee;
}
</style>
