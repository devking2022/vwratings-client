<template>
  <div class="commentItem mt-2">
    <b-badge v-if="comment.opinion === 1" variant="success">{{ comment.opinion | opinion }}</b-badge>
    <b-badge v-if="comment.opinion === 2" variant="danger">{{ comment.opinion | opinion }}</b-badge>
    <div class="commentItem__content">
      <p v-text="comment.content" v-linkified />
      <div class="commentItem__attachments">
        <viewer v-for="(attachment, key) in comment.attachments" :key="key">
          <img alt="Attachment" class="attachmentItem mr-2" :src="attachment.path"/>
        </viewer>
      </div>
    </div>
  </div>
</template>
<script>
import moment from "moment";

export default {
  props: {
    comment: {
      attachments: Array
    }
  },

  filters: {
    opinion(data) {
      if (typeof data === 'number') {
        if (data === 1) return 'positive';
        if (data === 2) return 'negative';
        return '';
      }
      return '';
    },
    date(data) {
      return moment(data).format('MMMM Do YYYY, h:mm:ss')
    }
  },

  data() {
    return {
      options: [
        {text: 'Positive', value: 1},
        {text: 'Negative', value: 0},
      ],
    }
  }
}
</script>
<style lang="scss">
.commentItem {
  font-size: 20px;
  background: transparent;
  display: block;
  margin: 20px 0;

  &__attachments {
    margin-top: 10px;
    display: flex;
    justify-content: flex-start;
  }

  &__content {
    min-height: 100px;
    border: 1px solid #204422;
    position: relative;
    background: #2083281a;
    border-bottom: none;
    padding: 15px;

    p {
      white-space: pre-line;
    }
  }

  &__attachmentsList {
    display: flex;
  }

  .attachmentItem {
    width: 50px;
    height: 50px;
    cursor: pointer;
    object-fit: cover;
  }

  p {
    margin-bottom: 0;
  }
}
</style>