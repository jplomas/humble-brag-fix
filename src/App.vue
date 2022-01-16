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
        <div class="text-danger mt-1" v-if="this.badSettings">Not enough options selected - please check below!</div>      
    <fieldset v-if="checkvalid()">
    <div v-if="!this.badSettings" class="form-group">
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
        Custom: <input @keyup="change()" v-model="g" type="text" class="mini-input">
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
        Custom: <input @keyup="change()" v-model="y" type="text" class="mini-input">
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
        Custom: <input @keyup="change()" v-model="w" type="text" class="mini-input">
      </div>
      <div>
        Wordle =
        <button @click="set('a', 'Humblebrag', $event)" class="btn" :class="check('a', 'Humblebrag')">Humblebrag</button>
        <button @click="set('a', 'W*rdle', $event)" class="btn" :class="check('a', 'W*rdle')">W*rdle</button>
        <button @click="set('a', 'W💍rdle', $event)" class="btn" :class="check('a', 'W💍rdle')">W💍rdle</button>
        <button @click="set('a', 'Wo®️dle', $event)" class="btn" :class="check('a', 'Wo®️dle')">Wo®️dle</button>
        <button @click="set('a', 'W0️⃣rdl€', $event)" class="btn" :class="check('a', 'W0️⃣rdl€')">W0️⃣rdl€</button>
        Custom: <input v-model="a" type="text" class="small-input">
      </div>
    </div>
  </fieldset>
</form>
  </div>
  <div>
    Made with ❤️ in Manchester by <a href="https://twitter.com/jplomas">@jplomas</a> |
    Open Source software: <a href="https://github.com/jplomas/humble-brag-fix">GitHub</a></div>
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
        a: 'Humblebrag',
        badSettings: false,
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
      change() {
        if (this.g === '' || this.y === '' || this.w === '') {
          this.badSettings = true;
        } else {
          this.badSettings = false;
        }
      },
      set(key, value, event) {
        event.preventDefault();
        this.badSettings = false;
        if (key === 'g') {
          this.g = value;
        }
        if (key === 'y') {
          this.y = value;
        }
        if (key === 'w') {
          this.w = value;
        }
        if (key === 'a') {
          this.a = value;
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
        if (key === 'a') {
          if (this.a === value) {
            return 'btn-primary';
          }
        }
        return 'btn-light';
      },
    },
    computed: {
      modify() {
        let newWordle = this.wordle
        if (this.g === '' || this.y === '' || this.w === '') {
          this.badSettings = true;
          return newWordle;
        }
        this.badSettings = false;
        newWordle = newWordle.replace(/Wordle/g, this.a);
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
  .mini-input {
    width: 1.8rem !important
  }
    .small-input {
    width: 6rem !important
  }
  .text-danger {
    color: #ff0039;
  }
</style>
