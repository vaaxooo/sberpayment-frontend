<template>
  	<div class="styles_routeSection__9ou9J">
		<div class="styles_layout__1AkLX">
			<div class="styles_header__1pWs-">
				<div class="styles_headerInner__3eiSi">
					<div class="styles_logotype__3hZ86">
						<img src="/payment/img/sberbank-logo-color.b918eacf.svg" alt="СберБанк">
					</div>
				</div>
			</div>
			<Nuxt />
			<div id="under-footer"></div>
		</div>
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