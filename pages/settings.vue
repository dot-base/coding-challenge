<template>
  <div>
    <h1 class="text-3xl mb-2">User Settings</h1>
    <p class="text-md mb-4">
      Update your personal information below. You can change your name and email
      address.
    </p>

    <Form
      v-slot="$form"
      :resolver="resolver"
      :initialValues="initialValues"
      @submit="onFormSubmit"
      class="flex flex-col gap-4 w-full"
    >
      <ControlledTextInput
        name="firstName"
        label="First Name"
        placeholder="First Name"
        type="text"
        fluid
        :invalid="$form.firstName?.invalid"
        :errorMessage="$form.firstName?.error?.message"
      />
      <ControlledTextInput
        name="lastName"
        label="Last Name"
        placeholder="Last Name"
        type="text"
        fluid
        :invalid="$form.lastName?.invalid"
        :errorMessage="$form.lastName?.error?.message"
      />

      <ControlledTextInput
        name="email"
        label="Email"
        placeholder="Email"
        type="text"
        fluid
        :invalid="$form.email?.invalid"
        :errorMessage="$form.email?.error?.message"
      />

      <Button type="submit" severity="secondary" label="Submit" />
    </Form>
  </div>
</template>

<script setup lang="ts">
const { data } = await useFetch("/api/user");

import { ref } from "vue";
import { zodResolver } from "@primevue/forms/resolvers/zod";
import { useToast } from "primevue/usetoast";
import { z } from "zod";

const toast = useToast();
const initialValues = ref({
  firstName: data.value?.firstName,
  lastName: data.value?.lastName,
  email: data.value?.email,
});

const resolver = ref(
  zodResolver(
    z.object({
      firstName: z.string().min(1, { message: "First name is required." }),
      lastName: z.string().min(1, { message: "Last name is required." }),
      email: z
        .string()
        .min(1, { message: "Email is required." })
        .email({ message: "Invalid email address." }),
    }),
  ),
);

const onFormSubmit = ({ valid }: { valid: boolean }) => {
  if (valid) {
    alert(`Form is submitted. ${valid}`);
  }
};
</script>
