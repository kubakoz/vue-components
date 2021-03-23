<template>
  <li>
    <h2>{{ name }} {{ isFavorite ? '(Favorite)': ''}}</h2>
    <button @click="toggleDetails">{{ detailsAreVisible ? 'Hide' : 'Show' }} Details</button>
    <button @click="toggleFavorite">{{ isFavorite ? 'Unset' : 'Set' }} Fave</button>
    <ul v-if="detailsAreVisible">
      <li>
        <strong>Phone:</strong>
        {{ phoneNumber }}
      </li>
      <li>
        <strong>Email:</strong>
        {{ emailAddress }}
      </li>
      <li>
        <strong>is Fave:</strong>
        {{ isFavorite }}
      </li>
    </ul>
  </li>
</template>

<script>
export default {
  // props: [
  //   'name',
  //   'phoneNumber',
  //   'emailAddress'
  // ], 
  props: {
    id: {
      type: String,
      required: true
    },
    name: {type: String, required: true},
    phoneNumber: String, 
    emailAddress: String,
    isFavorite: {
      type: Boolean, 
      required: false, 
      default: false
    }
  },
  // emits: ['toggle-favorite'],  
  emits: {
    'toggle-favorite': function(id) {
      if(id){
        return true;
      }else{
        console.warn('id is missing');
        return false
      }
    }
  },
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
      //this.isFavorite = !this.isFavorite;
      this.$emit('toggle-favorite', this.id);
    }
  }
};
</script>