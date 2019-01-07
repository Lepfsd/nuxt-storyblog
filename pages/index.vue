<template>
  <section id="posts">
    <PostPreview 
      v-for= "post in posts"
      :key="post.id"
      :title="post.title"
      :excerpt="post.previewText"
      :thumbnailImage="post.thumbnailUrl"
      :id="post.id" />
  </section>
</template>

<script>
import Logo from '~/components/Logo.vue'
import PostPreview from '@/components/Blog/PostPreview';

export default {
  components: {
    PostPreview
  },
  asyncData(context){
    return context.app.$storyapi
      .get("cdn/stories", {
        version: "draft",
        starts_width: 'blog/'
      }).
      then(res => {
        return {
          posts: res.data.stories.map(bp => {
            return {
              id: bp.slug,
              title: bp.content.title,
              previewText: bp.content.summary,
              thumbnailUrl: bp.content.thumbnail
            };
          })
        };
      });
  }
  /*data(){
    return {
      posts: [
        {
          title: "A new beginig",
          previewText: 'this will be awesome, dont miss it',
          thumbnailUrl: 'https://food.fnr.sndimg.com/content/dam/images/food/fullset/2015/12/1/3/WU1207H_Spaghetti-Carbonara_s4x3.jpg.rend.hgtvcom.616.462.suffix/1452882192060.jpeg',
          id: 'a-new-beginig'
        },
        {
          title: "A second beginig",
          previewText: 'this will be awesome, dont miss it',
          thumbnailUrl: 'https://food.fnr.sndimg.com/content/dam/images/food/fullset/2015/12/1/3/WU1207H_Spaghetti-Carbonara_s4x3.jpg.rend.hgtvcom.616.462.suffix/1452882192060.jpeg',
          id: 'a-second-beginig'
        }
      ]
    };
  }*/
};
</script>

<style scoped>
  #posts {
    padding-top: 2rem;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }
</style>
