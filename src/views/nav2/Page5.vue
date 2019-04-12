<template>
  <div>
  <LangSelect></LangSelect>
 	 <el-button type="primary">{{$t('login.btn')}}</el-button>
	 <!--查询-->
	<strong class="title">{{$t('login.chee')}}</strong>
	<strong class="title">{{$t('login.address')}}</strong>
  </div>

</template>
<script>
import LangSelect from '@/components/home/LangSelect'
export default {
  components: { LangSelect },
  data () {
		return {
			
		}
	},
  mounted () {},
  methods: {}
}
</script>

