<template>
  <div id="Home">
    <h2>{{title}}</h2>
    <div id="content">
      <div
        v-for="url in urls"
        v-bind:key="url.id"
        v-bind:class="{ 'open': url.isOpen, 'acd-block': true}"
      >
        <label class="acd-label">
          <span>
            <font-awesome-icon icon="chevron-down" @click="toggleAcd(url)"/>
          </span>
          URL:
          <input type="text" name="URL" size="50" v-model="url.url">
          <span>
            <font-awesome-icon icon="plus" @click="addUrl"/>
          </span>
          <span>
            <font-awesome-icon icon="minus"/>
          </span>
        </label>
        <div v-for="param in url.params" v-bind:key="param.id" class="acd-content">
          PARAM:
          <input type="text" name="KEY" v-model="param.key">
          <input type="text" name="VALUE" v-model="param.value">
          <span>
            <font-awesome-icon icon="plus"/>
          </span>
          <span>
            <font-awesome-icon icon="minus"/>
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Home",
  props: {
    title: String
  },
  data: function() {
    return {
      urls: [
        {
          id: 1,
          url: "hoge",
          params: [{ id: 1, key: "key1", value: "value1" }],
          nextParamId: 2,
          isOpen: true
        }
      ],
      nextUrlId: 2
    };
  },
  methods: {
    toggleAcd: function(url) {
      url.isOpen = !url.isOpen;
    },
    addUrl: function() {
      this.urls.push({
        id: this.nextUrlId++,
        url: "hoge",
        params: [{ id: 1, key: "key1", value: "value1" }],
        nextParamId: 2,
        isOpen: true
      });
    },
    addParam: function() {}
  }
};
</script>

<style scoped>
#content .acd-block label span {
  padding: 0 2px 0 2px;
}

#content .acd-block .acd-label {
  background: #333;
  color: #fff;
  display: block;
  margin-bottom: 1px;
  padding: 10px;
}

#content .acd-block .acd-content {
  border: 1px solid #333;
  height: 0;
  opacity: 0;
  padding: 0 10px;
  -webkit-transition: 0.5s;
  transition: 0.5s;
  visibility: hidden;
}

#content .acd-block.open .acd-content {
  height: 40px;
  opacity: 1;
  padding: 10px;
  visibility: visible;
}
</style>
