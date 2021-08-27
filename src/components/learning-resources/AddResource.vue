<template>
  <base-dialog v-if="inputIsInvalid" title="Invalid Input" @close='confirmError'>
    <template #default>
      <p>Unfortunatelly some input is invalid</p>
    </template>
    <template #actions>
      <base-button @click="confirmError">Okay</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label>Title</label>
        <input id="title" name="title" type="text" ref="enteredTitle" />
      </div>
      <div class="form-control">
        <label>Description</label>
        <textarea
          id="description"
          name="description"
          rows="3"
          ref="enteredDesc"
        />
      </div>
      <div class="form-control">
        <label>Link</label>
        <input id="link" name="link" type="url" ref="enteredUrl" />
      </div>
      <div>
        <base-button type="submit">Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>


<script>
export default {
  data() {
    return {
      inputIsInvalid: false
    };
  },

  inject: ['addResource'],

  methods: {
    submitData() {
      const title = this.$refs.enteredTitle.value;
      const description = this.$refs.enteredDesc.value;
      const url = this.$refs.enteredUrl.value;
      
      if(title.trim() === '' || description.trim() === '' || url.trim() === '') {
        this.inputIsInvalid = true;
        return;
      }

      this.addResource(title, description, url);
      
    },

    confirmError() {
      this.inputIsInvalid = false;
    }

  },
};
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>