<script setup>
const email = ref("");
const password = ref("");

const supabase = useSupabaseClient();
const user = useSupabaseUser();

const login = async () => {
  const { data, error } = await supabase.auth.signInWithPassword({
    email: email.value,
    password: password.value,
  });
  console.log("data: ", data);
  console.log("error: ", error);
};

const logout = async () => {
  const { error } = await supabase.auth.signOut();
};

const { data, error } = await supabase.auth.getSession();
</script>

<template>
  <div class="container">
    <h4 style="font-size: 0.8rem; width: 90%">{{ data }}</h4>

    <h4 style="font-size: 0.8rem; width: 90%">
      {{ user }}
    </h4>

    <p class="register">
      Don't have an account?
      <NuxtLink to="/" class="registerspan">Register</NuxtLink>
    </p>
    <button @click="logout()">logout</button>
    <h2>
      Login to
      <span>Site</span>
    </h2>

    <input placeholder="mail" type="text" v-model="email" />
    <input placeholder="pass" type="text" v-model="password" />
    <button @click="login()">login</button>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  row-gap: 0.2rem;
  justify-content: center;
  align-items: center;
  height: 100vh;
  width: 100vw;
}
.register {
  font-size: 2rem;
}
.registerspan {
  color: purple;
  font-weight: 700;
  cursor: pointer;
}
</style>
