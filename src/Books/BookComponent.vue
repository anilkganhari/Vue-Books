<template>
        <div class="tile">
            <div class="col-4">
                <img :src="book.volumeInfo.imageLinks.smallThumbnail" />
            </div>
            <div class="col-8 padding-left-10">
                <div><h4>{{book.volumeInfo.title}} {{book.volumeInfo.subtitle}}</h4></div>
                <div><i style="text-">{{book.volumeInfo.authors.join(',')}}</i></div>
                <div><span >Pages:{{book.volumeInfo.pageCount}}</span></div>
                <div><span >{{book.volumeInfo.description | truncate(140)}}</span></div>
            </div>
        </div>
</template>
<script>
export default {
  name: "BookComponent",
  props: {
    book: Object
  }
};
</script>
<style>
.tile {
  width: 100%;
  border: 1px solid #000;
  height: auto;
  display: inline-block;
}
</style>
