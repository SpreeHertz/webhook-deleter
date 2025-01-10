<template>
	<div class="webhook-deleter">
		<div class="card">
			<h1 class="title">Discord Webhook Deleter</h1>

			<div class="input-group">
				<label for="webhook-url">Enter Webhook URL:</label>
				<input
					id="webhook-url"
					v-model="webhookUrl"
					type="text"
					placeholder="discord.com/api/webhooks/..."
				>
			</div>

			<button @click="deleteWebhook" class="delete-btn" :disabled="isDeleting">
				<Trash2Icon v-if="!isDeleting" class="icon" />
				<LoaderIcon v-else class="icon animate-spin" />
				{{ isDeleting ? 'Deleting...' : 'Delete Webhook' }}
			</button>

			<TransitionGroup name="fade">
				<div v-if="status === 'success'" key="success" class="alert success" role="alert">
					<CheckCircleIcon class="icon" />
					<div>
						<strong>Success!</strong> The webhook has been successfully deleted.
					</div>
					<button @click="resetStatus" class="close-btn" aria-label="Close">
						<XIcon class="icon" />
					</button>
				</div>

				<div v-if="status === 'error'" key="error" class="alert error" role="alert">
					<AlertCircleIcon class="icon" />
					<div>
						<strong>Error:</strong> {{ errorMessage }}
					</div>
					<button @click="resetStatus" class="close-btn" aria-label="Close">
						<XIcon class="icon" />
					</button>
				</div>
			</TransitionGroup>

			<footer class="footer">
				<p>Made with ❤️ by spreehertz
				</p>
				<p class="contributor">Contributor:<a class="contributor_link" href="https://github.com/Fedox-die-Ente">Fedox-die-Ente</a></p>
				<a href="https://github.com/spreehertz/webhook-deleter" target="_blank" rel="noopener noreferrer">
					<GithubIcon class="icon" />
				</a>
			</footer>
		</div>
	</div>
</template>

<script setup>
import { ref } from 'vue'
import { Trash2Icon, LoaderIcon, CheckCircleIcon, AlertCircleIcon, XIcon, HeartIcon, GithubIcon } from 'lucide-vue-next'

const webhookUrl = ref('')
const status = ref('idle')
const errorMessage = ref('')
const isDeleting = ref(false)

const deleteWebhook = async () => {
	if (!webhookUrl.value) {
		status.value = 'error'
		errorMessage.value = 'Please enter a webhook URL.'
		return
	}
	const expression = "^https://discord\.com/api/.*"
	const regex = new RegExp(expression);
	if (!webhookUrl.value.match(regex)) {
		status.value = 'error'
		errorMessage.value = 'This is not a Discord webhook URL. Note: The webhook token is required.'
		return
	}
	isDeleting.value = true
	try {
		const response = await fetch(webhookUrl.value, { method: 'DELETE'})
		console.log(response)
		if (response.status == 404) throw new Error("This webhook does not exist (maybe you've already deleted it).")
		if (!response.ok) throw new Error(`Failed to delete webhook.`)
		
		status.value = 'success'
		webhookUrl.value = ''
	} catch (error) {
		status.value = 'error'
		errorMessage.value = error instanceof Error ? error.message : 'An unknown error occurred'
	} finally {
		isDeleting.value = false
	}
}

const resetStatus = () => {
	status.value = 'idle'
	errorMessage.value = ''
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap');

.webhook-deleter {
	min-height: 100vh;
	display: flex;
	justify-content: center;
	align-items: center;
	background: linear-gradient(135deg, #f9a8d4, #d8b4fe, #818cf8);
	font-family: 'Inter', sans-serif;
	overflow-y: hidden;
}

.card {
	background: white;
	border-radius: 1rem;
	padding: 2rem;
	width: 100%;
	max-width: 400px;
	box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
}

.title {
	font-size: 1.5rem;
	font-weight: 700;
	text-align: center;
	margin-bottom: 1.5rem;
	color: #4b5563;
}

.input-group {
	display: flex;
	flex-direction: column;
	gap: 1rem;
	margin-bottom: 1rem;
}


label {
	display: block;
	margin-bottom: 0.5rem;
	font-weight: 600;
	color: #4b5563;
}

input,
.delete-btn {
	width: 100%;
	padding: 0.75rem;
	box-sizing: border-box;
	font-family: 'Inter', sans-serif;
}



input:focus {
	outline: none;
	border-color: #818cf8;
	box-shadow: 0 0 0 3px rgba(129, 140, 248, 0.2);
	font-family: 'Inter', sans-serif;
}

.delete-btn {
	background-color: #ef4444;
	color: white;
	border: none;
	border-radius: 0.5rem;
	font-size: 1rem;
	font-weight: 600;
	cursor: pointer;
	display: flex;
	align-items: center;
	justify-content: center;
	transition: background-color 0.2s;
}

.delete-btn:hover:not(:disabled) {
	background-color: #dc2626;
}

.delete-btn:disabled {
	opacity: 0.7;
	cursor: not-allowed;
}

.alert {
	margin-top: 1rem;
	padding: 1rem;
	border-radius: 0.5rem;
	display: flex;
	align-items: flex-start;
}

.success {
	background-color: #d1fae5;
	color: #065f46;
}

.error {
	background-color: #fee2e2;
	color: #991b1b;
}

.close-btn {
	background: none;
	border: none;
	cursor: pointer;
	padding: 0;
	color: currentColor;
	margin-left: auto;
}

.footer {
	margin-top: 2rem;
	text-align: center;
	font-size: 0.875rem;
	color: #6b7280;
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
}

.contributor {
	margin-top: -0.5rem;
}

.contributor_link:hover {
	color: #303339;
}

.footer a {
	color: #6b7280;
	margin-left: 0.5rem;
}

.icon {
	width: 1.25rem;
	height: 1.25rem;
	margin-right: 0.5rem;
}

@media (max-width: 640px) {
	.card {
		padding: 1.5rem;
	}
}

@keyframes spin {
	to {
		transform: rotate(360deg);
	}
}

.animate-spin {
	animation: spin 1s linear infinite;
}

#webhook-url {
	font-family: 'Inter', sans-serif;
}
</style>