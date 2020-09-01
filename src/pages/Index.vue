<template>
  <q-page class="q-pa-sm">
    <section class="q-mb-md q-col-gutter-sm">
      <div class="row">
        <div class="col text-subtitle1 text-primary text-center ">Tasas</div>
      </div>
      <div class="row q-col-gutter-md">
        <div class="col">
          <q-input
            type="number"
            label="% Comisión"
            outlined
            v-model.number="porcentaje"
          />
        </div>
        <div class="col">
          <q-input type="number" label="$ Fee" outlined v-model.number="tasa" />
        </div>
      </div>
    </section>

    <q-separator spaced />

    <section class="q-gutter-sm q-my-md">
      <div class="row">
        <div class="col text-subtitle1 text-primary text-center">
          Cálculo para recibir
        </div>
      </div>

      <div class="row">
        <div class="col-6 offset-3">
          <q-input
            type="number"
            label="Para recibir:"
            clearable
            outlined
            v-model.number="paraRecibir"
            @keyup="calculoRecibir"
          />
        </div>
      </div>

      <div class="row">
        <div class="col-6 offset-3">
          <q-input
            type="number"
            label="Hay que enviar:"
            outlined
            v-model.number="hayqEnviar"
            readonly
          />
        </div>
      </div>

      <div class="row">
        <div class="col-6 offset-3">
          <q-input
            type="number"
            label="Comisión:"
            outlined
            v-model.number="comiRecibir"
            readonly
          />
        </div>
      </div>
    </section>

    <q-separator spaced />

    <section class="q-gutter-sm q-my-md">
      <div class="row">
        <div class="col text-subtitle1 text-primary text-center">
          Cálculo para enviar
        </div>
      </div>

      <div class="row">
        <div class="col-6 offset-3">
          <q-input
            type="number"
            label="Si se envían:"
            outlined
            clearable
            v-model.number="seEnvian"
            @keyup="calculoEnviar"
          />
        </div>
      </div>

      <div class="row">
        <div class="col-6 offset-3">
          <q-input
            type="number"
            label="Se reciben:"
            outlined
            v-model.number="seReciben"
            readonly
          />
        </div>
      </div>

      <div class="row">
        <div class="col-6 offset-3">
          <q-input
            type="number"
            label="Comisión:"
            outlined
            v-model.number="comiEnviar"
            readonly
          />
        </div>
      </div>
    </section>
  </q-page>
</template>

<script>
export default {
  name: "PageIndex",
  data() {
    return {
      porcentaje: 5.4,
      tasa: 0.3,
      paraRecibir: null,
      hayqEnviar: null,
      comiRecibir: null,
      seEnvian: null,
      seReciben: null,
      comiEnviar: null
    };
  },

  methods: {
    calculoRecibir() {
      if (this.paraRecibir == "" || this.paraRecibir == 0) {
        this.hayqEnviar = null;
        this.comiRecibir = null;
      } else {
        this.hayqEnviar = this.formatNumero((100 * (this.tasa + this.paraRecibir)) / (-this.porcentaje + 100));
        this.comiRecibir = this.formatNumero(this.hayqEnviar - this.paraRecibir);
      }
    },

    calculoEnviar() {
      this.seReciben = this.formatNumero(
        this.seEnvian - ((this.porcentaje * this.seEnvian) / 100 + this.tasa)
      );
      this.comiEnviar = this.formatNumero(this.seEnvian - this.seReciben);
    },

    formatNumero(valor) {
      return Math.round(valor * 100) / 100;
    }
  }
};
</script>
