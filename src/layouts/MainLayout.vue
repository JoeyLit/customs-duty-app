<template>
  <div class="WAL position-relative bg-grey-4" :style="style">
    <q-layout view="lHh Lpr lFf" class="WAL__layout shadow-3" container>
      <q-header elevated>
        <!-- <q-toolbar class="bg-grey-3 text-black">
          <q-btn round flat>
            <q-avatar>
              <img :src="currentConversation.avatar" />
            </q-avatar>
          </q-btn>

          <span class="q-subtitle-1 q-pl-md"> customs Duty Calculator </span>

          <q-space />

          <q-btn round flat icon="search" />
        </q-toolbar> -->
        <q-toolbar class="bg-grey-3 text-black">
          <q-btn round flat>
            <q-avatar>
              <img src="../assets/gra_logo.png" />
            </q-avatar>
          </q-btn>

          <q-toolbar-title>Customs Duty Calculator</q-toolbar-title>
        </q-toolbar>
      </q-header>

      <q-page-container class="bg-grey-2">
        <router-view />
      </q-page-container>

      <q-footer class="">
        <q-toolbar class="flex flex-center bg-grey-3 text-black row">
          <span
            >Developed by
            <a target="blank" href="https:/twitter.com/JoeyLit9">
              Gabriel Nyarkoh |
            </a></span
          >
          <span>All rights reserved &copy; Copyright 2023</span>
        </q-toolbar>
      </q-footer>
    </q-layout>
  </div>
</template>

<script>
import { useQuasar } from "quasar";
import { ref, computed } from "vue";

const conversations = [
  {
    id: 1,
    person: "Razvan Stoenescu",
    avatar: "https://cdn.quasar.dev/team/razvan_stoenescu.jpeg",
    caption: "I'm working on Quasar!",
    time: "15:00",
    sent: true,
  },
];

export default {
  name: "WhatsappLayout",

  setup() {
    const $q = useQuasar();

    const leftDrawerOpen = ref(false);
    const search = ref("");
    const message = ref("");
    const currentConversationIndex = ref(0);

    const currentConversation = computed(() => {
      return conversations[currentConversationIndex.value];
    });

    const style = computed(() => ({
      height: $q.screen.height + "px",
    }));

    function toggleLeftDrawer() {
      leftDrawerOpen.value = !leftDrawerOpen.value;
    }

    function setCurrentConversation(index) {
      currentConversationIndex.value = index;
    }

    return {
      leftDrawerOpen,
      search,
      message,
      currentConversationIndex,
      conversations,

      currentConversation,
      setCurrentConversation,
      style,

      toggleLeftDrawer,
    };
  },
};
</script>

<style lang="sass">
.WAL
  width: 100%
  height: 100%
  padding-top: 20px
  padding-bottom: 20px

  &:before
    content: ''
    height: 127px
    position: fixed
    top: 0
    width: 100%
    background-color: #009688
    // background-color: gold

  &__layout
    margin: 0 auto
    z-index: 4000
    height: 100%
    width: 90%
    max-width: 950px
    border-radius: 5px

  &__field.q-field--outlined .q-field__control:before
    border: none

  .q-drawer--standard
    .WAL__drawer-close
      display: none

@media (max-width: 850px)
  .WAL
    padding: 0
    &__layout
      width: 100%
      border-radius: 0

@media (min-width: 691px)
  .WAL
    &__drawer-open
      display: none

.conversation__summary
  margin-top: 4px

.conversation__more
  margin-top: 0!important
  font-size: 1.4rem
</style>
