<template>
  <div class="section-content terminal-section">
    <h2>Connect with Me</h2>
    
    <div class="terminal-casing">
      <div class="terminal-header">
        <div class="window-controls">
          <span class="dot close"></span>
          <span class="dot minimize"></span>
          <span class="dot maximize"></span>
        </div>
        <span class="terminal-title">contact_terminal.exe</span>
      </div>

      <form class="terminal-body" @submit.prevent="executeUplink">
        <div class="input-group">
          <label for="name"><span class="prompt">guest@aaron:~$</span> Enter Name</label>
          <input type="text" id="name" v-model="formData.name" required autocomplete="off" placeholder="John Doe" />
        </div>

        <div class="input-group">
          <label for="email"><span class="prompt">guest@aaron:~$</span> Enter Email</label>
          <input type="email" id="email" v-model="formData.email" required autocomplete="off" placeholder="john.doe@example.com" />
        </div>

        <div class="input-group">
          <label for="message"><span class="prompt">guest@aaron:~$</span> Write Message</label>
          <textarea id="message" v-model="formData.message" rows="5" required placeholder="Your message here..."></textarea>
        </div>

        <button type="submit" class="transmit-btn" :disabled="isTransmitting">
          {{ isTransmitting ? 'TRANSMITTING_DATA...' : 'SUBMIT' }}
        </button>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const formData = ref({
  name: '',
  email: '',
  message: ''
})

const isTransmitting = ref(false)

const executeUplink = async () => {
  isTransmitting.value = true
  
  try {
    // Transmits the payload to the serverless email API
    const response = await fetch('https://api.web3forms.com/submit', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'Accept': 'application/json'
      },
      body: JSON.stringify({
        access_key: 'e9f2740d-c8b0-4486-8a32-5d8f99aab501',
        // Maps your form data to the email output
        name: formData.value.name,
        email: formData.value.email,
        message: formData.value.message,
        
        // Customizes the subject line in your inbox
        subject: 'SYSTEM ALERT: New Uplink from VIP Portfolio'
      })
    })

    const result = await response.json()

    if (result.success) {
      alert(`UPLINK SUCCESSFUL. \nData received from: ${formData.value.name}\nI will review your directive shortly.`)
      // Clear the terminal upon successful transmission
      formData.value = { name: '', email: '', message: '' }
    } else {
      alert('UPLINK FAILED. Server rejected the payload.')
      console.error(result)
    }
    
  } catch (error) {
    alert('CRITICAL ERROR. Network connection severed.')
    console.error('Terminal Error:', error)
  } finally {
    isTransmitting.value = false
  }
}
</script>

<style scoped>
.terminal-section {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
}

.terminal-section h2 { 
  color: var(--color-accent); 
  font-family: 'Montserrat', sans-serif;
  letter-spacing: 2px;
  text-transform: uppercase;
  margin-bottom: 40px;
}

/* The Dark Glass Terminal Casing */
.terminal-casing {
  background: rgba(10, 10, 10, 0.85); /* Deepest dark glass */
  width: 100%;
  max-width: 700px; /* Constrains it to a highly readable width */
  border-radius: 12px;
  border: 1px solid rgba(40, 194, 194, 0.2); /* Faint turquoise rim */
  box-shadow: 
    0 25px 50px rgba(0, 0, 0, 0.8),
    0 0 30px rgba(40, 194, 194, 0.05);
  overflow: hidden;
}

/* Terminal Header Bar */
.terminal-header {
  background: #1a1a1a;
  padding: 12px 20px;
  display: flex;
  align-items: center;
  border-bottom: 1px solid #333;
  position: relative;
}

.window-controls {
  display: flex;
  gap: 8px;
}

.dot {
  width: 12px;
  height: 12px;
  border-radius: 50%;
}

.close { background-color: #ff5f56; }
.minimize { background-color: #ffbd2e; }
.maximize { background-color: #27c93f; }

.terminal-title {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  color: #666;
  font-family: 'Courier New', Courier, monospace;
  font-size: 0.85rem;
  letter-spacing: 1px;
}

/* Terminal Body & Inputs */
.terminal-body {
  padding: 40px;
  display: flex;
  flex-direction: column;
  gap: 30px;
}

.input-group {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

label {
  font-family: 'Courier New', Courier, monospace;
  color: #B0B0B0;
  font-size: 0.95rem;
}

.prompt {
  color: var(--color-cyan); /* The signature turquoise pops here */
  font-weight: bold;
}

input, textarea {
  background: transparent;
  border: none;
  border-bottom: 2px solid rgba(255, 255, 255, 0.1);
  color: var(--color-text);
  font-family: 'Courier New', Courier, sans-serif;
  font-size: 1.1rem;
  padding: 8px 0;
  transition: all 0.3s ease;
}

input:focus, textarea:focus {
  outline: none;
  border-bottom-color: var(--color-cyan);
  box-shadow: 0 10px 10px -10px rgba(40, 194, 194, 0.4); /* Glows when typed in */
}

/* The Execute Button */
.transmit-btn {
  margin-top: 20px;
  padding: 16px 0;
  background-color: transparent;
  color: var(--color-accent);
  border: 2px solid var(--color-accent);
  border-radius: 4px;
  font-family: 'Courier New', Courier, monospace;
  font-weight: bold;
  font-size: 1.1rem;
  letter-spacing: 2px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.transmit-btn:hover:not(:disabled) {
  background-color: var(--color-accent);
  color: var(--color-bg-1);
  box-shadow: 0 0 20px rgba(195, 155, 87, 0.3);
}

.transmit-btn:disabled {
  opacity: 0.5;
  cursor: wait;
}
</style>