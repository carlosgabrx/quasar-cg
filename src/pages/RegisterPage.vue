<template>
  <q-page padding>
    <div>
      <q-form class="row justify-center" @submit.prevent="handleRegister">
      <p class="col-12 text-h5 text-center"> Registro </p>
      <div class="col-md-4 col-sm-6 col-xs-10 q-gutter-y-md">
        <q-input
          label="Name"
          v-model="form.name"
          outlined
        />
        
        <q-input
          label="Email"
          v-model="form.email"
          outlined
        />

        <q-input
          label="Password"
          v-model="form.password"
          outlined
        />

        <div class="full-width">
          <q-btn
          label="Register"
          color="primary"
          class="full-width"
          type="submit"
          outlined
        />
        </div>
      </div>     
    </q-form> 
  </div>
    
  </q-page>
</template>

<script>
import { defineComponent, ref } from 'vue'
import useAuthUser from 'src/composables/useAuthUser'
import { useRouter } from 'vue-router'

export default defineComponent({
  name: 'RegisterPage',

  setup () {
    const router = useRouter()
    const { register } = useAuthUser()

    const form = ref({
      name: '',
      email: '',
      password: ''
    })

    const handleRegister = async () => {
      try {
        await register(form.value)
        router.push({
          name: 'email-confirmation',
          query: { email: form.value.email }
        })
        
      } catch (error) {
        alert(error)
      }
    }
    return {
      form,
      handleRegister
    }
  }
})

</script>
