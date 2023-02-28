<template>
   <div class="first">
        <h1 class="webhook-deleter">discord webhook deleter</h1>
    </div>
        <label for="webhook-url" class="webhook-url-label">enter webhook url</label>
        <div class="webhook-input">
			<input type="text"  @input="handleInput" v-model="webhookurl" class="webhook-url-input-box" id="webhook-url" placeholder="discord.com/api/webhooks/...">
        </div>
		
       <div class="delete">
        <button @click="deleteWebhook" class="delete-btn" id="delete-btn">Delete</button>
       </div>
	   <div class="success-container hidden" role="alert">
  	<svg aria-hidden="true" class="success-svg" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7-4a1 1 0 11-2 0 1 1 0 012 0zM9 9a1 1 0 000 2v3a1 1 0 001 1h1a1 1 0 100-2v-3a1 1 0 00-1-1H9z" clip-rule="evenodd"></path></svg>
  <div>
    <span class="font-medium">Success!</span> The webhook has been successfully deleted.
  </div>
</div>
</template>

<script>
import axios from 'axios';

export default {
	name: "App",
	data() {
		return {
			webhookurl: ''
		}
	},
	methods: {
  deleteWebhook() {
    axios.delete(this.webhookurl)
      .then(() => {
        // show success message
        this.showSuccessMessage();
      })
      .catch((error) => {
        console.error(error);
      });
  },
  showSuccessMessage() {
    // show the success message by removing the "hidden" class from the success container
    const successContainer = document.querySelector('.success-container');
    successContainer.classList.remove('hidden');
  },
  handleInput(event) {
    // update the webhookurl data property with the input value
    this.webhookurl = event.target.value;
  }
}

}

</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap');

* {
    font-family: 'Inter';
}

body {
	background: linear-gradient(to right, rgb(59, 130, 246), rgb(37, 99, 235));
	background-size: 400% 400%;
	animation: gradient 15s ease infinite;
	height: 100vh;
}

@keyframes gradient {
	0% {
		background-position: 0% 50%;
	}
	50% {
		background-position: 100% 50%;
	}
	100% {
		background-position: 0% 50%;
	}
}


.webhook-deleter {
    font-family: 'Inter', sans-serif;
    text-align: center;
    padding-top: 10em;
}

.webhook-url-label {
	display: block;
    align-items: center;
	text-align: center;
}

/* parent div */
.webhook-input {
	display: grid;
	align-items: center;
	place-content: center;
	place-items: center;
	margin: 0 auto;
	margin-top: 8px;
	
}

.webhook-url-input-box {
	display: grid;
	padding: 10px;
	margin-top: 4px;
	width: 200%;
	text-align: center;
	align-items: center;
	border-radius: 0.5rem; /* 8px */
	background: rgb(116, 164, 246);
	border: 1px solid transparent;
}

.delete {
	display: grid;
	place-items: center;
	margin-top: 24px;
}

.delete-btn {
	padding: 10px;
	padding-left: 15px;
	padding-right: 15px;
	background: rgb(237, 66, 69);
	border: 1px solid transparent;
	color: white;
	font-family: 'Inter', sans-serif;
	font-weight: 600;
	border-radius: 0.5rem;
	box-sizing: border-box;
	cursor: pointer;
}
.success-container {
	display: flex;
	padding: 1rem;
	color: #166534;
	border-radius: 0.5rem;
	background-color: #bbf7d0;
	width: 25%;
}

.success-svg {
	display: inline;
	flex-shrink: 0;
	width: 1.25rem;
	height: 0.75rem;
	margin-right: 0.75rem;
}

.font-medium {
	font-weight: 700;
}

.hidden {
	display: none;
}
</style>
