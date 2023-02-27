
<template>
   <div class="first">
        <h1 class="webhook-deleter">discord webhook deleter</h1>
    </div>
        <label for="webhook-url" class="webhook-url-label">enter webhook url</label>
        <div class="webhook-input">
            <input type="text" v-model="text" class="webhook-url-input-box" id="webhook-url" placeholder="discord.com/api/webhooks/...">
        </div>
       <div class="delete">
        <button class="delete-btn" id="delete-btn">Delete</button>
       </div>
</template>

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

</style>
