<script lang="ts">
  interface Notificacion {
    text: string;
    type: string;
  }
  let notificaciones: Array<Notificacion> = [];
  let index: number = 0;

  const themes: object = {
    light: "light",
    dark: "dark",
  };

  let theme = "dark";

  export const notification = {
    autoNormal: async (text: string, time: number, theme: string) => {
      //notificaciones[index] = { text: text, type: "normal" };
      notificaciones = [...notificaciones, { text, type: "normal" }];
      if (time <= 2000 || time === undefined) {
        time = 4000;
      }
      let i: number = index;
      index++;
      console.log(notificaciones);
      setTimeout(() => {
        notificaciones = notificaciones.filter((n, i) => i !== 0);
        //delete notificaciones[i];
        console.log("Con delete" + notificaciones[i]);
      }, time);
    },

    autoError: async (text: string, time: number) => {
      notificaciones = [...notificaciones, { text, type: "error" }];
      if (time <= 2000 || time === undefined) {
        time = 4000;
      }
      let i: number = index;
      index++;
      setTimeout(() => {
        notificaciones = notificaciones.filter((n, i) => i !== 0);
      }, time);
    },

    autoOption: async (text: string, time: number) => {},
    closeNormal: async (text: string, time: number) => {
      notificaciones = [...notificaciones, { text, type: "closeNormal" }];
      if (time <= 2000 || time === undefined) {
        time = 4000;
      }
      let i: number = index;
      index++;
      //Hay que pensar
    },
  };
</script>

<main>
  <ul class="notis">
    {#each notificaciones as noti, ind}
      {#if noti.type === "normal"}
        {#if theme === "dark"}
          <div id={ind.toString()} class="n">
            <p class="light">{noti.text}</p>
          </div>
        {/if}
      {:else if noti.type === "error"}
        <div id={ind.toString()} class="n red">
          <p>{noti.text}</p>
        </div>
      {:else if noti.type === "opcion"}
        <div id={ind.toString()} class="n">
          <p>{noti.text}</p>
          <div class="opc">
            <button>Accept</button>
            <button>Cancel</button>
          </div>
        </div>
      {/if}
    {/each}
  </ul>
</main>

<style>
  @import url("https://fonts.googleapis.com/css2?family=Inter&display=swap");
  .notis {
    position: fixed;
    bottom: 0;
    right: 20px;
    width: 350px;
    height: auto;
    display: flex;
    flex-direction: column-reverse;
  }
  .opc {
    display: flex;
    flex-direction: column;
  }
  .light {
    color: white;
  }
  .n {
    font-family: Inter, sans-serif;
    position: relative;
    width: 350px;
    height: 100px, auto;
    align-items: center;
    display: flex;
    flex-direction: row;
    border-radius: 5px;
    box-shadow: rgba(66, 66, 66, 0.35) 0px 5px 15px;
    transition: 0.4s ease-in;
    margin-top: 20px;
    animation-name: salir;
    animation-duration: 1s;
    animation-iteration-count: 1;
    transition: opacity 0.5s ease-out;
    word-break: break-all;
  }
  .n > :nth-child(1) {
    font-weight: bold;
    margin-top: 20px;
    margin-left: 20px;
  }
  .n > :nth-child(2) {
    position: relative;
    margin-left: 40px;
    margin-top: -5px;
    margin-right: 5px;
  }
  .red {
    background-color: red;
  }
  @keyframes salir {
    from {
      right: -350px;
    }
    to {
      right: 0;
    }
  }
</style>
