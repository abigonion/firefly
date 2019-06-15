<template>
  <div>
    <tool-bar :title="$t(title)" :showmenuicon="false" :showbackicon="true" @goback="back">
      <v-btn icon slot="right-tool" @click="readAll">
        <i class="btn-readAll">全部已读</i>
      </v-btn>
    </tool-bar>
    <ul class="content">
      <li v-for="(item ,index) in messages" class="item" @click="goToDetils(item)" :key="index">
        <div :class="'item-title' + (reads.indexOf(item.link) === -1  ? '':' read')">{{item.title }}</div>
        <div class="item-time">{{ item.date }}</div>
        <span class="circular" v-if="reads.indexOf(item.link) === -1 "></span>
      </li>
    </ul>
  </div>
</template>

<script>
import ToolBar from "@/components/Toolbar";
import Scroll from "@/components/Scroll";
import { mapActions, mapState, mapGetters } from "vuex";
export default {
  name: "message-center",
  data() {
    return {
      title: "MessageCenter"
    };
  },
  components: {
    ToolBar,
    Scroll
  },
  methods: {
    ...mapActions(["getMessages", "selectMsg", "readAllMsg"]),
    back() {
      this.$router.back();
    },
    goToDetils(item) {
      this.selectMsg(item);
      this.$router.push({ name: "MessageDetils" });
    },
    readAll() {
      this.readAllMsg();
      this.$toasted.show(this.$t("ReadAllMsg"));
    }
  },
  computed: {
    ...mapGetters(["unReadCount"]),
    ...mapState({
      messages: state => state.message.items,
      reads: state => state.message.reads
    })
  }
};
</script>

<style lang="stylus" scoped>
@require '~@/stylus/color.styl';

.btn-readAll {
  font-size: 0.35rem;
  color: #fff;
  padding-right: 15px;
}

.content {
  .item {
    position: relative;
    padding: 0.2rem 0.2rem;
    background: #fff;
    margin: 0.1rem auto;
    border-bottom : 1px solid #999;

    .item-title {
      line-height: 24px;
      height: 24px;
      font-size: 0.45rem !important;
      white-space: nowrap;
      overflow: hidden;

      &.read {
        color: $secondarycolor.font;
      }
    }

    .item-time {
      font-size: 0.35rem;
      color: $secondarycolor.font;
    }

    .item-content {
      flex: 2;
      height: initial;
      text-overflow: ellipsis;
      overflow: hidden;
      white-space: nowrap;
      padding-top: 15px;
    }

    .circular {
      position: absolute;
      width: 0.2rem;
      height: 0.2rem;
      background: $primarycolor.red;
      border-radius: 0.2rem;
      right: 0.1rem;
      top: 0.1rem;
    }
  }
}
</style>
