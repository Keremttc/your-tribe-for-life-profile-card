<script>
  export let data;
  const member = data.member;

  let message = member?.message || '';
  let sentMessage = '';

  function handleSubmit(event) {
    event.preventDefault();
    if (message.trim() === '') return;

    sentMessage = message;
    message = '';
    alert('Bericht verzonden! :)');
  }

  let buttonEl;

  function handleMouseMove(event) {
    const rect = buttonEl.getBoundingClientRect();
    const mouseX = event.clientX;
    const mouseY = event.clientY;

    const centerX = rect.left + rect.width / 2;
    const centerY = rect.top + rect.height / 2;

    const deltaX = (mouseX - centerX) / 1; 
    const deltaY = (mouseY - centerY) / 1;

    buttonEl.style.transform = `translate(${deltaX}px, ${deltaY}px)`;
  }

  function handleMouseLeave() {
    buttonEl.style.transform = `translate(0, 0)`;
  }
</script>

<div class="wrapper">
  <div class="card">
    <!-- Profile Card -->
    <div class="bio">
      <img src={member?.avatar} alt={member?.name} />
      <div class="details">
        <h1>{member?.name}</h1>
        <h2>{member?.bio}</h2> 
      </div>
    </div>

    <!-- Message Card -->
    <div class="box">
      <form on:submit={handleSubmit}>
        <textarea
          placeholder="Zeg eens gedag!"
          bind:value={message}
        ></textarea>
      </form>

      <div class="nav">
        <button 
          type="submit" 
          class="btn-cta" 
          bind:this={buttonEl} 
          on:click={handleSubmit}
          on:mousemove={handleMouseMove}
          on:mouseleave={handleMouseLeave}
        >
          Submit!
        </button>
      </div>

      {#if sentMessage}
        <p class="feedback">Je hebt verzonden: "{sentMessage}"</p>
      {/if}
    </div>
  </div>
</div>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600;700&display=swap');

* {
  font-family: "Montserrat", sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.wrapper {
  height: 100vh; 
  display: flex;
  align-items: center; 
  justify-content: center; 
  background: linear-gradient(to bottom, #a8edea, #fed6e3, #fbc2eb);
}

.card {
  z-index: 2;
  min-width: 350px;
  height: 265px;
  display: flex;
  flex-direction: column;
  background: #fff;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 0 7px rgba(0,0,0,0.3);
}

.bio {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px 10px;
}

.bio img {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  box-shadow: 0 0 5px rgba(0,0,0,1);
}

.details {
  margin-left: 20px;
  display: flex;
  flex-direction: column;
  flex: 1 0;
}

.details h1 { font-weight: 600; font-size: 1.3rem; }
.details h2 { font-weight: 500; font-size: 0.8rem; }

.box {
  width: 100%;
  height: 127px;
  background: #A52017;
  overflow: hidden;
}

textarea {
  width: 100%;
  height: 85px;
  padding: 10px;
  border-radius: 10px 10px 0 0;
  border: none;
  background: #A52017;
  font-size: 1rem;
  word-break: break-word;
  resize: none;
}

textarea:focus { outline: none; }

.nav {
  display: flex;
  justify-content: flex-end;
  padding: 5px 10px;
}

button {
  all: unset;
  width: 90px;
  text-align: center;
  cursor: pointer;
  background: #ffffff;  
  padding: 0 20px;
  border-radius: 10px;
  color: #000;
  font-weight: bold;
  letter-spacing: 5px;
  transition: transform 0.2s ease; /* Magnetisch smooth */
}

button::after {
  content: "";
  display: block;
  width: 0%;
  height: 2px;
  background: #fff;
  transition: width 0.5s ease-in-out;
}

button:hover::after { width: 100%; }

.feedback {
  margin-top: 10px;
  font-size: 0.9rem;
  color: green;
  text-align: center;
}
</style>
