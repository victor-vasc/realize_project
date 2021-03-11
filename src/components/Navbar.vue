<template lang="html">
  <div>
  <b-navbar toggleable="lg" type="dark" fixed="top" variant="info" class="border-bottom  border-light">
    <b-navbar-toggle target="nav-collapse" class="border-0 pl-0"></b-navbar-toggle>
    <b-navbar-brand href="#">Realize App</b-navbar-brand>
    <div class="" v-if="navbarButtonIcon == 'Home'">
      <b-icon v-b-modal.modal-1 font-scale="2" icon="plus" variant="light" aria-label="Add"></b-icon>
    </div>
    <div class="" v-if="navbarButtonIcon == 'Metas'">
      <b-icon v-b-toggle.accordion font-scale="1.3" icon="arrows-angle-expand" variant="light" aria-label="Add"></b-icon>
    </div>

    <!-- <b-collapse id="nav-collapse" is-nav>
      <b-navbar-nav>
        <b-nav-item href="#">Link</b-nav-item>
        <b-nav-item href="#" disabled>Disabled</b-nav-item>
      </b-navbar-nav> -->

      <!-- Right aligned nav items -->
      <!-- <b-navbar-nav class="ml-auto">
        <b-nav-form>
          <b-form-input size="sm" class="mr-sm-2" placeholder="Search"></b-form-input>
          <b-button size="sm" class="my-2 my-sm-0" type="submit">Search</b-button>
        </b-nav-form>

        <b-nav-item-dropdown text="Lang" right>
          <b-dropdown-item href="#">EN</b-dropdown-item>
          <b-dropdown-item href="#">ES</b-dropdown-item>
          <b-dropdown-item href="#">RU</b-dropdown-item>
          <b-dropdown-item href="#">FA</b-dropdown-item>
        </b-nav-item-dropdown>

        <b-nav-item-dropdown right> -->
          <!-- Using 'button-content' slot -->
          <!-- <template #button-content>
            <em>User</em>
          </template>
          <b-dropdown-item href="#">Profile</b-dropdown-item>
          <b-dropdown-item href="#">Sign Out</b-dropdown-item>
        </b-nav-item-dropdown>
      </b-navbar-nav>
    </b-collapse> -->
  </b-navbar>
</div>
</template>

<script>
export default {
  name: 'Navbar',
  props:{
    navbarButtonIcon: String,
  }
}
</script>

<style lang="css" scoped>
</style>
