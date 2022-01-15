<template>
  <div class="container mt-4">
    <div class="card border-primary mb-3">
    <div class="card-header">Apropos of Wordle Twitter humblebrags</div>
    <div class="card-body">
      <h4 class="card-title">Wordle Humblebrag Fix</h4>
      <p class="card-text">Worried your daily Wordle humblebrags are being ignored?</p>
      <p class="card-text">This is a simple fix to make sure your humblebrags are not ignored.</p>
    </div>
    <form class="m-1">
  <fieldset>
    <div class="form-group has-danger">
      <label for="pasteWordle" class="form-label mt-1">Paste your Wordle humblebrag here</label>
      <textarea v-model="wordle" :class="{ 'is-invalid': wordle && !checkvalid() }" class="form-control" id="pasteWordle" rows="8"></textarea>
      <div class="invalid-feedback" v-if="wordle && !checkvalid()">Invalid humblebrag: paste directly from Wordle!</div>
    </div>
  </fieldset>
  
    <fieldset v-if="checkvalid()">
    <div class="form-group">
      <label for="result" class="form-label mt-1">Here's your modified humblebrag</label>
      <textarea v-model="modify" class="form-control" ref="textToCopy" id="result" rows="8"></textarea>
    <button @click="copy" class="btn btn-primary">Copy to clipboard</button>
    </div>
    <div class="mt-1">
      <span class="mt-1"><strong>Options</strong></span>
      <div>
        🟩 =
        <button @click="set('g', '🇸🇦', $event)" class="btn" :class="check('g', '🇸🇦')">🇸🇦</button>
        <button @click="set('g', '💚', $event)" class="btn" :class="check('g', '💚')">💚</button>
        <button @click="set('g', '📗', $event)" class="btn" :class="check('g', '📗')">📗</button>
        <button @click="set('g', '🍏', $event)" class="btn" :class="check('g', '🍏')">🍏</button>
        <button @click="set('g', '🌲', $event)" class="btn" :class="check('g', '🌲')">🌲</button>
        <button @click="set('g', '🥬', $event)" class="btn" :class="check('g', '🥬')">🥬</button>
        <button @click="set('g', '🟢', $event)" class="btn" :class="check('g', '🟢')">🟢</button>
      </div>
      <div>
        🟨 =
        <button @click="set('y', '🇳🇺', $event)" class="btn" :class="check('y', '🇳🇺')">🇳🇺</button>
        <button @click="set('y', '💛', $event)" class="btn" :class="check('y', '💛')">💛</button>
        <button @click="set('y', '🟡', $event)" class="btn" :class="check('y', '🟡')">🟡</button>
        <button @click="set('y', '🌕', $event)" class="btn" :class="check('y', '🌕')">🌕</button>
        <button @click="set('y', '🌞', $event)" class="btn" :class="check('y', '🌞')">🌞</button>
        <button @click="set('y', '👊', $event)" class="btn" :class="check('y', '👊')">👊</button>
        <button @click="set('y', '🤔', $event)" class="btn" :class="check('y', '🤔')">🤔</button>
      </div>
      <div>
        ⬜ =
        <button @click="set('w', '🏳️', $event)" class="btn" :class="check('w', '🏳️')">🏳️</button>
        <button @click="set('w', '🤍', $event)" class="btn" :class="check('w', '🤍')">🤍</button>
        <button @click="set('w', '🔳', $event)" class="btn" :class="check('w', '🔳')">🔳</button>
        <button @click="set('w', '🇨🇾', $event)" class="btn" :class="check('w', '🇨🇾')">🇨🇾</button>
        <button @click="set('w', '🌫️', $event)" class="btn" :class="check('w', '🌫️')">🌫️</button>
        <button @click="set('w', '🍚', $event)" class="btn" :class="check('w', '🍚')">🍚</button>
        <button @click="set('w', '🗯️', $event)" class="btn" :class="check('w', '🗯️')">🗯️</button>
      </div>
    </div>
  </fieldset>
</form>
  </div>
  <div>Open Source software: <a href="https://github.com/jplomas/humble-brag-fix">GitHub</a></div>
</div>
</template>

<script>
  export default {
    data() {
      return {
        wordle: '',
        g: '🇸🇦',
        y: '🇳🇺',
        w: '🏳️',
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
      },
      set(key, value, event) {
        event.preventDefault();
        if (key === 'g') {
          this.g = value;
        }
        if (key === 'y') {
          this.y = value;
        }
        if (key === 'w') {
          this.w = value;
        }
      },
      check(key, value) {
        if (key === 'g') {
          if (this.g === value) {
            return 'btn-primary';
          }
        }
        if (key === 'y') {
          if (this.y === value) {
            return 'btn-primary';
          }
        }
        if (key === 'w') {
          if (this.w === value) {
            return 'btn-primary';
          }
        }
        return 'btn-light';
      },
    },
    computed: {
      modify() {
        let newWordle = this.wordle.replace(/Wordle/g, 'Humblebrag');
        newWordle = newWordle.replace(/🟩/g, this.g);
        newWordle = newWordle.replace(/⬜/g, this.w);
        newWordle = newWordle.replace(/🟨/g, this.y);
        return newWordle
      },
    },
  };
</script>
<style scoped>
  .mt-4 {
    margin-top: 4rem;
  }
  .mt-1 {
    margin-top: 1rem;
  }
  .m-1 {
    margin: 1rem;
  }
  .btn-primary:focus {
    box-shadow: none;
    background-color: #2780e3;
    border-color: #2780e3;
  }
</style>
