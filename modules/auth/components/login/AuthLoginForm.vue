<script setup lang="ts">
import {
  AppText,
  FormInput,
  FormPasswordInput,
} from '@wisemen/vue-core'
import type { Form } from 'formango'
import { useI18n } from 'vue-i18n'

import type { CurrentUser } from '@/models/auth/current-user/currentUser.model'
import type { loginFormSchema } from '@/models/auth/login/loginForm.model'

const props = defineProps<{
  form: Form<typeof loginFormSchema>
  lastLoggedInUser: CurrentUser | null
}>()

const { t } = useI18n()

const email = props.form.register('email', props.lastLoggedInUser?.email)
const password = props.form.register('password')
</script>

<template>
  <AppForm :form="form">
    <AppFormElementSpacer>
      <FormInput
        v-bind="email"
        :is-required="true"
        :label="t('form.fields.email')"
        placeholder="email@example.com"
        type="email"
      />

      <FormPasswordInput
        v-bind="password"
        :is-required="true"
        :label="t('form.fields.password')"
        :placeholder="t('form.fields.password')"
      />

      <NuxtLinkLocale
        to="/auth/forgot-password"
        class="py-2"
      >
        <AppText
          class="font-medium text-primary"
          variant="subtext"
        >
          {{ t('auth.login.forgot_password') }}
        </AppText>
      </NuxtLinkLocale>
    </AppFormElementSpacer>

    <AuthFormSubmitButton :form="form">
      {{ t('auth.login.log_in') }}
    </AuthFormSubmitButton>
  </AppForm>
</template>
