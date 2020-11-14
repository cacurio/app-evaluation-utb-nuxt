<template>
  <div>
    <!-- <h1>Hola {{ $route.params.id }} /Hola {{ id }}</h1> -->
    <div>
      <v-row>
        <h1 class="pl-2">{{ filterData.standardName }}</h1>

        <v-chip class="ma-2" color="grey lighten-1" text-color="brown darken-4">
          {{ filterData.assessment }}
        </v-chip>
        <v-card-text>
          <div>{{ filterData.description }}</div>
        </v-card-text>
      </v-row>

      <v-row justify="left" align="left">
        <v-chip class="ma-2" :ripple="false">
          Tipo {{ filterData.type }}
        </v-chip>
        <v-chip class="ma-2" :ripple="false">
          Eje {{ filterData.axis }}
        </v-chip>
        <v-chip class="ma-2" :ripple="false">
          {{ filterData.dimension }}
        </v-chip>
        <v-chip class="ma-2" :ripple="false">
          {{ filterData.component }}
        </v-chip>
      </v-row>
      <v-row>
        <h2 class="pa-2">Concepto</h2>
      </v-row>
      <v-row>
        <p class="pl-2 pr-2">{{ filterData.concept }}</p>
      </v-row>
    </div>
    <br />
    <h2 class="pb-2">Elementos fundamentales</h2>
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
                <v-card-title> {{ d.name }} </v-card-title>
                <v-card-text>
                  <!-- <p>adjective</p> -->
                  <div class="text--primary">
                    {{ d.description }}
                  </div>
                </v-card-text>
                <v-chip class="ma-2" color="primary">
                  {{ d.fulfilled }} cumplido
                </v-chip>
              </v-card>
            </v-col>
          </v-row>
        </v-expansion-panel-content>
      </v-expansion-panel>
    </v-expansion-panels>
    <br />
    <v-card>
      <v-toolbar color="" dark dense flat>
        <v-toolbar-title class="body-2"> Observación</v-toolbar-title>
      </v-toolbar>
      <v-card-text>
        {{ filterData.observation }}
      </v-card-text>
    </v-card>
  </div>
</template>

<script>
import jsonData from '../../static/data.json'
export default {
  asyncData({ params }) {
    const id = params.id
    const filterData = jsonData.find((e) => e.sku === id)
    return { id, filterData }
  },
}
</script>
