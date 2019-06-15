//激活帮助说明
<template>
  <div>
     <toolbar :title="$t('fund_free_title')"
          :showmenuicon="false"
          :showbackicon="true"
          ref="toolbar"
        >
    </toolbar>
    <card >
      <div class="help pa-1 pt-4" >
        <h2 class="help-t pt-1 pl-2">一、为什么账号需要激活</h2>
        <p class="help-c pl-2">
          彩虹是基于(Rainbow)的去中心化钱包。<br/>
          Rainbow的特性：账号（G地址）创建后并不能立即使用，需要进行账号激活。<br/>
          激活的唯一方式：老账号向新账号转账至少20ORC才能使用。这1ORC将被冻结在彩虹网络中。<br/>
        </p>
        <h2 class="help-t pt-1 pl-2">二、什么是ORC</h2>
        <p class="help-c pl-2">
          Rainbow原生资产的标识为ORC (通常指的彩虹币就是ORC)任何账户都可以持有ORC，可以在网络中使用ORC交易其他资产。类似于BTC、ETH。<br/>
        </p>
        <h2 class="help-t pt-1 pl-2">三、什么是资产授信</h2>
        <p class="help-c pl-2">
          Rainbow的任意一个账户可以任意发行一种资产，充分体现价值互联网的特性。<br/>
          例如：账户A发行资产：BTC，账户B也发行资产：BTC，但二者的发行地址绝对不同，所以两种资产属于不同发行资产，由发行账户背后的人、组织或机构进行信用保证。<br/>
          您想要持有某一种发行资产，首选需要信任该资产的发行账户，即手动添加信任线（Trustline）。添加一项资产需要冻结0.5ORC。<br/>
        </p>

        <h2 class="help-t pt-1 pl-2">四、冻结与消耗</h2>
        <p class="help-c pl-2">
          1.冻结定义：是可以解冻的一次性抵押。根据Rainbox网络特性，所有的冻结都可以解冻，所以您不用担心被冻结的ORC，它将一直属于您的资产。<br/>
          2.消耗定义：是操作手续费。这部分ORC会因您的部分行为被消耗掉，属于您的成本。<br/>
          3.所有需要冻结、消耗ORC的内容包含：<br/>
          &nbsp;&nbsp;a.激活：冻结1ORC<br/>
          &nbsp;&nbsp;b.添加资产：冻结0.5ORC/个<br/>
          &nbsp;&nbsp;c.挂单：冻结0.5ORC/次（交易成功后自动解冻）<br/>
          &nbsp;&nbsp;d.操作：消耗0.00001ORC/次。操作行为包括：转账、授信、吃单、撤单等，凡是需要记录到Rainbox网络且被Rainbox网络认可的行为都需要消耗0.00001ORC<br/>
          4.如果您首次创建账号并进行最简单的交易，激活账号（冻结1ORC）+授信A资产（冻结0.5ORC）+授信B资产（冻结0.5ORC）+挂单（冻结0.5ORC）+交易（消耗0.00001ORC）=2.50001ORC。即首次的交易需要最小余额为2.50001ORC；<br/>
          5.如果第二次进行相同的动作，因为账号已经激活，资产已经添加，则需要最小余额0.50001ORC；<br/>
          6.综上所述，每次交易您的成本仅为0.00001ORC，是不是很便宜呀。看不懂，没关系，您只要知道：在彩虹钱包交易成本很低，可以忽略不计。<br/>
        </p>

        <h2 class="help-t pt-1 pl-2">五、友情提示</h2>
        <p class="help-c pl-2">
          随着您的姿势越来越熟练，多存点ORC可以防止交易行为被打断。另，ORC本身也是可以交易的。<br/>
        </p>

        <h2 class="help-t pt-1 pl-2">六、联系我们</h2>
        <p class="help-c pl-2">
          <!--1.TG群：<span @click="toHref('https://t.me/fchain_io')">https://t.me/fchain_io</span><br/>-->
          1.网址：<span @click="toHref('https://lhtech.info/')">https://lhtech.info/</span><br/>
        </p>



      </div>
    </card>
  </div>
</template>

<script>
import { mapState, mapActions} from 'vuex'
import Toolbar from '@/components/Toolbar'
import Card from '@/components/Card'


export default {
  data(){
    return {
      working: false,
      err: null,
    }
  },
   computed:{
    ...mapState({
      account: state => state.accounts.selectedAccount,
      accountData: state => state.accounts.accountData,
      islogin: state => (state.accounts.accountData.seed ? true : false),
    }),
  },
  methods: {
    toHref(url){
      window.open(url, "_system");
    }
  },
  components: {
    Toolbar,
    Card,
  }


}
</script>


<style lang="stylus" scoped>
@require '~@/stylus/color.styl'
.help
  color: $primarycolor.font
  .help-t
    font-size: 16px
    font-weight: bold
    color: $primarycolor.green
  .help-c
    font-size: 14px
</style>
