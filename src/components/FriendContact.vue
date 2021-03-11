<template>
  <li>
    <h2>{{ name }} {{ isFavorite ? '(Favorite)' : '' }}</h2>
    <button @click="toggleFavorite">Toggle Favorite</button>
    <button @click="toggleDetails">{{ detailsAreVisible ? 'Hide' : 'Show' }} Details</button>
    <ul v-if="detailsAreVisible">
      <li>
        <strong>Phone:</strong>
        {{ phoneNumber }}
      </li>
      <li>
        <strong>Email:</strong>
        {{ emailAddress }}
      </li>
    </ul>
    <button @click="deletFriend">Delete</button>
  </li>
</template>

<script>
export default {
  /*props: [
    'name',
    'phoneNumber',
    'emailAddress',
    'isFavorite'
  ],*/
  //or Props as JS objects
  props: {
    id: {
      type: String,
      required: true
    },
    name: {
      type: String,
      required: true
    },
    phoneNumber: {
      type: String,
      required: true
    },
    emailAddress: {
      type: String,
      required: true
    },
    isFavorite: {
      type: Boolean,
      required: false,
      default: false,
    },
  },
  emits: ['toggle-favorite', 'delete'],
   /* emits: {
     'toggle-favorite': function(id) {
       if (id) {
         return true;
       } else {
         console.warn('ID is missing!');
         return false;
       }
     }
   }, */
  //emits define which custom events the component will emit
//prop names should be different than data property names
//see the difference between phone and phoneNumber

  data() {
    return {
      detailsAreVisible: false
    };
  },
  methods: {
    toggleDetails() {
      this.detailsAreVisible = !this.detailsAreVisible;   
    },
    toggleFavorite() {
      this.$emit('toggle-favorite', this.id); 
    },
    deleteFriend() {
      this.$emit('delete', 'id');
    }
  },
};
</script>