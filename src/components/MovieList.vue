<template>
  <div>
    <table>
      <caption>
        Movies
        <div>
          <SearchBox @search="handleSearch" />
        </div>
      </caption>
      <thead>
        <tr>
          <th>Id</th>
          <th>Movie Name</th>
          <th>Director</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="movie in moviesDetails" :key="movie.id">
          <td>{{ movie.id }}</td>
          <td>{{ movie.movieName }}</td>
          <td>{{ movie.directorName }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from "axios";
import SearchBox from "@/components/SearchBox.vue";
export default {
  components: {
    SearchBox,
  },
  data() {
    return {
      movies: [],
      directors: [],
      searchQuery: "",
    };
  },
  async created() {
    try {
      this.movies = await this.fetchMovies();
      this.directors = await this.fetchDirectors();
    } catch (error) {
      console.error("Error fetching data:", error);
    }
  },
  computed: {
    moviesDetails() {
      return this.showMovies();
    },
  },
  methods: {
    fetchMovies() {
      axios
        .get("https://mocki.io/v1/5210535c-0673-42a0-8608-85b04158e5d2")
        .then((response) => {
          this.movies = response.data;
        })
        .catch((error) => {
          console.error("Error fetching movies:", error);
        });
    },
    fetchDirectors() {
      axios
        .get("https://mocki.io/v1/98864832-79a3-4775-b184-c477b3a24c6a")
        .then((response) => {
          this.directors = response.data;
        })
        .catch((error) => {
          console.error("Error fetching directors:", error);
        });
    },
    handleSearch(query) {
      this.searchQuery = query;
    },
    showMovies() {
      var movies = this.movies.map((movie) => {
        const director =
          this.directors &&
          this.directors.find((dir) => dir.id == movie.director);
        return {
          id: movie.id,
          movieName: movie.title,
          directorName: director ? director.name : "Unknown Director",
        };
      });
      if (this.searchQuery != "") {
        movies = movies.filter((movie) =>
          movie.movieName.toLowerCase().includes(this.searchQuery.toLowerCase())
        );
      }
      return movies;
    },
  },
};
</script>
