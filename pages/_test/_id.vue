<template>
  <div id="detail">
    <div id="wrapper">
      <Header />
      <div id="contents">
        <article :id="id">
          <div class="detail">
            <ul>
              <template v-for="item in data.media">
                <li v-html="createMediaDom(item, data.id)"></li>
              </template>
            </ul>

            <h3 class="first_title">{{ data.title }}</h3>
            <p class="first_date">{{ data.date }}</p>
            <p class="info">{{ data.text }}</p>

            <dl>
              <template v-for="link in data.links">
                <dt>{{ link[0] }}</dt>
                <dd>
                  <a :href="link[1]" target="_blank">{{ link[1] }}</a>
                </dd>
              </template>
            </dl>
          </div>
        </article>
      </div>
      <Footer />
    </div>
  </div>
</template>

<script>
import json from "@/assets/data.json";

async function checkData(id, dirname) {
  let obj = {
    is404: true,
    isRedirect: false,
    redirectPath: "",
    index: -1
  };

  if (dirname == "test") {
    if (id == undefined) {
      obj.is404 = false;
      obj.isRedirect = true;
      obj.redirectPath = "/";
    } else {
      let index = 0;
      for (let item of json.post) {
        if (item.id == id) {
          //Correct URL
          obj.is404 = false;
          obj.isRedirect = false;
          obj.index = index;
          break;
        }
        index++;
      }
    }
  } else {
    // これgenerate後動かない
    for (let item of json.post) {
      if (item.id == dirname) {
        obj.is404 = false;
        obj.isRedirect = true;
        obj.redirectPath = "/test/" + dirname + "/";
        break;
      }
    }
  }
  return obj;
}

export default {
  data() {
    return {};
  },
  async asyncData({ params, redirect, error }) {
    const dirname = params.test; //dirname
    const id = params.id;

    let check = await checkData(id, dirname);

    if (check.is404) {
      return error({ errorCode: 404 });
    }
    if (check.isRedirect) {
      return redirect(302, check.redirectPath);
    }

    let data = json.post[check.index];

    //detail page ok
    return { dirname, id, data };
  }
};
</script>

<style lang="scss"></style>
