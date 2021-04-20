<template>
  <v-card
    class="mx-auto summary-card ma-3 pt-6"
    :class="bgColor"
    dark
    outlined
    tile
    max-width="400"
  >
    <v-img
      class="white--text align-end"
      height="200px"
      src="https://cdn.vuetifyjs.com/images/cards/docks.jpg"
    >
        <div class="icon-wrapper">
            <v-icon>{{ cardIcon }}</v-icon>
        </div>
        <v-card-title class="headline text-bold justify-center">
            <span class="count" :title="cardAmountNew + 'last day'">
              {{ cardAmount }}
            </span>
        </v-card-title>
    </v-img>

    <v-card-subtitle class="pb-0 text-center text-bold">
      {{ cardTitle }}
    </v-card-subtitle>

    <v-card-text class="text--primary">
      <div>Whitehaven Beach</div>

      <div>Whitsunday Island, Whitsunday Islands</div>
    </v-card-text>

    <v-card-actions
      class= "justify-center"
    >
      <v-btn
        color="orange"
        text        
      >
        Share
      </v-btn>

      <v-btn
        color="orange"
        text
      >
        Explore
      </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
  export default {
      name: 'StatCard',
      data () {
          return {}
      },
      props: {
          bgColor: String,
          cardIcon: String,
          cardTitle: String,
          cardAmount: Number,
          cardAmountNew: Number
      }
  }
</script>
<style scoped>
    .text-bold {
        font-weight: 600;
    }
    .icon-wrapper .v-icon {
        margin: auto;
        width: 100%;
        font-size: 2rem;
    }
    .summary-card {
        width: 100%;
        border-radius: 5px;
        box-shadow: 0 0 10px rgba(0,0,0,.25);
    }
        .summary-card .headline {
            width: 100%;
            text-align: center;
        }
</style>