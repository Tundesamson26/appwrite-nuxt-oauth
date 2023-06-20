<template>
  <section class="container">
    <div>
      <h2 class="u-text-center u-font-size-32 u-margin-32">
        Amazon Authentication with Appwrite
      </h2>
      <div
        class="card u-text-center u-cross-center u-width-full-line u-max-width-350"
        style="margin: auto"
      >
        <div class="">
          <h3 class="body-text-2 u-margin-block-start-16 u-bold">
            Name:
          </h3>
          <p class="">{{name}}</p>
          <h3 class="u-margin-block-start-4 u-color-text-gray u-bold">
            Email:
          </h3>
          <p>{{email}}</p>
        </div>
        <button class="button u-margin-inline-auto u-margin-block-start-24" @click="logOutWithGithub">
          <span class="text">Logout</span>
        </button>
      </div>
    </div>
  </section>
</template>
<script setup>
import { ref, onMounted } from "vue";
import { useRouter } from 'vue-router';
import { Client, Account } from "appwrite";
import "@appwrite.io/pink"; // optionally, add icons
import "@appwrite.io/pink-icons";

const client = new Client();
const account = new Account(client);

client
  .setEndpoint("https://cloud.appwrite.io/v1")
  .setProject("648b874f54b5092cdf00");

const name = ref("");
const email = ref("");
const response = ref("");

const $router = useRouter();

onMounted(async () => {
  await getUserSession();
});

const getUserSession = async () => {
  try {
    response.value = await account.get();
    if (response.value) {
      name.value = response.value.name;
      email.value = response.value.email;
    }
  } catch (error) {
    console.log(error);
  }
};

const logOutWithGithub = async () => {
  try {
    await account.deleteSession('current');
    $router.push('/');
  } catch (error) {
    console.log(error);
  }
};
</script>
