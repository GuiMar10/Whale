<script>
  import { GoogleGenerativeAI } from "@google/generative-ai";
  import "@material/web/progress/linear-progress";
  var aiResponse;
  var awsered;
  var chatHist = [];
  var loading = false;

  // Fetch your API_KEY
  const API_KEY = "AIzaSyD3ZBSwbEXjI6G8yOSN6nzvbeBZp6d6UBI";

  // Access your API key (see "Set up your API key" above)
  const genAI = new GoogleGenerativeAI(API_KEY);
  // For text-only input, use the gemini-pro model
  const model = genAI.getGenerativeModel({ model: "gemini-pro" });
  const chat = model.startChat({});
  async function search() {
    const prompt = document.getElementById("prompt").value;
    document.getElementById("prompt").value = "";
    if (prompt !== "") {
      loading = true;
      const result = await chat.sendMessage(prompt);
      aiResponse = result.response.text();
      awsered = true;
      loading = false;
      chatHist = chat._history;
    }
  }
  function promptKeyUp(e) {
    if (e.keyCode == 13) {
      search();
    }
  }
</script>

<div id="searcharea" class="content">
  {#if !awsered}
    <h1>Olá, humano.</h1>
    <h2>Posso ajudar?</h2>
  {/if}
  {#each chatHist as hist}
    {#if hist.role == "user"}
      <h1 class="prompttitle">{hist.parts[0].text}</h1>
    {:else}
      <h4 class="responselabel"><span>neurology</span>Resposta</h4>
      <div class="response">{hist.parts[0].text}</div>
      <hr />
    {/if}
  {/each}
</div>
<div id="searcharea" class={awsered ? "aiwelcomed" : "aiwelcome"}>
  <textarea
    on:keyup={promptKeyUp}
    id="prompt"
    type="text"
    placeholder={awsered ? "Pergunta do milênio..." : "Pergunta do século..."}
    autofocus
  />
  <button on:click={search}>search</button>
  {#if loading}
    <md-linear-progress
      style="position: absolute; border-radius: 100px; margin-top: 10px; width: 600px;"
      indeterminate
    ></md-linear-progress>
  {/if}
</div>

<style lang="scss">
  @import url("https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap");
  @import url("https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@24,400,0,0");
  @import url("https://fonts.googleapis.com/css2?family=Open+Sans:ital,wght@0,300..800;1,300..800&display=swap");
  :root {
    /* light */
    --md-sys-color-primary-light: #984717;
    --md-sys-color-on-primary-light: #ffffff;
    --md-sys-color-primary-container-light: #ffdbcb;
    --md-sys-color-on-primary-container-light: #341100;
    --md-sys-color-secondary-light: #765849;
    --md-sys-color-on-secondary-light: #ffffff;
    --md-sys-color-secondary-container-light: #ffdbcb;
    --md-sys-color-on-secondary-container-light: #2c160b;
    --md-sys-color-tertiary-light: #655f31;
    --md-sys-color-on-tertiary-light: #ffffff;
    --md-sys-color-tertiary-container-light: #ece4aa;
    --md-sys-color-on-tertiary-container-light: #1f1c00;
    --md-sys-color-error-light: #ba1a1a;
    --md-sys-color-error-container-light: #ffdad6;
    --md-sys-color-on-error-light: #ffffff;
    --md-sys-color-on-error-container-light: #410002;
    --md-sys-color-background-light: #fffbff;
    --md-sys-color-on-background-light: #201a18;
    --md-sys-color-surface-light: #fffbff;
    --md-sys-color-on-surface-light: #201a18;
    --md-sys-color-surface-variant-light: #f4ded5;
    --md-sys-color-on-surface-variant-light: #52443d;
    --md-sys-color-outline-light: #85736c;
    --md-sys-color-inverse-on-surface-light: #fbeee9;
    --md-sys-color-inverse-surface-light: #362f2c;
    --md-sys-color-inverse-primary-light: #ffb692;
    --md-sys-color-shadow-light: #000000;
    --md-sys-color-surface-tint-light: #984717;
    --md-sys-color-outline-variant-light: #ddc0b452;
    --md-sys-color-scrim-light: #000000;
    /* dark */
    --md-sys-color-primary-dark: #ffb692;
    --md-sys-color-on-primary-dark: #562000;
    --md-sys-color-primary-container-dark: #793000;
    --md-sys-color-on-primary-container-dark: #ffdbcb;
    --md-sys-color-secondary-dark: #e6beac;
    --md-sys-color-on-secondary-dark: #432a1e;
    --md-sys-color-secondary-container-dark: #5c4033;
    --md-sys-color-on-secondary-container-dark: #ffdbcb;
    --md-sys-color-tertiary-dark: #d0c890;
    --md-sys-color-on-tertiary-dark: #353107;
    --md-sys-color-tertiary-container-dark: #4c481c;
    --md-sys-color-on-tertiary-container-dark: #ece4aa;
    --md-sys-color-error-dark: #ffb4ab;
    --md-sys-color-error-container-dark: #93000a;
    --md-sys-color-on-error-dark: #690005;
    --md-sys-color-on-error-container-dark: #ffdad6;
    --md-sys-color-background-dark: #201a18;
    --md-sys-color-on-background-dark: #ede0db;
    --md-sys-color-surface-dark: #201a18;
    --md-sys-color-on-surface-dark: #ede0db;
    --md-sys-color-surface-variant-dark: #52443d;
    --md-sys-color-on-surface-variant-dark: #d7c2b9;
    --md-sys-color-outline-dark: #a08d85;
    --md-sys-color-inverse-on-surface-dark: #201a18;
    --md-sys-color-inverse-surface-dark: #ede0db;
    --md-sys-color-inverse-primary-dark: #984717;
    --md-sys-color-shadow-dark: #000000;
    --md-sys-color-surface-tint-dark: #ffb692;
    --md-sys-color-outline-variant-dark: #52443d;
    --md-sys-color-scrim-dark: #000000;

    --md-sys-color-primary: var(--md-sys-color-primary-light);
    --md-sys-color-on-primary: var(--md-sys-color-on-primary-light);
    --md-sys-color-primary-container: var(
      --md-sys-color-primary-container-light
    );
    --md-sys-color-on-primary-container: var(
      --md-sys-color-on-primary-container-light
    );
    --md-sys-color-secondary: var(--md-sys-color-secondary-light);
    --md-sys-color-on-secondary: var(--md-sys-color-on-secondary-light);
    --md-sys-color-secondary-container: var(
      --md-sys-color-secondary-container-light
    );
    --md-sys-color-on-secondary-container: var(
      --md-sys-color-on-secondary-container-light
    );
    --md-sys-color-tertiary: var(--md-sys-color-tertiary-light);
    --md-sys-color-on-tertiary: var(--md-sys-color-on-tertiary-light);
    --md-sys-color-tertiary-container: var(
      --md-sys-color-tertiary-container-light
    );
    --md-sys-color-on-tertiary-container: var(
      --md-sys-color-on-tertiary-container-light
    );
    --md-sys-color-error: var(--md-sys-color-error-light);
    --md-sys-color-error-container: var(--md-sys-color-error-container-light);
    --md-sys-color-on-error: var(--md-sys-color-on-error-light);
    --md-sys-color-on-error-container: var(
      --md-sys-color-on-error-container-light
    );
    --md-sys-color-background: var(--md-sys-color-background-light);
    --md-sys-color-on-background: var(--md-sys-color-on-background-light);
    --md-sys-color-surface: var(--md-sys-color-surface-light);
    --md-sys-color-on-surface: var(--md-sys-color-on-surface-light);
    --md-sys-color-surface-variant: var(--md-sys-color-surface-variant-light);
    --md-sys-color-on-surface-variant: var(
      --md-sys-color-on-surface-variant-light
    );
    --md-sys-color-outline: var(--md-sys-color-outline-light);
    --md-sys-color-inverse-on-surface: var(
      --md-sys-color-inverse-on-surface-light
    );
    --md-sys-color-inverse-surface: var(--md-sys-color-inverse-surface-light);
    --md-sys-color-inverse-primary: var(--md-sys-color-inverse-primary-light);
    --md-sys-color-shadow: var(--md-sys-color-shadow-light);
    --md-sys-color-surface-tint: var(--md-sys-color-surface-tint-light);
    --md-sys-color-outline-variant: var(--md-sys-color-outline-variant-light);
    --md-sys-color-scrim: var(--md-sys-color-scrim-light);

    background: var(--md-sys-color-background);
    font-family: Roboto;
  }
  h1.prompttitle {
    margin-bottom: 10px;
    font-weight: 400;
  }
  h4.responselabel {
    color: var(--md-sys-color-on-background);
    margin-bottom: 10px;
    animation: titleswelcome 0.5s;
    font-family: Open Sans;
    font-weight: 600;
    & span {
      font-family: Material Symbols Outlined;
      font-weight: 300;
      margin-right: 5px;
    }
  }
  hr {
    background-color: var(--md-sys-color-on-background);
    opacity: 0.2;
    margin-bottom: 20px;
    height: 1px;
    border: 0;
  }
  textarea {
    resize: none;
    border: 0;
    font-family: Roboto;
    padding-top: 18px;
    padding-left: 20px;
    width: calc(100% - 30px);
    height: 32px;
    font-size: 14px;
    border-radius: 100px;
    color: var(--md-sys-color-on-background);
    background: var(--md-sys-color-outline-variant);
    transition: border 0.5s;
    &:focus {
      outline: none;
    }
    &::placeholder {
      color: var(--md-sys-color-secondary);
      opacity: 0.5;
    }
    &.welcomed {
      position: fixed;
      bottom: 0px;
    }
  }
  div.response {
    margin-bottom: 15px;
    color: var(--md-sys-color-on-secondary-container);
    animation: msgwelcome 0.4s;
    width: 600px;
  }
  h1 {
    color: var(--md-sys-color-on-background);
    margin: 0;
    animation: titleswelcome 0.5s;
    font-family: Open Sans;
    font-weight: 600;
  }
  h2 {
    color: var(--md-sys-color-outline);
    margin: 0;
    margin-bottom: 30px;
    animation: titleswelcome 1s;
    font-family: Open Sans;
    font-weight: 500;
  }
  button {
    font-family: Material Symbols Outlined;
    height: 40px;
    border-radius: 100px;
    padding: 0px 15px;
    border: 0;
    background: var(--md-sys-color-primary);
    cursor: pointer;
    color: var(--md-sys-color-on-primary);
    position: absolute;
    transform: translateX(-50px) translateY(6px);
    transition: 0.1s;
    &:active {
      scale: 0.95;
    }
  }
  div#searcharea {
    &.content {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      margin-bottom: 2000px;
      width: 600px;
    }
    &.aiwelcome {
      position: absolute;
      top: 50%;
      left: 50%;
      width: 600px;
      transform: translate(-50%, -50%);
      margin-top: 70px;
    }
    &.aiwelcomed {
      position: fixed;
      left: 50%;
      width: 600px;
      transform: translate(-50%, -50%);
      bottom: 20px;
    }
  }
  @keyframes msgwelcome {
    from {
      transform: translateX(-10px);
      opacity: 0;
    }
  }
  @keyframes titleswelcome {
    from {
      transform: translateX(-5px);
      opacity: 0;
    }
  }
  @media screen and (prefers-color-scheme: dark) {
    :root {
      --md-sys-color-primary: var(--md-sys-color-primary-dark);
      --md-sys-color-on-primary: var(--md-sys-color-on-primary-dark);
      --md-sys-color-primary-container: var(
        --md-sys-color-primary-container-dark
      );
      --md-sys-color-on-primary-container: var(
        --md-sys-color-on-primary-container-dark
      );
      --md-sys-color-secondary: var(--md-sys-color-secondary-dark);
      --md-sys-color-on-secondary: var(--md-sys-color-on-secondary-dark);
      --md-sys-color-secondary-container: var(
        --md-sys-color-secondary-container-dark
      );
      --md-sys-color-on-secondary-container: var(
        --md-sys-color-on-secondary-container-dark
      );
      --md-sys-color-tertiary: var(--md-sys-color-tertiary-dark);
      --md-sys-color-on-tertiary: var(--md-sys-color-on-tertiary-dark);
      --md-sys-color-tertiary-container: var(
        --md-sys-color-tertiary-container-dark
      );
      --md-sys-color-on-tertiary-container: var(
        --md-sys-color-on-tertiary-container-dark
      );
      --md-sys-color-error: var(--md-sys-color-error-dark);
      --md-sys-color-error-container: var(--md-sys-color-error-container-dark);
      --md-sys-color-on-error: var(--md-sys-color-on-error-dark);
      --md-sys-color-on-error-container: var(
        --md-sys-color-on-error-container-dark
      );
      --md-sys-color-background: var(--md-sys-color-background-dark);
      --md-sys-color-on-background: var(--md-sys-color-on-background-dark);
      --md-sys-color-surface: var(--md-sys-color-surface-dark);
      --md-sys-color-on-surface: var(--md-sys-color-on-surface-dark);
      --md-sys-color-surface-variant: var(--md-sys-color-surface-variant-dark);
      --md-sys-color-on-surface-variant: var(
        --md-sys-color-on-surface-variant-dark
      );
      --md-sys-color-outline: var(--md-sys-color-outline-dark);
      --md-sys-color-inverse-on-surface: var(
        --md-sys-color-inverse-on-surface-dark
      );
      --md-sys-color-inverse-surface: var(--md-sys-color-inverse-surface-dark);
      --md-sys-color-inverse-primary: var(--md-sys-color-inverse-primary-dark);
      --md-sys-color-shadow: var(--md-sys-color-shadow-dark);
      --md-sys-color-surface-tint: var(--md-sys-color-surface-tint-dark);
      --md-sys-color-outline-variant: var(--md-sys-color-outline-variant-dark);
      --md-sys-color-scrim: var(--md-sys-color-scrim-dark);
    }
  }
</style>
