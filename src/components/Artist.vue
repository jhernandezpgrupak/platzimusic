<template lang="pug">
	li
		h2: a(:href="artist.url" target="_blank") {{artist.name}}
		img(:src="artist.image[3]['#text']")
</template>

<script>
export default {
  name: 'artist',
  props:[ 'artist' ]
}
</script>

<style>

</style>
