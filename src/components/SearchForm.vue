<template>
  <div class="search-form">
    <h3>Search HR133 (Covid "Relief" Package) for a term</h3>
    <a
      class="bill-link"
      href="https://rules.house.gov/sites/democrats.rules.house.gov/files/BILLS-116HR133SA-RCP-116-68.pdf"
      target="_blank"
      >Bill Text (pdf)</a
    >
    <form ref="form">
      <input v-model="input" placeholder="Enter Search Term" />
      <button @click.prevent="submit()">Submit</button>
    </form>

    <ul v-for="item in results" :key="item.term">
      <li>
        HR133 contains the word
        <span class="search-term"> {{ item.term }}</span>
        <span class="occurences"> {{ item.occurences }}</span> times
      </li>
    </ul>
  </div>
</template>

<script>
import BillText from "../assets/bill_text.txt";
export default {
  name: "HelloWorld",
  data() {
    return {
      input: "",
      billText: [],
      submitted: false,
      results: [],
    };
  },
  methods: {
    submit: function () {
      const term = this.input;
      const occurences = this.billText.reduce((acc, curr) => {
        return (acc += curr.toLowerCase().includes(term.toLowerCase()));
      }, 0);
      this.results.push({
        term: term,
        occurences: occurences,
      });
    },
  },
  mounted() {
    this.billText = BillText.split("\n");
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
a {
  text-decoration: none;
  color: cornflowerblue;
}
a:hover {
  text-decoration: underline;
}
h3 {
  margin-bottom: 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
input {
  margin-top: 10px;
}

.search-term,
.occurences {
  font-weight: bold;
  font-size: 1.2rem;
}
.search-term {
  /* text-decoration: underline; */
  border: 1px solid black;
  padding: 0 5px;
}
.occurences {
  color: cornflowerblue;
}
</style>
