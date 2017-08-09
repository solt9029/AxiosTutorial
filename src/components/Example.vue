<template>
  <div>
    <ul v-if="posts && posts.length">
      <li v-for="post of posts">
        <p><strong>{{post.time}}</strong></p>
        <p>{{post.code}}</p>
      </li>
    </ul>

    <ul v-if="errors && errors.length">
      <li v-for="error of errors">
        {{error.message}}
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'example',
  data: () => ({
    posts: [],
    errors: []
  }),

  // Fetches posts when the component is created.
  created() {
    axios.get('http://api.p2pquake.com/v1/human-readable')
    .then(response => {
      // JSON responses are automatically parsed.
      this.posts = response.data
    })
    .catch(e => {
      this.errors.push(e)
    })
  }
}
</script>