<template>
  <div class="voletta">
    <div class="voletta-body">
      <header>
        <img src="https://vuejs.org/images/logo.png">
        <h1>Voletta</h1>
        <p>Calcula tu boleta de honorarios</p>
      </header>

      <main>
        <div class="voletta-input">
          <input type="number" v-model.number="valor" placeholder="$" autofocus="true" @keyup="procesa">
        </div>

        <div class="voletta-bottom">
          <h2>Líquido</h2>
          Si lo pactado fue en valores líquidos, <br>
          deberás hacer la boleta por <label>$ {{ liquidoHacer | formatMoney }}</label> y recibirás:
          <label>$ {{ valor | formatMoney }}</label> en efectivo.

          <h2>Bruto</h2>
          Si lo pactado fue en valores brutos, <br>
          deberás hacer la boleta por <label>$ {{ valor | formatMoney }}</label> y recibirás:
          <label>$ {{ brutoHacer | formatMoney }}</label> en efectivo.
        </div>
      </main>

      <footer>
        Desarrollado con Vue 2, Webpack 2, PostCSS + cssnext
      </footer>

      <a href="https://github.com/raulghm/voletta"><img style="position: absolute; top: 0; right: 0; border: 0;" src="https://camo.githubusercontent.com/38ef81f8aca64bb9a64448d0d70f1308ef5341ab/68747470733a2f2f73332e616d617a6f6e6177732e636f6d2f6769746875622f726962626f6e732f666f726b6d655f72696768745f6461726b626c75655f3132313632312e706e67" alt="Fork me on GitHub" data-canonical-src="https://s3.amazonaws.com/github/ribbons/forkme_right_darkblue_121621.png"></a>
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
      // Factores para calculo
      const factorBruto = 0.9;
      const factorLiquido = 1.1111111111111112;

      // Calculo y asignacion de valores
      this.liquidoHacer = this.valor * factorLiquido;
      this.brutoHacer = this.valor * factorBruto;
    },
  },

  filters: {
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

body {
  font-family: var(--font-family-serif);
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-color: var(--color-primary);
  color: var(--color-base);
  font-size: var(--font-size-base);
  font-weight: var(--font-weight-base);
  line-height: 1.3;
}

h1,
h2 {
  margin-bottom: 1rem;
}

h1 {
  font-size: 3rem;
  font-weight: 300;
}

.voletta {
  padding: 20px;
}

.voletta-body {
  flex: 1;
}

header {
  margin-bottom: 20px;
}

header img {
  max-width: 100px;
}

.voletta-input {
  font-size: 2rem;
  margin-bottom: 20px;
}

.voletta-input input {
  padding: 16px 20px;
  font-size: 2.2rem;
  max-width: 80%;
  margin: 0 auto;
  border-radius: var(--border-radius);
  box-shadow: 0 0 4px color(var(--color-primary) b(40%)) inset;
  border: 2px solid color(var(--color-primary) b(40%));
  outline: 0;
}

.voletta-bottom h2 {
  margin-top: 1.2rem;
}

label {
  color: var(--color-primary);
  border-radius: var(--border-radius);
  background-color: var(--color-white);
  padding: 0 4px;
  display: inline-block;
  font-size: 1.4rem;
  vertical-align: middle;
  margin-bottom: 1px;
}

footer {
  margin-top: 80px;
  border-top: 1px solid var(--color-white);
  padding: 20px;
  font-size: 1rem;
  opacity: .6;
}
</style>
