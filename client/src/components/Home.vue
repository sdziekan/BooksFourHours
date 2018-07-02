<template>
  <v-layout>
    <v-flex>
      <v-card height="100px">
        <!-- <img src="../assets/3redbooks-300px.png"> -->
        <v-card-title>

          <v-spacer></v-spacer>
          <v-spacer></v-spacer>
          <v-text-field append-icon="search" label="Search" single-line hide-details v-model="search"></v-text-field>
        </v-card-title>
        <v-data-table hide-actions v-bind:headers="headers" v-bind:items="books" v-bind:search="search">
          <template slot="items" slot-scope="props">
            <td class="text-xs-center">
              <a v-bind:href="props.item.bUrl" target=”_blank”>{{ props.item.bTitle }}</a>
            </td>
            <td class="text-xs-right">{{ props.item.bAuthor }}</td>
            <td class="text-xs-right">{{ props.item.bGuest }}</td>
            <td class="text-xs-center">{{ props.item.bEpNumber }}</td>

            <td class="text-xs-right">
              <a v-bind:href="props.item.bShowNotes" target=”_blank”>Link to Show Notes</a>
            </td>
          </template>

        </v-data-table>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
import axios from "axios";
import api from "./api";

export default {
  name: 'Home',
  data() {
    return {

      books: [],
      search: '',
      headers: [
        { text: 'Book Title', align: 'left', value: 'bTitle' },
        { text: 'Author', value: 'bAuthor' },
        { text: 'Guest', value: 'bGuest' },
        { text: 'Episode Number', value: 'bEpNumber' },
        { text: 'Show Notes', sortable: false, value: 'bShowNotes' }
      ],
    }
  },
  created() {
    // function that GETS books from API
    api.getBooks().then(books => {
      this.books = books;
    });
  },
  computed: {
    //function to place items within an array each on their own line
    newLineWithinCell() {

    }
  }

}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

img {
  margin: 75px 0 40px 40%;
  width: 20%;
}
</style>
