<template>
	
</template>
<script type="text/javascript">
import {mapGetters} from 'vuex'
	export default {
		data(){
			return {
				type:null
			}
		},
		created(){
			this.type=this.$route.params.id;
			this.$store.dispatch('changeShow',this.$route.params.id)
			this.$store.dispatch('changeNowbrand',this.$route.params.id);
		},
		watch:{
			$route(){
				
				this.type=this.$route.params.id;
				this.$store.dispatch('changeShow',this.$route.params.id)
				this.$store.dispatch('changeNowbrand',this.$route.params.id)
				
			}
		},
		computed:{
			...mapGetters({
				contents:'getIntro'
			})
		
		}
	}
</script>
<style scoped>

</style>