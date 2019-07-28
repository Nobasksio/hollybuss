<template>

    <div>
        {{mapAddress}}

        <div class="c-map">

            <img class="c-map__pointer" src="/img/map-pointer.png"/>

            <yandex-map :coords="[52.261543, 104.265431]"
                        :zoom="17"
                        :controls="controls"
                        @click="onClick"
                        @map-was-initialized="onMapWasInitialized"
                        class="c-map__embed"
                        ref="map"
                        :settings="mapSettings"
            >

            </yandex-map>

        </div>

    </div>


</template>

<script>

  import axios from 'axios'

  import { yandexMap, ymapMarker } from 'vue-yandex-maps'

  export default {
    components: {
      yandexMap,
      ymapMarker
    },
    props: {
      value: {},
      coordinates: {},
    },
    data () {
      return {
        currentCoordinates: [52.261543, 104.265431],
          mapAddress: null,
        mapAddressTimeout: null,
          controls:[],
        centerCoodinates: [52.261543, 104.265431],

        mapSettings: {
          apiKey: 'ca064f42-4a24-4bd3-ba47-52337cdf5268',
          lang: 'ru_RU',
          version: '2.1',
            controls: [],
        }
      }
    },
    computed: {},
    watch: {},
    mounted () {

    },
    methods: {

      onMapWasInitialized (map) {

        map.events.add('actiontick', (e) => {

          var tick = e.get('tick')

          let coords = map.options.get('projection').fromGlobalPixels(tick.globalPixelCenter, tick.zoom)

          this.centerCoodinates = coords

          if (this.mapAddressTimeout)
            clearTimeout(this.mapAddressTimeout)

          this.mapAddressTimeout = setTimeout(() => {

            axios.get('https://geocode-maps.yandex.ru/1.x/', {
                params: {
                  apikey: 'ca064f42-4a24-4bd3-ba47-52337cdf5268',
                  geocode: coords.join(','),
                  results: 1,
                  //kind: 'house',
                  format: 'json',
                  sco: 'latlong'
                }
              }
            ).then((response) => {

              let result = []

              if (response.data.response.GeoObjectCollection.featureMember.length) {

                var obj = response.data.response.GeoObjectCollection.featureMember[0]

                if (obj.GeoObject) {
                  result.push(obj.GeoObject)
                }
              }

              if (result.length) {
                this.mapAddress = result[0].name
              }

            }).catch((e) => {


            })

          }, 1000)
        })

      },
      onClick (e) {
        this.currentCoordinates = e.get('coords')
      },


    },
      watch: {
          mapAddress: {

          }
      }
  }
</script>

<style lang="scss" scoped>

    .c-map {
        position: relative;
    }

    .c-map__pointer {
        margin: auto;
        position: absolute;
        top: 0;
        left: 0;
        bottom: 0;
        right: 0;
        z-index: 100;
    }

    .c-map__embed {
        width: 100%;
        height: 100vh;
        filter: grayscale(1);

    }

    .c-closer {

        position: absolute;
        right: 20px;
        top: 20px;
    }
</style>
