<template>
<section class="hero is-dark is-large">
<div class="hero-body is-mobile">
    <div class="container">
        <center><gmap-map
    :center="center"
    :zoom="15"
    style="width: 100%px; height: 500px"
  >
  <gmap-info-window :options="infoOptions" :position="infoWindowPos" :opened="infoWinOpen" @closeclick="infoWinOpen=false">
        {{infoContent}}
      </gmap-info-window>
  <gmap-polygon :paths="paths">
      </gmap-polygon>
    <gmap-marker
      :key="i"
      v-for="(m, i) in markers"
      :position="m.position"
      :clickable="true"
      @click="toggleInfoWindow(m,i)"
    ></gmap-marker>
  </gmap-map></center>  
  <center>
      <h2 class="subtitle">
        Reporta tus incidentes</h2>
        <button class="button is-danger is-medium"
            @click="isModalActive = true">
            Reportar incidente
        </button>
        <b-modal :active.sync="isModalActive" :width="moda">
            <form action="">
              <div class="modal-card">
                  <header class="modal-card-head">
                      <p class="modal-card-title">Reportar incidente</p>
                  </header>
                  <section class="modal-card-body">
                      <b-field label="Titulo">
                          <b-input
                              type="text"
                              v-model="titulo"
                              placeholder="Titulo del incidente"
                              required>
                          </b-input>
                      </b-field>

                  <b-field>
                  <b-radio-button v-model="radioButton"
                      native-value="Robo"
                      type="is-danger">
                      <span>Robo</span>
                  </b-radio-button>

                  <b-radio-button v-model="radioButton"
                      native-value="Secuestro"
                      type="is-danger">
                      <span>Secuestro</span>
                  </b-radio-button>

                  <b-radio-button v-model="radioButton"
                      native-value="Pelea"
                      type="is-danger">
                      Pelea
                  </b-radio-button>
                  <b-radio-button v-model="radioButton"
                      native-value="Asesinato"
                      type="is-danger">
                      Asesinato
                  </b-radio-button>
                  <p class="content nigru">
                    <b> Seleccion:</b>
            {{ radioButton }}
              </p>
                  </b-field>     
                 <b-field label="Descripcion">
                    <b-input
                        type="text"
                        v-model="desc"
                        placeholder="Descripcion del incidente"
                        required>
                    </b-input>
                </b-field>

                
            </section>
            <footer class="modal-card-foot">           
                <button class="button" type="button">Cerrar</button>
                <button class="button is-primary">Enviar</button>
            </footer>
        </div>
    </form>
        </b-modal>
  </center>    
    </div>
  </div>
  
</section>
</template>



 

<script>  
  export default {
       data () {
          return {    
            isModalActive: false,
                isModalActive: false,
                radioButton: '',
                titulo:'',
                desc:'',
                moda:'80%',    
            center: {lat: -8.1285196, lng: -79.0278064},  
            infoContent: '5',
            infoWindowPos: {
              lat: 0,
              lng: 0
            },      
            infoWinOpen: false,
            currentMidx: null,
             infoOptions: {
            pixelOffset: {
              width: 0,
              height: -35
            }
          },
             paths: [
                        [ {lat: -8.125, lng: -79.0250}, {lat: -8.1235196, lng: -79.035}, {lat: -8.130, lng: -79.035}, {lat: -8.130, lng: -79.025} ],
                      ],
             
              markers: [{
            position: {lat: -8.1274836, lng: -79.0319926},
            infoText: 'Marker 1'
          }, {
            position: {lat: -8.1288996, lng: -79.0312268},
            infoText: 'Marker 2'
          }, {
            position: {lat: -8.1285196, lng: -79.0278064},
            infoText: 'Marker 3'
          }] 
         

           
          }
        },
        methods: {
          toggleInfoWindow: function(marker, idx) {
            this.infoWindowPos = marker.position;
            this.infoContent = "marker.infoText";
            //check if its the same marker that was selected if yes toggle
            if (this.currentMidx == idx) {
              this.infoWinOpen = !this.infoWinOpen;
            }
            //if different marker set infowindow to open and reset current marker index
            else {
              this.infoWinOpen = true;
              this.currentMidx = idx;
            }
          }
        }

     
      }
</script>


<style scoped>
  .nigru {
   color:black;  
  }
   .modal-card {
        width: auto;
    }
</style>
