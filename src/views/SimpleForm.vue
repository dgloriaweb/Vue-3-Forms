<template>
  <div>
    <h1>Create an event</h1>
    <form @submit.prevent="sendForm">
      <BaseSelect
        :options="categories"
        v-model="event.category"
        label="Select a category"
      />
      <h3>Name & describe your event</h3>

      <BaseInput v-model="event.title" label="Title" type="text" />
      <BaseInput v-model="event.description" label="Description" type="text" />

      <h3>Where is your event?</h3>

      <BaseInput v-model="event.location" label="Location" type="text" />

      <h3>Are pets allowed?</h3>
      <BaseRadioGroup v-model="event.pets" name="pets" :options="petOptions" />

      <h3>Extras</h3>
      <div>
        <BaseCheckbox v-model="event.extras.catering" label="Catering" />
      </div>

      <div>
        <BaseCheckbox v-model="event.extras.music" label="Live music" />
      </div>

      <button class="button -fill-gradient" type="submit">Submit</button>
    </form>
  </div>
</template>

<script>
import BaseInput from "../components/BaseInput.vue";
import axios from "axios";
export default {
  components: { BaseInput },
  data() {
    return {
      categories: [
        "sustainability",
        "nature",
        "animal welfare",
        "housing",
        "education",
        "food",
        "community"
      ],
      event: {
        category: "",
        title: "",
        description: "",
        location: "",
        pets: 1,
        extras: {
          catering: false,
          music: false
        }
      },
      petOptions: [
        {
          label: "Yes",
          value: 1
        },
        {
          label: "No",
          value: 0
        },
        {
          label: "Maybe",
          value: 2
        }
      ]
    };
  },
  methods: {
    sendForm() {
      axios
        .post(
          "https://my-json-server.typicode.com/dgloriaweb/testRestApi/events",
          this.event
        )
        .then(function(response) {
          console.log("Response", response);
        })
        .catch(function(err) {
          console.log("Error", err);
        });
    }
  }
};
</script>
