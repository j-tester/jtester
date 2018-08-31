<template>
  <div id="diff">
    <section class="section">
      <div class="container">
        <div class="tabs is-large is-centered">
          <ul>
            <li :class="{ 'is-active': this.tab === 'json' }"><a>Diff JSON</a></li>
            <li>Diff URLs (coming soon)</li>
          </ul>
        </div>
        <div v-if="this.tab === 'json'">
          <diff-json />
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import DiffJSON from '@/components/DiffJSON.vue';

export default {
  data() {
    return {
      tab: 'json',
    };
  },

  components: {
    'diff-json': DiffJSON,
  },
};
</script>
