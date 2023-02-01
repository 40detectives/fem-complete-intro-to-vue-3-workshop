<script>
export default {
  data: () => ({
    newCharacter: {
      name: "(Anonymous)",
      hangul: "(?)",
      gender: "fluid",
    },
    cast: [
      {
        name: "Shin Seul Gi",
        hangul: "신슬기",
        gender: "female",
      },
      {
        name: "Park Se Jung",
        hangul: "박세정",
        gender: "female",
      },
      {
        name: "Lee So E",
        hangul: "이소이",
        gender: "female",
      },
      {
        name: "Lee Na Din",
        hangul: "이나딘",
        gender: "female",
      },
      {
        name: "Choi Seo Eun",
        hangul: "최서은",
        gender: "female",
      },
      // ! ! ! //
      {
        name: "Choi Jong Woo",
        hangul: "최종우",
        gender: "male",
      },
      {
        name: "Jo Yung Jae",
        hangul: "조융재",
        gender: "male",
      },
      {
        name: "Kim Han Bin",
        hangul: "김한빈",
        gender: "male",
      },
      {
        name: "Shin Dong Woo",
        hangul: "신동우",
        gender: "male",
      },
    ],
    favList: [],
  }),
  computed: {
    genderStatistics() {
      // returns object with the aggregation of genders in cast
      return this.cast.reduce(
        (obj, character) => (
          (obj[character.gender.toLocaleLowerCase()] = obj[character.gender.toLocaleLowerCase()]
            ? ++obj[character.gender.toLocaleLowerCase()]
            : 1),
          obj
        ),
        {}
      );
    },
  },
  methods: {
    makeFav(character) {
      if (this.favList.includes(character)) {
        this.favList = this.favList.filter((fav) => fav !== character);
      } else {
        this.favList.push(character);
      }
    },
    addNewCharacter() {
      this.cast.push(this.newCharacter);
      this.newCharacter = {
        name: "(Anonymous)",
        hangul: "(?)",
        gender: "fluid",
      };
    },
  },
};
</script>

<template>
  <h1>Single's Inferno S02</h1>
  <h2>Cast</h2>
  <p v-if="cast.length === 0">There are no characters</p>
  <ul v-else>
    <li
      v-for="character in cast"
      v-bind:key="character.name.replace(/\s+/gi, '-')"
    >
      <span>{{ character.name }}</span>
      <button v-on:click="makeFav(character)">❤️ Fav</button>
    </li>
  </ul>
  <h2>Fav Characters</h2>
  <ul v-if="favList.length > 0">
    <li
      v-for="character in favList"
      v-bind:key="character.name.replace(/\s+/gi, '-')"
    >
      <span>{{ character }}</span>
    </li>
  </ul>
  <p v-else>No favorite characters now</p>

  <h2>Statistics</h2>
  <ul>
    <li>Gender statistics: {{ genderStatistics }}</li>
    <li
      v-for="(stat, gender) in genderStatistics"
      v-bind:key="`stats-${gender}-${stat}`"
    >
      {{ gender }}: {{ (stat / cast.length).toFixed(3) }}%
    </li>
  </ul>

  <hr />

  <h2>Add a new Character</h2>
  <form action="" v-on:submit.prevent="addNewCharacter">
    <pre>{{ newCharacter }}</pre>
    <label>
      Name:
      <input type="text" v-model="newCharacter.name" />
    </label>
    <label>
      Korean Name:
      <input type="text" v-model="newCharacter.hangul" />
    </label>
    <label>
      Gender:
      <input type="text" v-model="newCharacter.gender" />
    </label>
    <button type="submit">Add New Character</button>
  </form>

  <hr />

  <h2>Example of a "v-for" with names joined by commas in between</h2>
  <p>
    <span
      v-for="(character, index) in cast"
      v-bind:key="`comma-separated-list-${index}`"
    >
      {{ character.name }}{{ index === cast.length - 1 ? "" : ", " }}
    </span>
  </p>
</template>

<style scoped></style>
