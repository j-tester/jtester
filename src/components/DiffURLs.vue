
<template>
  <div id="diff-json">
    <div class="columns">
      <div class="column">
        <div class="field">
          <div class="control">
            <input
              type="text"
              class="input"
              v-model="leftURL"
              id="leftURL"
              placeholder="left url"
            >
          </div>
        </div>
      </div>
      <div class="column">
        <div class="field">
          <div class="control">
            <input
              type="text"
              class="input"
              v-model="rightURL"
              id="rightURL"
              placeholder="right url"
            >
          </div>
        </div>
      </div>
    </div>
    <div class="columns">
      <div class="column has-text-centered">
        <a
          :class="{
            button: true,
            'is-primary': true,
            'is-loading': this.loading
          }"
          @click="this.diffJSON"
        >Go!</a>
      </div>
    </div>
    <div class="columns" v-if="this.error">
      <div class="column">
        <div class="notification is-danger">
          {{ this.error }}
        </div>
      </div>
    </div>
    <table class="table is-fullwidth is-hoverable is-striped is-bordered" v-if="this.diff">
      <thead>
        <tr>
          <th>key</th>
          <th>left</th>
          <th>right</th>
          <th>diff</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="diff in this.diff" :key="diff.key">
          <td>{{ diff.key }}</td>
          <td>{{ diff.left }}</td>
          <td>{{ diff.right }}</td>
          <td>{{ diff.diff }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
// import axios from 'axios'
import { diffJSON } from 'json-diff-core';

export default {
  name: 'diff-urls',
  data() {
    return {
      leftURL: '',
      rightURL: '',
      leftJSON: '',
      rightJSON: '',
      error: null,
      diff: null,
      loading: false,
    };
  },
  methods: {
    async diffJSON() {
      this.loading = true;
      try {
        this.leftResponse = await fetch(this.leftURL);
      } catch (err) {
        this.error = 'failed to fetch from left url';
      }
      try {
        this.rightResponse = await fetch(this.rightURL);
      } catch (err) {
        this.error = 'failed to fetch from right url';
      }
      try {
        this.leftJSON = await this.leftResponse.json();
        this.leftJSON = JSON.stringify(this.leftJSON, null, 2);
      } catch (err) {
        this.diff = null;
        this.loading = false;
        this.error = 'Left JSON is invalid';
        return;
      }
      try {
        this.rightJSON = await this.rightResponse.json();
        this.rightJSON = JSON.stringify(this.rightJSON, null, 2);
      } catch (err) {
        this.diff = null;
        this.loading = false;
        this.error = 'Right JSON is invalid';
        return;
      }

      const diff = await diffJSON(
        JSON.parse(this.leftJSON),
        JSON.parse(this.rightJSON),
        { sortKeys: null },
      );
      this.error = null;
      this.diff = diff;
      this.loading = false;
    },
    prettyPrintJSON(json) {
      if (typeof json !== 'string') {
        // eslint-disable-next-line
        json = JSON.stringify(json, undefined, 2);
      }
      // eslint-disable-next-line
      json = json.replace(/&/g, '&amp;').replace(/</g, '&lt;').replace(/>/g, '&gt;');
      return json.replace(/("(\\u[a-zA-Z0-9]{4}|\\[^u]|[^\\"])*"(\s*:)?|\b(true|false|null)\b|-?\d+(?:\.\d*)?(?:[eE][+-]?\d+)?)/g, (match) => {
        let cls = 'number';
        if (/^"/.test(match)) {
          if (/:$/.test(match)) {
            cls = 'key';
          } else {
            cls = 'string';
          }
        } else if (/true|false/.test(match)) {
          cls = 'boolean';
        } else if (/null/.test(match)) {
          cls = 'null';
        }
        return `<span class="${cls}">${match}</span>`;
      });
    },
  },
};
</script>
