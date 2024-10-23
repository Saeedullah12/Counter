# Vue.js Counter App with Reset Confirmation

This is a simple Vue.js counter app that allows users to increment, decrement, and reset the count. When a user clicks the reset button, a confirmation dialog appears, allowing them to either reset the count to 0 or cancel the action and keep the previous count.

## Features
Increment: Increase the count by 1 each time the increment button is clicked.
Decrement: Decrease the count by 1 each time the decrement button is clicked.
Reset Confirmation: When the reset button is clicked, the user is asked to confirm whether they want to reset the count to 0. If confirmed, the count is reset. If declined, the count remains unchanged.
## Project Setup
### Installation :
Clone the repository:
git clone https://github.com/Saeedullah12/Counter.git

Navigate into the project folder:
cd counter

Install the necessary dependencies:
npm install
Start the development server
npm run dev
Open your browser and visit http://localhost:8080 to view the app.

## Code Explanation
### Template
The template consists of:

A display of the current count.
Three buttons: increment, decrement, and reset.
html 
<template>
  <h2>{{ count }}</h2>
  <button @click="inc">increment</button>
  <button @click="dec">decrement</button>
  <button @click="showResetConfirmation">reset</button>
</template>

### Script
#### Data properties:

count: The current count value.
previousCount: Stores the previous count before a reset confirmation.
isResetting: Boolean used to manage the reset process.
Methods:

inc(): Increases the count by 1.
dec(): Decreases the count by 1.
showResetConfirmation(): Asks the user for confirmation before resetting the count.
reset(): Resets the count to 0 after confirmation.
javascript

<script>
export default {
  name: "app",
  data() {
    return {
      count: 0,
      previousCount: 0,
      isResetting: false,
    };
  },
  methods: {
    inc() {
      this.count++;
    },
    dec() {
      this.count--;
    },

    showResetConfirmation() {
      this.previousCount = this.count;
      const confirmReset = confirm("Do you want to reset the count?");
      if (confirmReset) {
        this.reset();
      } else {
        this.count = this.previousCount;
      }
    },

    reset() {
      this.count = 0;
      alert("Count has been reset to 0.");
    },
  },
};
</script>

### Usage
Click the increment button to increase the count.
Click the decrement button to decrease the count.
Click the reset button to open a confirmation dialog. If you click "OK", the count will be reset to 0. If you click "Cancel", the count will remain as is.
