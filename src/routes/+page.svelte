<script lang="ts">
  import Icon from "@iconify/svelte";
  import Notis from "./Notifications.svelte";
  import { bind } from "svelte/internal";
  let notification: any;

  const installNPM = "npm i svelte-notifications -D";

  let copied: boolean = false;
  const copyClipboard = async (text: string) => {
    navigator.clipboard
      .writeText(text)
      .then(() => {
        console.log("Text copied to clipboard successfully!");
        copied = true;
        setTimeout(() => {
          copied = false;
        }, 2000);
      })
      .catch((error) => {
        console.error("Error copying text to clipboard:", error);
      });
  };

  $: noti =
    option === obj.NORMAL ? "This is a notification" : "Error notification";
  let option: string = "normal";
  const obj = {
    NORMAL: "normal",
    ERROR: "error",
  };
  const sendNoti = async () => {
    if (option === obj.NORMAL) {
      notification.autoNormal(noti, 0);
    } else {
      notification.autoError(noti, 0);
    }
  };
</script>

<main class="main">
  <Notis bind:notification />
  <a class="gh" href="jdfaklj" target="_blank">
    <Icon icon="mdi:github" />
  </a>
  <div class="header box">
    <h1>Simple and minimialist <span class="color">Notifications</span></h1>
    <p>
      Super easy to use notification component for <span class="color">
        svelte !</span
      >
    </p>
  </div>
  <div class="installation box">
    <h1>Installation</h1>
    <p>You can install the component via npm:</p>
    <div class="npm">
      <p>npm i svelte-notifications</p>
      {#if copied === false}
        <button
          class="cpy"
          on:click={() => {
            copyClipboard(installNPM);
          }}><Icon icon="material-symbols:content-copy-outline" /></button
        >
      {:else}
        <div class="chek">
          <p>Copied !</p>
          <button><Icon icon="material-symbols:check-small" /></button>
        </div>
      {/if}
    </div>
    <p style="margin-top: 30px;">
      Or you can just copy the code into a component
      <a href="sdfas" class="linkto"
        ><Icon icon="material-symbols:add-link" /></a
      >
    </p>
  </div>
  <div class="usage box">
    <h1>Try out !</h1>
    <div class="try">
      <select bind:value={option} name="" id="">
        <option value={obj.NORMAL}>{obj.NORMAL}</option>
        <option value={obj.ERROR}>{obj.ERROR}</option>
      </select>
      <input
        maxlength="20"
        bind:value={noti}
        placeholder="Type a notification"
        type="text"
      />
      <button
        on:click={() => {
          sendNoti();
        }}>Push it !</button
      >
    </div>
  </div>
  <div style="height: 100vh;" />
</main>

<style>
  @import url("https://fonts.googleapis.com/css2?family=Roboto&display=swap");
  @import url("https://fonts.googleapis.com/css2?family=Inter:wght@900&display=swap");

  a {
    text-decoration: none;
    color: white;
    cursor: pointer;
  }
  p {
    color: rgb(202, 202, 202);
  }
  button {
    cursor: pointer;
    background-color: transparent;
    border: 1px solid rgb(126, 126, 126);
    border-radius: 3px;
    color: rgb(125, 125, 125);
    font-size: 1rem;
    transition: 0.2s ease;
  }
  button:hover {
    background-color: #222222;
    color: white;
    transition: 0.2s ease;
  }
  main {
    font-family: Inter, Roboto, serif;
    display: flex;
    align-items: center;
    flex-direction: column;
    position: absolute;
    width: 100%;
    top: 0;
    left: 0;
    background-color: #0a0a0a;
    color: white;
  }
  input {
    outline: none;
    background-color: transparent;
    border: 1px solid rgb(126, 126, 126);
    border-radius: 3px;
    color: rgb(126, 126, 126);
    font-size: 1.1rem;
    height: 50px;
    text-indent: 20px;
    color: white;
    transition: 0.2s ease;
  }
  input:hover {
    background-color: #222222;
    color: white;
    transition: 0.2s ease;
  }

  .linkto {
    margin-left: 14px;
    color: rgb(125, 125, 125);
    font-size: 1.3rem;
    position: absolute;
  }
  .try {
    font-family: Inter, Roboto;
    margin-top: 25px;
    display: flex;
    gap: 35px;
  }
  .try > button {
    width: 120px;
  }
  .try > input {
    width: 600px;
    color: rgb(126, 126, 126);
  }
  .try > input:hover {
    color: white;
  }
  .try > select {
    background-color: transparent;
    color: rgb(125, 125, 125);
    border: 1px solid grey;
    border-radius: 3px;
    height: 53px;
    margin-top: 0.1px;
    width: 100px;
    text-indent: 10px;
    outline: none;
    font-size: 1rem;
    text-decoration: none;
    text-transform: capitalize;
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: 0.2s ease;
    cursor: pointer;
  }
  .try > select:hover {
    color: white;
    transition: 0.2s ease;
    background-color: #222222;
  }

  .try > select > option {
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
    background-color: transparent;
    outline: none;
  }
  .linkto {
    color: white;
  }
  .npm {
    border: 1px solid rgb(125, 125, 125);
    border-radius: 6px;
    margin-top: 10px;
  }
  .npm > p {
    margin-left: 20px;
  }
  .cpy {
    position: absolute;
    margin-top: -39px;
    background-color: transparent;
    border: none;
    color: rgb(126, 126, 126);
    font-size: 1.5rem;
    margin-left: 850px;
    transition: 0.4s;
  }
  .chek {
    display: flex;
    position: absolute;
    margin-top: -55px;
    margin-left: 780px;
  }
  .chek > button {
    border: none;
    font-size: 2rem;
    margin-top: 10px;
  }
  .npm button:hover {
    background-color: transparent;
  }
  .npm > button:hover {
    color: white;
    transition: 0.4s;
  }
  .box {
    margin-top: 50px;
    display: flex;
    flex-direction: column;
    width: 900px;
  }

  .gh {
    font-size: 2rem;
    position: fixed;
    top: 10px;
    right: 10px;
    transition: 0.4s;
  }
  .gh:hover {
    color: #e21143;
    transition: 0.4s;
  }
  .header {
    text-align: center;
    font-size: 1.8rem;
    font-family: Inter, serif;
    margin-top: 150px;
    width: 900px;
    border: none;
    border-bottom: 1px solid gray;
  }
  .header > p {
    font-family: Roboto, serif;
    font-size: 1.1rem;
    margin-bottom: 80px;
  }
  .color {
    font-weight: bold;
    background-image: linear-gradient(60deg, #e21143, #ffb03a);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }
</style>
