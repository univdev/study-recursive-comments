<style scoped>
.comment {
  border-radius: 4px;
  box-shadow: 0 0 5px rgba(0, 0, 0, .2);
  padding: 16px;
}
.comment__author {
  font-weight: bold;
  font-size: 24px;
  margin-bottom: 8px;
}
.comment__content {
  line-height: 24px;
}
.comment__child {
  margin-top: 16px;
}
.button {
  border-radius: 8px;
  padding: 8px 16px;
  background-color: #FFF;
  border: 1px solid #EEE;
  margin-top: 16px;
}
</style>

<template>
  <div class="comment">
    <div class="comment__author">{{ author }}</div>
    <div class="comment__content">{{ content }}</div>
    <Comment
      v-for="(comment, key) in children"
      :key="key"
      class="comment__child"
      :author="comment.author"
      :content="comment.content"
      :children="comment.comments"
      @click:save-button="onClickSaveButton"></Comment>
    <div class="comment__buttons">
      <button
        class="button"
        @click="onClickSaveButton">저장</button>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue';
import Comment from './Comment.vue';

export type CommentType = {
  author: String,
  content: String,
  comments: Array<CommentType>,
};

export default defineComponent({
  props: {
    author: {
      type: String as PropType<String>,
      required: false,
      default: '작성자',
    },
    content: {
      type: String as PropType<String>,
      required: false,
      default: null,
    },
    children: {
      type: Array as PropType<Array<CommentType>>,
      required: false,
      default: () => [],
    },
    depth: {
      type: Number as PropType<number>,
      required: false,
      default: 0,
    },
  },
  setup(props, { emit }) {
    const { author, content, children } = props;
    const onClickSaveButton = () => {
      emit('click:save-button');
    };
    return {
      author,
      content,
      children,
      onClickSaveButton,
    };
  },
});
</script>
