<template>
  <div class="container">    
    <div class="row" id="bookContainer">
      {{this.selectBook.id}}
      <!-- TO display the featured books on the TOP on the mobile  -->
      <div class="col-rightcontainer" v-if="width<=768">
         <ul class="row" >
          <li v-for="fBook in featuredBooks" v-bind:key="fBook.id" class="featured"   v-on:click="selectBook(fBook)"  v-bind:class="{ 'selected': selectedBooks | isSelected(fBook) }"><book-Component :book="fBook" ></book-Component></li>      
        </ul>
      </div>
      <div class="col-leftcontainer"  ref="leftContainer">
        <ul class="row" v-for="couple in books">
          <li v-for="book in couple" v-bind:key="book.id" class="col-5 box" v-on:click="selectBook(book)"  v-bind:class="{ 'selected': selectedBooks | isSelected(book) }"><book-Component :book="book" ></book-Component></li>      
        </ul>
      </div>
      <!-- To display the featured book on left to the book list on Desktop view -->
      <div class="col-rightcontainer" ref="rightContainer" v-if="width > 768">
         <ul class="row" >
          <li v-for="fBook in featuredBooks" v-bind:key="fBook.id" class="featured" v-on:click="selectBook(fBook)"  v-bind:class="{ 'selected': selectedBooks | isSelected(fBook) }"><book-Component :book="fBook" ></book-Component></li>      
        </ul>
      </div>      
    </div>
   </div>
</template>

<script>
import axios from "axios";
import BookComponent from "./BookComponent.vue";
export default {
  name: "BookList",
  components: {
    BookComponent
  },
  props: {
    width: Number
  },
  data: function() {
    return {
      selectedBooks: [],
      books: [],
      featuredBooks: []
    };
  },
  methods: {
    selectBook: function(book) {
      if (!this.isSelected(book)) {
        this.selectedBooks.push(book);
      } else {
        this.selectedBooks.splice( this.findSelectedBookIndex(book), 1);
      }
      // To retain selected books on reload.
      localStorage.setItem("selectedBooks", JSON.stringify(this.selectedBooks));
    },
    findSelectedBookIndex: function(book) {
      if (this.selectedBooks) {
        return this.selectedBooks.findIndex(x => x.id == book.id);
      } else {
        return -1;
      }
    },
    isSelected: function(book) {
      return this.findSelectedBookIndex(book) > -1;
    }
  },
  created: function() {
    // Get the selected Books
    var selectedBooks = JSON.parse(localStorage.getItem("selectedBooks"));
    if (selectedBooks) {
      this.selectedBooks = selectedBooks;
    } else {
      this.selectedBooks = [];
    }
    // API to pull books.
    axios
      .get("https://www.googleapis.com/books/v1/volumes?q=HTML5")
      .then(response => {
        // JSON responses are automatically parsed.
        this.books = response.data.items.map(x => {
          x.selected = false;
          return x;
        });
        var unflat = [];
        var fetured = [];
        // Make a two dimensional array of books length 2 , So to display the books in two columns.
        while (this.books.length) {
          var spliced = this.books.splice(0, 2);
          if (this.books.length == 0) {
            fetured = spliced;
          }
          unflat.push(spliced);
        }
        this.books = unflat;
        this.featuredBooks = fetured;
      })
      .catch(e => {
        this.errors.push(e);
      });
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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
</style>
