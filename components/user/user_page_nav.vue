<template>
  <nav class="nav">
    <router-link
      v-for="(item, index) in navList"
      :key="index"
      :class="$route.name === item.url && 'active'"
      :to="{name: item.url, params: {id: $route.params.id}}"
      replace
    >
      {{ item.title }}
    </router-link>
  </nav>
</template>

<script>
import { mapGetters } from 'vuex'
export default {
  data() {
    return {

    }
  },
  computed: {
    ...mapGetters(['isMe']),
    navList() {
      const isMe = this.isMe(this.$route.params.id)
      if (isMe) return this.user
      else return this.user.filter(i => !i.self)
    },
    user() {
      return [
      // self 只有自己才能看
        { title: this.$t('user.creation'), url: 'user-id', self: false },
        // { title: this.$t('share'), url: 'user-id-share', self: false },
        { title: this.$t('user.draft'), url: 'user-id-draft', self: true },
        { title: this.$t('user.fan'), url: 'user-id-fan', self: false },
        { title: this.$t('user.follow'), url: 'user-id-follow', self: false },
        // { title: this.$t('user.buy'), url: 'user-id-buy', self: true },
        // { title: this.$t('user.bookmark'), url: 'user-id-bookmark', self: true },
        { title: this.$t('user.information'), url: 'user-id-info', self: false }
      ]
    }
  }
}
</script>

<style lang="less" scoped>
.nav {
  text-align: center;
  margin: 0 auto;
  padding: 20px 0 10px;
  display: block;
  flex-wrap: wrap;
  a {
    font-size: 18px;
    line-height:33px;
    text-decoration: none;
    margin: 0 10px;
    flex: 1;
    cursor: pointer;
    color: #333;
    &:nth-of-type(1) {
      margin-left: 0;
    }
    &:nth-last-child(1) {
      margin-right: 0;
    }
    &.active {
      font-weight:bold;
      color:rgba(0,0,0,1);
    }
  }
}
</style>
