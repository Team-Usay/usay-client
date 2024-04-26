<template>

  <div class="pa-4 text-center" scrollable>
    <v-dialog max-width="800">
      <template v-slot:activator="{ props: activatorProps }">
        <v-btn
          variant="tonal"
          rounded
          v-bind="activatorProps"
          text="watch"
        ></v-btn>
      </template>

      <template v-slot:default="{ isActive }">
        <v-card title="Use Google's location service?">
          <template v-slot:text>
            Semper wisi et, sollicitudin nunc vestibulum, cursus accumsan nunc
            pede tempus mi ipsum, ligula sed. Non condimentum ac dolor sit.
            Mollis eu aliquam, vel mattis mollis massa ut dolor ante, tempus
            lacinia arcu. Urna vestibulum lorem, nulla fermentum, iaculis ut
            congue ac vivamus. Nam libero orci, pulvinar nulla, enim
            pellentesque consectetuer leo, feugiat rhoncus rhoncus vel. Magna
            sociosqu donec, dictum cursus ullamcorper viverra. Ultricies quis
            orci lorem, suspendisse ut vestibulum integer, purus sed lorem
            pulvinar habitasse turpis.
          </template>

          <v-card-actions>
            <v-spacer></v-spacer>

            <v-btn
              color="surface-variant"
              text="Close"
              variant="flat"
              @click="isActive.value = false"
            ></v-btn>
          </v-card-actions>
        </v-card>
      </template>
    </v-dialog>
  </div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "Record",
});

</script>
