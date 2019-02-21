<template>
  <div id="diff">
    <section class="section">
      <div class="container">
        <div class="tabs is-large is-centered">
          <ul>
            <li :class="{ 'is-active': this.tab === 'json' }">
              <a @click="changeTab('json')">Diff JSON</a>
            </li>
            <li :class="{ 'is-active': this.tab === 'urls' }">
              <a @click="changeTab('urls')">Diff URLs</a>
            </li>
          </ul>
        </div>
        <div v-if="this.tab === 'json'">
          <diff-json />
        </div>
        <div v-if="this.tab === 'urls'">
          <diff-urls />
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import DiffJSON from '@/components/DiffJSON.vue';
import DiffURLs from '@/components/DiffURLs.vue';

export default {
  data() {
    return {
      tab: 'json',
    };
  },

  methods: {
    changeTab(name) {
      this.tab = name;
    },
  },

  components: {
    'diff-json': DiffJSON,
    'diff-urls': DiffURLs,
  },
};
</script>
