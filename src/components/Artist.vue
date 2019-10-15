<template lang="pug">
    li 
        h2: a(:href="artist.url" target="_blank") {{ artist.name }}
        h4:  a(:text="artist.listeners" target="_blank") Total listeners : {{ artist.listeners}}
        //- img(:src="artist.image[2]['#text']")
</template>

<script>

export default {
 name:'artist',
 props: [ 'artist' ]
}
</script>

<style lang="stylus" scoped>
li.artist
    margin 10px
    display inline
    padding 10px
    width auto

</style>
