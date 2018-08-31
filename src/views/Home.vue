<template>
  <div class="home">
    <section class="hero is-primary">
      <div class="hero-body has-text-centered">
        <div class="container">
          <h1 class="title">
            JTester.com
          </h1>
          <h2 class="subtitle">
            Easily diff the JSON in your API's
          </h2>
          <a
            href="/diff"
            class="button is-info is-medium"
            disabled
          >Get Started Online (coming soon)</a>
        </div>
      </div>
    </section>
    <section class="hero">
      <div class="hero-body">
        <div class="container">
          <div class="columns">
            <div class="column">
              <h1 class="title is-size-2">
                JSON-DIFF-CLI
              </h1>
              <h2 class="subtitle is-size-4">
                Run a suite of tests right from your command line. json-diff-cli is
                easily integratable into any CI platform and can be used to test differences
                before and after deployments.
              </h2>
              <div class="field is-grouped">
                <p class="control">
                  <a href="https://github.com/j-tester/json-diff-cli" class="button is-success is-medium">Github</a>
                </p>
                <p class="control">
                  <a href="/diff" class="button is-info is-medium" disabled>
                    Try Online (coming soon)
                  </a>
                </p>
              </div>
            </div>
            <div class="column">
<pre>
<code class="json">// ~/tests/v1-api-test.json
{{JSON.stringify(this.sample, null, 2)}}
</code></pre>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
// @ is an alias to /src
import sample from '@/../public/sample.json';

export default {
  name: 'home',
  data() {
    return {
      sample,
    };
  },
};
</script>
