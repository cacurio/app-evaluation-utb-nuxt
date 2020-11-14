<template>
  <v-container style="max-width: 600px">
    <v-timeline dense clipped>
      <v-timeline-item fill-dot class="white--text mb-12" color="green" large>
        <template v-slot:icon>
          <span>{{ brandName }}</span>
        </template>
        <v-text-field
          v-model="input"
          hide-details
          flat
          :label="institutionName"
          solo
          @keydown.enter="comment"
        >
          <template v-slot:append> </template>
        </v-text-field>
      </v-timeline-item>

      <v-slide-x-transition group>
        <v-timeline-item
          v-for="event in timeline"
          :key="event.id"
          class="mb-4"
          color="pink"
          small
        >
          <v-row justify="space-between">
            <v-col cols="7" v-text="event.text"></v-col>
            <v-col class="text-right" cols="5" v-text="event.time"></v-col>
          </v-row>
        </v-timeline-item>
      </v-slide-x-transition>

      <v-timeline-item class="mb-6" hide-dot>
        <span>{{ title }}</span>
      </v-timeline-item>

      <v-timeline-item
        v-for="item in standards"
        :key="item.id"
        class="mb-4"
        color="grey"
        icon-color="grey lighten-2"
        small
      >
        <v-row justify="space-between">
          <v-col cols="7">
            <!-- <v-chip
              class="white--text ml-0"
              color="green darken-4"
              label
              small
            >
          
            </v-chip> -->
            {{ item.name }}

            <br class="pa-md-5" />
            <p class="font-weight-light">
              Valoración
              <v-chip class="white--text ml-0" color="orange" label outlined>
                {{ item.assessment }}
              </v-chip>
            </p>
          </v-col>
          <v-col class="text-right" cols="5">
            <v-btn
              nuxt
              :to="{ name: 'evaluacion-id', params: { id: item.id } }"
              class="mx-0"
            >
              Ver
            </v-btn>
          </v-col>
        </v-row>
      </v-timeline-item>
    </v-timeline>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    title: 'EVALUACIÓN INSTITUCIONAL EXTERNA 2019',
    institutionName: 'UNIVERSIDAD TÉCNICA DE BABAHOYO',
    brandName: 'UTB',
    standards: [],
  }),

  mounted() {
    this.getStandards()
  },

  methods: {
    async getStandards() {
      try {
        const snapshot = await this.$fire.firestore
          .collection('standards')
          .orderBy('order')
          .get()
        const standards = []
        snapshot.forEach((doc) => {
          const standardsData = doc.data()
          standardsData.id = doc.id
          standards.push(standardsData)
        })
        this.standards = standards
        // eslint-disable-next-line no-console
        console.log(this.standards)
      } catch (error) {
        // eslint-disable-next-line no-console
        console.log(error)
      }
    },
  },
}
</script>
