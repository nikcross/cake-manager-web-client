<template>
  <form id="newCakeForm">
    <fieldset>
      <legend>New Cake</legend>
    <div class="grid-container">
      <div class="grid-x grid-padding-x">
        <div class="medium-6 cell">
          <label>Title
            <input type="text" placeholder="Cake title" id="title" v-model="cake.title">
          </label>
        </div>
        <div class="medium-6 cell">
          <label>Image Url
            <input type="text" placeholder="Cake image url" id="image" v-model="cake.image">
          </label>
        </div>
        <div class="medium-12 cell">
          <label>Description
            <textarea placeholder="Description of the cake" id="description" v-model="cake.description"></textarea>
          </label>
        </div>
        <div class="medium-12 cell">
          <a class="button" v-on:click="$emit('addCakeEvent', cake)">Add A New Cake</a>
        </div>
      </div>
    </div>
    </fieldset>
  </form>
</template>

<script>

export default {

  data() {
    return {
      cake: {
        title: "1",
        description: "2",
        image: "3",
      }
    };
  }
}
</script>

<style>
  legend {
    margin-left: 10px;
    padding: 5px;
  }

  fieldset {
    border: solid 1px;
    border-radius: 10px;
  }
</style>