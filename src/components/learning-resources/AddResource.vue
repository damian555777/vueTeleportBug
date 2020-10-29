<template>
  <BaseCard>
    <form v-on:submit.prevent="submitData">
      <div class="form-control">
        <label for="title">Title</label>
        <input id="title" name="title" type="text" ref="titleInput" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea
          id="description"
          name="description"
          rows="3"
          ref="descInput"
        />
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input id="link" name="link" type="url" ref="linkInput" />
      </div>
      <div class="form-control">
        <BaseButton>Add Resource</BaseButton>
      </div>
    </form>
  </BaseCard>
  <BaseDialog v-if="inputIsInvalid" v-on:close-dialog="confirmError">
    <template v-slot:header>
      Input Error
    </template>
    <template v-slot:default>
      <p>
        Unfortunately, at least one input value is invalid.
      </p>
      <p>
        Please check all inputs and make sure you entered at least a few
        characters into each input field.
      </p>
    </template>
    <template v-slot:actions>
      <BaseButton v-on:click="confirmError">Okay</BaseButton>
    </template>
  </BaseDialog>
</template>

<script>
  import BaseCard from '../UI/BaseCard'
  import BaseButton from '../UI/BaseButton'
  import BaseDialog from '../UI/BaseDialog'

  export default {
    components: {
      BaseCard,
      BaseButton,
      BaseDialog,
    },
    data() {
      return {
        inputIsInvalid: false,
      }
    },
    inject: ['addResource'],
    methods: {
      submitData() {
        const enteredTitle = this.$refs.titleInput.value
        const enteredDesc = this.$refs.descInput.value
        const enteredLink = this.$refs.linkInput.value
        if (
          !enteredTitle ||
          enteredTitle.trim() === '' ||
          !enteredDesc ||
          enteredDesc.trim() === '' ||
          !enteredLink ||
          enteredLink.trim() === ''
        ) {
          this.inputIsInvalid = true
        } else {
          this.addResource(enteredTitle, enteredDesc, enteredLink)
          this.$refs.titleInput.value = ''
          this.$refs.descInput.value = ''
          this.$refs.linkInput.value = ''
        }
      },
      confirmError() {
        this.inputIsInvalid = false
      },
    },
  }
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
