<template>
  <q-page class="q-pa-md">
    <q-form
      class="q-gutter-md"
      style="max-width: 600px"
      @submit="onSubmit"
      @reset="onReset"
    >
      <!-- ชื่อ -->
      <q-input
        filled
        v-model="name"
        label="Your name *"
        hint="Name and surname"
        :rules="[
          val => !!val || 'Please enter your name'
        ]"
      />

      <!-- อายุ -->
      <q-input
        filled
        v-model.number="age"
        type="number"
        label="Your age *"
        :rules="[
          val => val !== null && val !== '' || 'Please enter your age'
        ]"
      />

      <!-- ยอมรับเงื่อนไข -->
      <q-toggle
        v-model="accept"
        label="I accept the license and terms"
      />

      <div>
        <q-btn
          label="SUBMIT (提出する)"
          type="submit"
          color="primary"
        />

        <q-btn
          label="RESET (リセット)"
          type="reset"
          color="primary"
          flat
          class="q-ml-sm"
        />
      </div>
    </q-form>
  </q-page>
</template>

<script setup>
import { ref } from 'vue'
import { useQuasar } from 'quasar'

const $q = useQuasar()
const name = ref('')
const age = ref(null)
const accept = ref(false)

function onSubmit () {
  if (accept.value !== true) {
    $q.notify({
      type: 'negative',
      message: 'You need to accept the license and terms first'
    })
  } else {
    $q.notify({
      type: 'positive',
      message: 'Submitted successfully'
    })
  }
}

function onReset () {
  name.value = ''
  age.value = null
  accept.value = false
}
</script>
