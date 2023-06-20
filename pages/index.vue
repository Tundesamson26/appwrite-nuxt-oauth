<template>
  <h2 class="u-text-center u-font-size-32 u-margin-32">Login with Amazon</h2>
  <div class="card u-text-center u-max-width-400" style="margin: auto">
    <div class="u-text-center">
      <p>Click on this button to login</p>
      <button
        class="button u-margin-inline-auto u-margin-block-start-24"
        @click="loginWithAmazon"
      >
        <span class="text">Login with Amazon</span>
      </button>
    </div>
  </div>
</template>
<script setup>
import { Client, Account } from "appwrite";
import "@appwrite.io/pink";
import "@appwrite.io/pink-icons";

const client = new Client();
const account = new Account(client);

client
  .setEndpoint("https://cloud.appwrite.io/v1")
  .setProject("648b874f54b5092cdf00");

const loginWithAmazon = async () => {
  try {
    await account.createOAuth2Session(
      "amazon",
      "http://localhost:3000/dashboard"
    );
  } catch (e) {
    alert("user does not exist");
    console.log(e);
  }
};
</script>
