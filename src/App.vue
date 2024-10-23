<!-- <template>
  <div>
    <h1>( v-for Rendering )</h1>
    <div :style="border"></div>
    <h2 v-for="(name, index) in names" :key="name">{{ index }}: {{ name }}</h2>
    <hr />
    <h2 v-for="name in fullname" :key="name.first">
      {{ name.first }} {{ name.last }}
    </h2>
    <hr />
    <div v-for="player in players" :key="player.name">
      <h2>{{ player.name }}</h2>
      <p v-for="formt in player.format" :key="formt">{{ formt }}</p>
    </div>
    <hr />
    <h2 v-for="(value, index, key) in myInfo" :key="value">
      {{ key }} : {{ index }} = {{ value }}
    </h2>
    <hr />
    <template v-for="name in namess" :key="name">
      <h2 v-if="name === 'Saeed Ullah'">{{ name }}</h2>
    </template>
    <hr />
  </div>
</template>
<script>
export default {
  data() {
    return {
      names: ["saeed", "zohaib", "samad", "ikram"],
      border: {
        border: "2px white solid",
        width: "500px",
      },
      fullname: [
        { first: "saeed", last: "ullah" },
        { first: "zohaib", last: "quraishi" },
        { first: "ikram", last: "durani" },
      ],
      players: [
        {
          name: "Babar Azam",
          format: ["T20", "ODI", "Test"],
        },
        {
          name: "M Rizwan",
          format: ["T20", "ODI", "Test"],
        },
      ],
      myInfo: {
        name: "Saeed Ullah",
        age: "24",
        class: "10th blue",
      },
      namess: ["Saeed Ullah", "Ikram Ullah", "Tahir Ullah"],
    };
  },
};
</script> -->

<!-- <script>
export default {
  data() {
    return {
      count: 0,
    };
  },
  methods: {
    increment() {
      this.count++;
    },
    decrement() {
      this.count--;
    },
    reset() {
      this.count = 0;
    },
    greet() {
      alert("Hello, Vue!");
    },
  },
};
</script>
<template>
  <div>
    <p>Count: {{ count }}</p>
    <button @click="increment">Increment</button>
    <button @click="decrement">Decrement</button>
    <button @click="reset">Reset</button>
    <button @click="greet">Greet</button>
  </div>
</template> -->

<template>
  <h2>{{ count }}</h2>
  <button @click="inc(1)">increment 1</button>
  <button @click="inc(5)">increment 5</button>
  <button @click="dec(1)">decrement 1</button>
  <button @click="dec(5)">decrement 5</button>
  <button @click="showResetConfirmation">reset</button>
</template>

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
    inc(num) {
      this.count += num;
    },
    dec(num) {
      this.count -= num;
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
<!-- <template>
  <div class="registration-form">
    <h2>Registration Form</h2>
    <form @submit.prevent="registerUser">
      <div>
        <label for="name">Name:</label>
        <input type="text" v-model="form.name" required />
        <span v-if="errors.name">{{ errors.name }}</span>
      </div>

      <div>
        <label for="username">Username:</label>
        <input type="text" v-model="form.username" required />
      </div>

      <div>
        <label for="email">Email:</label>
        <input type="email" v-model="form.email" required />
        <span v-if="errors.email">{{ errors.email }}</span>
      </div>

      <div>
        <label for="password">Password:</label>
        <input type="password" v-model="form.password" required />
      </div>

      <div>
        <label for="status">Status:</label>
        <select v-model="form.status" required>
          <option value="">Select Status</option>
          <option v-for="status in statuses" :key="status" :value="status">
            {{ status }}
          </option>
        </select>
        <span v-if="errors.status">{{ errors.status }}</span>
      </div>

      <button type="submit">Register</button>
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      form: {
        name: "",
        username: "",
        email: "",
        password: "",
        status: "",
      },
      statuses: ["active", "inactive"],
      errors: {},
    };
  },
  methods: {
    validateForm() {
      this.errors = {};

      if (this.form.name.length < 6) {
        this.errors.name = "Name must be more than 6 letters.";
      }

      const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      if (!emailPattern.test(this.form.email)) {
        this.errors.email = "Email must be a valid email address.";
      }

      if (!this.statuses.includes(this.form.status)) {
        this.errors.status = "Status must be either 'active' or 'inactive'.";
      }

      return Object.keys(this.errors).length === 0;
    },
    async registerUser() {
      if (this.validateForm()) {
        try {
          const response = await axios.post(
            "http://192.168.1.102:8000/api/register/",
            this.form
          );
          alert("User registered successfully");
          console.log(response.data);
        } catch (error) {
          console.error("Registration failed:", error.response.data);
        }
      }
    },
  },
};
</script>

<style scoped>
.registration-form {
  width: 300px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 5px;
}

.registration-form label {
  display: block;
  margin-bottom: 5px;
}

.registration-form input,
.registration-form select {
  width: 100%;
  padding: 8px;
  margin-bottom: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.registration-form button {
  width: 100%;
  padding: 10px;
  background-color: #28a745;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.registration-form button:hover {
  background-color: #218838;
}

span {
  color: red;
  font-size: 12px;
}
</style> -->
