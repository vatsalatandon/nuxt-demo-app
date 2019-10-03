<template>
  <section class="container">
    <Navigation :pages='navItems'/>
    <div class="container__content">
      <h1>Please select a page you wish to view</h1>
    </div>
  </section>
</template>
<script>
import Navigation from '../components/Navigation';
import {createClient} from '../plugins/contentful';
const contentfulClient = createClient();
export default {
    components: {
      Navigation
    },
    asyncData ({env}) {
      return Promise.all([
        // fetch all blog posts sorted by creation date
        contentfulClient.getEntries({
          'content_type': 'page',
          order: '-sys.createdAt'
        })
      ]).then(([pages]) => {
        // return data that should be available
        // in the template
        return {
          navItems: pages.items
        }
      }).catch(console.error)
    }
  }
</script>

 <style>
/* .container {
  min-height: 100vh;
  display: flex;
  position: top;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.container_content {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
} */
</style>