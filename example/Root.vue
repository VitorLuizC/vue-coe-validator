<template>
  <div id="app">
    <section>
      <h3>form1</h3>
      <form name="form1" @prevent.stop>
        <c-input
          name="input1"
          label="input1"
          :validation="$hasError('input1', 'form1')"
          v-model="form1.input1"
        />

        <c-input
          name="input2"
          label="input2"
          :validation="$hasError('input2', 'form1')"
          v-model="form1.input2"
        />
      </form>

      <button @click="submit1('form1')">salvar</button>
    </section>

    <section>
      <h3>form2</h3>
      <form name="form2" @prevent.stop>
        <c-input
          name="input1"
          label="input1"
          :validation="$hasError('input1', 'form2')"
          v-model="form2.input1"
        />
      </form>

      <button @click="submit2('form2')">salvar</button>
    </section>
  </div>
</template>

<script>
// components
import CInput from './components/CInput'

// mixins
import { formSetup } from 'vue-coe-validator'

export default {
  name: 'root',

  mixins: [ formSetup ],

  components: { CInput },

  data () {
    return {
      form1: { input1: '', input2: '22' },
      form2: { input1: '33' }  
    }
  },

  validation: {
    form1: {
      input1: {
        required: true,
        alphabetic: true
      },
      input2: {
        required: true,
        pattern: /^[A-Z0-9_'%=+!`#~$*?^{}&|-]+([.][A-Z0-9_'%=+!`#~$*?^{}&|-]+)*@[A-Z0-9-]+(\.[A-Z0-9-]+)+$/i
      }
    },
    form2: {
      input1: {
        required: true,
        alpha: true
      }
    }
  }

  // methods: {
  //   submit1 (form) {
  //     this.$allTouched(form)
  //     const isValid = this.$isValidForm(form)

  //     if (isValid) {
  //       console.log('save data form1')
  //     }
  //   },
  //   submit2 (form) {
  //     this.$allTouched(form)
  //     const isValid = this.$isValidForm(form)

  //     if (isValid) {
  //       console.log('save data form2')
  //     }
  //   }
  // }
}
</script>

<style>
.input { margin-bottom: 15px; }
</style>
