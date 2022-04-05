<style scoped>

</style>

<template>
  <div>
    <Comment
      v-for="(comment, key) in comments"
      :key="key"
      :author="comment.author"
      :content="comment.content"
      :children="comment.comments"
      @click:save-button="onSave"></Comment>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Comment, { CommentType } from './components/Comment.vue';

export default defineComponent({
  components: {
    Comment,
  },
  setup() {
    const comments: Array<CommentType> = [{
      author: '박찬영',
      content: '댓글입니다!',
      comments: [{
        author: '박찬영',
        content: '하위 댓글입니다!',
        comments: [{
          author: '박찬영',
          content: '하위의 하위 댓글입니다!',
          comments: [],
        }],
      }],
    }];
    const onSave = () => {
      window.alert('저장 되었습니다!');
    };
    return { comments, onSave };
  },
});
</script>
