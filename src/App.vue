<template>
  <v-app >
    <v-content>
      <Container/>
    </v-content>
  </v-app>
</template>

<script>
import Container from './components/Container';

export default {
  name: 'App',

  components: {
    Container,
  },

  data: () => ({
    //
  }),
};
</script>
