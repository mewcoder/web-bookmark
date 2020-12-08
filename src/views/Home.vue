<template>
  <div class="wrap">
    <div class="class-box" v-for="(item, index) in data" :key="index">
      <div class="title">
        {{ item.classify }}
      </div>
      <div class="item-wrap">
        <div class="item" v-for="(site, id) in item.sites" :key="id">
          <div @click="handle(site.href)">
            <div class="logo">
              <img :src="site.logo" />
              <span>{{ site.name }}</span>
            </div>
            <div class="desc">
              {{ site.desc || '这个网站什么描述也没有...' }}
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Home',
  components: {
    // HelloWorld
  },
  data() {
    return {
      data: []
    };
  },
  created() {
    this.getData();
  },
  methods: {
    handle(url) {
      window.open(url, '_blank');
    },
    async getData() {
      const res = await this.$http.get('data.json');
      this.data = res.data;
    }
  }
};
</script>
<style lang="less">
body {
  margin: 0;
  padding: 0;
  background-color: #1b1b1b;
}
.wrap {
  width: 960px;
  margin: 0 auto;
  .class-box {
    margin-top: 50px;
    .title {
      font-size: 16px;
      font-weight: 500;
      color: #e6e6e6;
      margin-left: 5px;
      margin-bottom: 5px;
    }
    .item-wrap {
      display: flex;
      flex-wrap: wrap;
      .item {
        background-color: #363636;
        width: 190px;
        height: 80px;
        border-radius: 5px;
        padding: 15px;
        margin: 10px;
        transition: all 0.2s;
        &:hover {
          transform: translateY(-5px);
          cursor: pointer;
        }
        .logo {
          height: 40px;
          display: flex;
          align-items: center;
          img {
            width: 35px;
            height: 35px;
            border-radius: 50%;
            margin-right: 10px;
          }
          span {
            font-size: 15px;
            font-weight: 600;
            color: #d9d9d9;
            text-overflow: ellipsis;
            white-space: nowrap;
          }
        }
        .desc {
          color: #a6a6a6;
          font-size: 12px;
          padding-top: 10px;
          text-overflow: ellipsis;
        }
      }
    }
  }
}
</style>
