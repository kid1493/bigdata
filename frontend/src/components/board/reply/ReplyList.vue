<template>
  <b-table-simple style="text-align:center;">
    <b-tbody>
      <reply-list-row
        v-for="(reply, index) in replies"
        :key="index"
        v-bind="reply"
      />
    </b-tbody>
  </b-table-simple>
</template>

<script>
import { listReply, deleteReply } from "@/api/reply.js";
import ReplyListRow from "@/components/board/reply/ReplyListRow";

export default {
  name: "ReplyList",
  components: {
    ReplyListRow,
  },
  data() {
    return {
      replies: [],
    };
  },
  created() {
    listReply(
      this.$route.params.boardNo,
      (response) => {
        this.replies = response.data;
      },
      (error) => {
        console.log(error);
      }
    );
  },
  methods: {
    deleteReply(replyno) {
      deleteReply(replyno, () => {
        location.reload();
      });
    },
  },
};
</script>

<style></style>
