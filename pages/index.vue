<script lang="ts" setup>
import { object, string, mixed } from 'yup'

const schema = [
  object({
    firstName: string().required('First Name is required'),
    lastName: string().required('Last Name is required.'),
    email: string().required('Email address is required.').email('Invalid email.'),
    password: string().required('Password is required.').min(10, 'Minimum of 10 characters')
  }),
  object({
    companyName: string().required('Company Name is required.'),
    linkedIn: string().required('Linked in link is required.').url('Invalid URL'),
    website: string().required('Website field is required.').url('Invalid URL'),
    companyLogo: mixed().required('Company Logo is required.'),
    termsAndConditions: string().required()
  })
]

const loading = ref(false)

function createAnAccount (formData: object) {
  loading.value = true
  setTimeout(() => {
    loading.value = false
    console.log(formData)
  }, 2000)
}

/*
CPU - 125595 ,
Motherboard - 12995
GPU - 34995 - 3 fans 31995 dual
RAM - GSkill 3600  - 5995
SSD - 3495
PSU - 6495
Daskflash dlx21 - 4195

09173141342

*/


</script>
<template>
  <div class="h-screen grid place-items-center">
    <div class="w-full max-w-xl rounded">
      <h1 class="text-[30px] font-bold text-zinc-800 text-center">
        Composition API
      </h1>
      <div>
        <FormWizard
          :validation-schema="schema"
          :loading="loading"
          @submit="createAnAccount"
        >
          <FormStep>
            <FormField
              name="firstName"
              label="First Name"
              placeholder="Reagan"
            />
            <FormField
              name="lastName"
              label="Last Name"
              placeholder="Mahinay"
              class="mt-4"
            />
            <FormField
              name="email"
              label="Email Address"
              placeholder="reagan@gmail.com"
              class="mt-4"
              type="email"
            />
            <FormField
              name="password"
              label="Password"
              placeholder="********"
              class="mt-4"
              type="password"
            />
          </FormStep>
          <FormStep>
            <FormField
              label="Company Name"
              name="companyName"
            />
            <FormField
              label="LinkedIn"
              name="linkedIn"
              class="mt-4"
            />
            <FormField
              label="Website"
              name="website"
              class="mt-4"
            />
            <FormFile
              label="Company Logo"
              name="companyLogo"
              class="mt-4"
            />
            <FormCheckbox
              name="termsAndConditions"
              :value="true"
              class="mt-4"
            >
              I agree with the <NuxtLink class="text-blue-500">
                terms and conditions
              </NuxtLink>
            </FormCheckbox>
          </FormStep>
        </FormWizard>
      </div>
    </div>
  </div>
</template>
<style scoped lang="css"></style>
