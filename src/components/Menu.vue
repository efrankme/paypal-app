<template>
  <q-list>
        <q-item-label header class="text-grey-8"></q-item-label>
        <q-item clickable to="/">
          <q-item-section avatar>
            <q-icon name="web_asset" />
          </q-item-section>

          <q-item-section>
            <q-item-label>Calculadora</q-item-label>
          </q-item-section>
        </q-item>

        <q-item clickable tag="a" to="/acerca">
          <q-item-section avatar>
            <q-icon name="account_box" />
          </q-item-section>

          <q-item-section>
            <q-item-label>Acerca</q-item-label>
          </q-item-section>
        </q-item>
      </q-list>
</template>

<script>
export default {
  name: 'Menu'
}
</script>
