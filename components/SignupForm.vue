<script setup>
const userName = ref("");
const email = ref("");
const password = ref("");

const supabase = useSupabaseClient();
const user = useSupabaseUser();

const signUp = async () => {
  const { data, error } = await supabase.auth.signUp({
    email: email.value,
    password: password.value,
    options: {
      data: {
        user_name: userName.value,
      },
    },
  });
  console.log("data: ", data);
  console.log("error: ", error);
};
const logout = async () => {
  const { error } = await supabase.auth.signOut();
};
</script>

<template>
  <div class="container">
    <h2 style="font-size: 0.8rem; width: 90%" if="user">{{ user }}</h2>
    <p class="login">
      Already have an account?
      <NuxtLink to="/login" class="loginspan">Login</NuxtLink>
    </p>
    <button @click="logout()">logout</button>
    <h2>
      Create Your <br />
      <span>Site</span> Account
    </h2>

    <input placeholder="username" type="text" v-model="userName" />
    <input placeholder="mail" type="text" v-model="email" />
    <input placeholder="pass" type="text" v-model="password" />
    <button @click="signUp()">signup</button>
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
.login {
  font-size: 2rem;
}
.loginspan {
  color: purple;
  font-weight: 700;
  cursor: pointer;
}
</style>
