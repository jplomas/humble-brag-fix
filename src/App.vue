<template>
  <div class="container mt-5">
    <div class="card border-primary mb-3">
    <div class="card-header">Apropos of Wordle Twitter humblebrags</div>
    <div class="card-body">
      <h4 class="card-title">Wordle Humblebrag Fix</h4>
      <p class="card-text">Worried your daily Wordle humblebrags are being ignored?</p>
      <p class="card-text">This is a simple fix to make sure your humblebrags are not ignored.</p>
    </div>
    <form class="m-3">
  <fieldset>
    <div class="form-group has-danger">
      <label for="pasteWordle" class="form-label mt-4">Paste your Wordle humblebrag here</label>
      <textarea v-model="wordle" :class="{ 'is-invalid': wordle && !checkvalid() }" class="form-control" id="pasteWordle" rows="8"></textarea>
      <div class="invalid-feedback" v-if="wordle && !checkvalid()">Invalid humblebrag: paste directly from Wordle!</div>
    </div>
  </fieldset>
  
    <fieldset v-if="checkvalid()">
    <div class="form-group">
      <label for="result" class="form-label mt-4">Here's your modified humblebrag</label>
      <textarea v-model="modify" class="form-control" ref="textToCopy" id="result" rows="8"></textarea>
    <button @click="copy" class="btn btn-primary">Copy to clipboard</button>
    </div>
    <p class="mt-4">
      Customised emoji substitution? That would just be overengineering... 🤔
    </p>
  </fieldset>
</form>
  </div>
</div>
</template>

<script>
  export default {
    data() {
      return {
        wordle: "",
      };
    },
    methods: {
      checkvalid() {
        if (this.wordle.includes('Wordle')) {
          return true;
        }
        return false;
      },
      copy(event) {
        event.preventDefault();
        this.$refs.textToCopy.focus();
        this.$refs.textToCopy.select();
        document.execCommand('copy');
      }
    },
    computed: {
      modify() {
        let newWordle = this.wordle.replace(/Wordle/g, 'Humblebrag');
        newWordle = newWordle.replace(/🟩/g, '🇸🇦');
        newWordle = newWordle.replace(/⬜/g, '🏳️');
        newWordle = newWordle.replace(/🟨/g, '🇳🇺');
        return newWordle
      },
    },
  };
</script>

