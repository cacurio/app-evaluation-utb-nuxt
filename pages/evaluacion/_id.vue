<template>
  <div>
    <!-- <h1>Hola {{ $route.params.id }} /Hola {{ id }}</h1> -->
    <div>
      <v-row>
        <h1>{{ filterData.standardName }}</h1>

        <v-chip class="ma-2" color="secondary">
          {{ filterData.assessment }}
        </v-chip>
      </v-row>

      <v-row justify="left" align="left">
        <v-chip :ripple="false"> Tipo {{ filterData.type }} </v-chip>
        <v-chip :ripple="false"> Eje {{ filterData.axis }} </v-chip>
        <v-chip :ripple="false"> {{ filterData.dimension }} </v-chip>
      </v-row>
      <v-row>
        <h2>Concepto</h2>
        {{ filterData.concept }}
      </v-row>
    </div>
    <br />
    <br />
    <h2>Elementos fundamentales</h2>
    <v-expansion-panels>
      <v-expansion-panel
        v-for="(item, i) in filterData.fundamentalElement"
        :key="i"
      >
        <v-expansion-panel-header>
          {{ item.name }}
        </v-expansion-panel-header>
        <v-expansion-panel-content>
          <v-chip class="ma-2"> {{ item.assessment }}</v-chip>
          <v-banner two-line>
            {{ item.description }}
          </v-banner>

          <v-row>
            <v-spacer></v-spacer>
            <v-col
              v-for="(d, j) in item.components"
              :key="j"
              cols="12"
              sm="6"
              md="4"
            >
              <v-card>
                <v-card-text>
                  <p class="display-1 text--primary">{{ d.name }}</p>
                  <!-- <p>adjective</p> -->
                  <div class="text--primary">
                    {{ d.description }}
                  </div>
                </v-card-text>
                Cumplido
                <v-chip class="ma-2" color="success" outlined>
                  <!-- <v-icon left> mdi-server-plus </v-icon> -->
                  {{ d.fulfilled }}
                </v-chip>
                <!-- <span
                  class="headline white--text pl-4 pt-4 d-inline-block"
                  v-text="d.name"
                ></span> -->
                <!-- </v-img> -->

                <!-- <v-card-actions class="white justify-center">
                    <v-btn
                      v-for="(social, j) in socials"
                      :key="j"
                      :color="social.color"
                      class="white--text"
                      fab
                      icon
                      small
                    >
                      <v-icon>{{ social.icon }}</v-icon>
                    </v-btn>
                  </v-card-actions> -->
              </v-card>
            </v-col>
          </v-row>
        </v-expansion-panel-content>
      </v-expansion-panel>
    </v-expansion-panels>
    <br />
    <!-- <h2>Fuentes de información</h2>
    <v-card class="mx-auto" max-width="900" tile>
      <v-list-item v-for="item in filterData.InformationSources" :key="item.id">
        <v-list-item-content>
          <v-list-item-title>{{ item.description }}</v-list-item-title>
        </v-list-item-content>
      </v-list-item>
    </v-card> -->
  </div>
</template>

<script>
import jsonData from '../../static/data.json'
export default {
  asyncData({ params }) {
    const id = params.id
    const filterData = jsonData.find((e) => e.id === id)
    return { id, filterData }
  },
}
</script>
