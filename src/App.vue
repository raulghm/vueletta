<template>
  <div class="voletta">
    <div class="voletta-body">
      <header>
        <h1>Voletta</h1>
        <p>Calcula tu boleta de honorarios</p>
      </header>

      <main>
        <div class="voletta-input">
          $ <input type="number" v-model="valor" @keyup="procesa" placeholder="0" autofocus="true">
        </div>

        <div class="voletta-bottom">
          <div>
            <h2>Líquido</h2>
            Si lo pactado fue en valores líquidos, <br>
            deberás hacer la boleta por <label>$ {{ liquidoHacer }}</label> y recibirás:
            <label>$ {{ valor }}</label> en efectivo.
          </div>

          <div>
            <h2>Bruto</h2>
            Si lo pactado fue en valores brutos, <br>
            deberás hacer la boleta por <label>$ {{ valor }}</label> y recibirás:
            <label>$ {{ brutoHacer }}</label> en efectivo.
          </div>
        </div>
      </main>

      <footer>
        Desarrollado con Vue 2.x, Webpack 2, PostCSS + cssnext
      </footer>
    </div>
  </div>
</template>

<script>
import accounting from 'accounting';

export default {
  name: 'app',

  data() {
    return {
      valor: null,
      liquidoHacer: 0,
      brutoHacer: 0,
    };
  },

  methods: {
    procesa() {
      const factorBruto = 0.9;
      const factorLiquido = 1.1111111111111112;

      this.liquidoHacer = this.formatMoney(this.valor * factorLiquido);
      this.brutoHacer = this.formatMoney(this.valor * factorBruto);
    },
    formatMoney(value) {
      return accounting.formatMoney(value, '', 0, '.'); // $4.999;
    },
  },
};
</script>

<style>
@import 'suitcss-base';

:root {
  /* Brand colors */
  --color-primary: #4fc08d;
  --color-secondary: #4eb7a8;
  --color-success: #70c7be;
  --color-info: #3498db;
  --color-warning: #fbbe41;
  --color-danger: #e84949;

  /* Basic colors */
  --color-white: #fff;
  --color-black: #232323;

  /* Gray colors */
  --color-gray-darker: #222;
  --color-gray-dark: #333;
  --color-gray: #555;
  --color-gray-light: #bbb;
  --color-gray-lighter: #eee;

  /* Base variables */
  --background-color-base: #fff;
  --font-weight-base: 600;
  --color-base: var(--color-white);
  --font-family-serif: 'Source Sans Pro', Helvetica, Arial, sans-serif;
  --font-family-base: var(--font-family-serif);
  --link-color-base: var(--color-primary);
  --font-size-base: 18px;
  --border-radius: 4px;
}

html,
body {
  height: 100%;
}

body {
  font-family: var(--font-family-serif);
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-color: var(--color-primary);
  color: var(--color-base);
  font-size: var(--font-size-base);
  font-weight: var(--font-weight-base);
}

.voletta {
  display: flex;
  align-items: center;
  justify-content: center;
  height: inherit;
  padding: 20px;
}

.voletta-body {
  flex: 1;
}

header {
  margin-bottom: 20px;
}

.voletta-input {
  font-size: 2rem;
  margin-bottom: 20px;
}

.voletta-input input {
  padding: 20px;
  font-size: 2rem;
  max-width: 80%;
  margin: 0 auto;
  border-radius: var(--border-radius);
  border: 2px solid color(var(--color-primary) b(40%));
  outline: 0;
}

.voletta-bottom h2 {
  margin-top: 1.2rem;
}

h1,
h2 {
  margin-bottom: 1rem;
}

h1 {
  font-size: 3rem;
  font-weight: 300;
}

label {
  color: var(--color-primary);
  border-radius: var(--border-radius);
  background-color: var(--color-white);
  padding: 0 4px;
  display: inline-block;
  font-size: 1.2rem;
}

footer {
  margin-top: 80px;
  border-top: 1px solid var(--color-white);
  padding: 20px;
  font-size: 1rem;
  opacity: .6;
}
</style>
