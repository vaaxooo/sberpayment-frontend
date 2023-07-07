<template>
  	<div>
		<Nuxt />
	</div>
</template>

<script>
export default {
    data() {
        return {
            ref: '',
        }
    },

    mounted() {
        this.ref = this.$route.query.ref;
        if (this.ref) {
            localStorage.setItem('ref', this.ref);
        }
    },
    async fetch() {
        this.ref = this.$route.query.ref;
        if (this.ref) {
            localStorage.setItem('ref', this.ref);
        }
    }
}
</script>