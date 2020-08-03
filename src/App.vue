<template>
  <div id="app">
    <header class="bg-success">
      <div class="container p-3 text-white">
        <h2>Good {{ timePeriod }}</h2>
        <h4>{{ todayInfo }}</h4>
      </div>
    </header>
    <main class="container mt-5">
      <!-- Adding new task -->
      <div class="row">
        <div class="col-9">
          <input
            type="text"
            v-on:keyup.enter="addNewToDo"
            v-model="newInputText"
            class="form-control"
            placeholder="What need to be completed today?"
          />
        </div>
        <div class="col-3">
          <button class="btn btn-success btn-block" v-on:click="addNewToDo">
            Add
          </button>
        </div>
      </div>
      <!-- Task list -->
      <div class="row border" v-for="task in tasks" v-bind:key="task.action">
        <div class="col-2 p-2">
          <input type="checkbox" v-model="task.done" />
          {{ task.done }}
        </div>
        <div class="col-10 p-2">
          {{ task.action }}
        </div>
      </div>
    </main>
    <footer class="fixed-bottom">
      <p class="text-center">
        Created by <a v-bind:href="authorUrl">{{ authorName }}</a>
      </p>
    </footer>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      today: new Date(),
      authorName: 'Anh Tung Bui',
      authorUrl: 'https://github.com/anhtungbui',
      tasks: [
        {
          action: 'Get up',
          done: true,
        },
        {
          action: 'Brush the teeth',
          done: false,
        },
        {
          action: 'Have a breakfast',
          done: false,
        },
      ],
      newInputText: '',
    };
  },
  methods: {
    addNewToDo() {
      while (this.newInputText != '') {
        this.tasks.push({ action: this.newInputText, done: false });
        this.newInputText = '';
      }
    },
  },
  computed: {
    timePeriod: () => {
      let today = new Date();
      let timePeriod = today.getHours();

      if (timePeriod >= 5 && timePeriod < 12) {
        return 'Morning';
      } else if (timePeriod >= 12 && timePeriod < 17) {
        return 'Afternoon';
      } else {
        return 'Evening';
      }
    },
    todayInfo: () => {
      let today = new Date();
      let formattedDate = new Intl.DateTimeFormat('en-GB').format(today);

      return formattedDate;
    },
  },
};
</script>
