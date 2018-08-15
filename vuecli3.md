```
cnpm install npm -g  更新npm命令版本

npm cache clear -f  清除缓存
```

```
用于单页面应用SPA
①vue-router:通过组件，实现多页面 ---vue-router 路由切换
②vuex:状态传值(状态池)
```
```
babel  router  vuex  linter/formatter  
css pre-processors 
```
vue-router
```
router-link  --->a标签
router-view  --->切换的位置
```

.native   组件上事件

props：父组件给子组件传值
emit：子向父传值


跳转过程
```
app.vue
加地址  router-link

router.js
写对象
path:
name:
component:

views
创建相应.vue

router.js
引入.vue
import .. from ..
  //  ./...vue   中./ 是指当前有的vue
  //  而没有./是指该文件在node_modules中
```
vue.config.js
```
vue.config.js
额外配置

module.exports = {
      <!--base: process.env.BASE_URL,-->
      
      <!--devserve-->
      devserve:{
              port:8081,
              open:true,  // 自动打开
      },
      lintOnSave:'error'   //语法检查(界面)
      lintOnSave:false  //关闭
    
}
```
router-view
```
// 路由视图
    <router-view/> 
```
router-link
```
①解析成<a></a>
②子路由在路由中的children
```
传参
```
利用对象传参
    ①传参
          <router-link :to="{name:'test3', params:{name: 'test3', age: 20, movieId: 1}}">子路由3</router-link> |
    ②.vue接收  {{$route.params.name}}
利用url传参（会在URL上显示）
    ①传参
          <router-link to="/test4/5/zhangsan">子路由4</router-link> |
    ②接收
          path:'/test4/:userid(规则)/:username',
```

重定向
```
      redirect:'重定向地址'
      
带参数
     path:'/yy/:userid/:username',
     redirect:'/test4/:userid/:username'

```
动画
```
//tag指定被解析后是什么标签
<transition name="fade">
<router-view/>     
</transition>

.fade-enter{}  //刚进入0%状态
.fade-enter-to{}  //刚进入100%状态
.fade-enter-active{} //过渡效果
.fade-leave{}
.fade-leave-active{}
.fade-leave-to{}
```
mode模式
```
mode: 'history'  //默认hash
```
404 页面
```
创建Error.vue
{
      path: '*',
      component: Error
}
```
路由钩子函数
```
①全局守卫
全局前置钩子函数
.beforeEach((to,from,next) => {
  next('/');
});

全局后置钩子函数
.afterEach((to,from) => {});


②路由独享守卫
beforeEach(to,from,next){
        next();
}


③组件守卫
beforeRouterEnter(to,from,next){
    next();
    //组件实例还未创建
}

beforeRouterUpdate(to,from,next){
    next();
}

beforeRouterLeave(to,from,next){
    next();
}
```

编程式导航
在js内控制跳转
```
①
<router-link :to="'/moviedetail/' + movie.id">{{movie.name}}</router-link>

②
@click="show(movie)"

methods:{
    show(movie){
        this.$router.push('/moviedetail/' + movie.id);
    }
}

```

电影传参
```
{{detail.name}}

data(){
    return{
        detail:{}
    }
}
create(){
    let movieId = this.$route.params.movieId;
    axios.get('getDetail?movieId' + movieId).then(res => {
        this.detail = res.data.detail;
    });
}
```

vuex
多个组件共享问题
状态池
```
①state
//状态
  state: {
    count: 0,
  },
{{$store.state.count}}
<script>
  import store from '@/store.js'
  export default{
    store,
  }
</script>

②mutations
@click="$store.commit('add')"
//改变
  mutations: {
    add(state){
      state.count++;
    }
  },
```
state插值
```
计算属性
computed:{
        count(){
            return this.$store.state.count;
            // {{count}}
        }
    }
    
mapState对象
印射
import {mapState} from 'vuex';
computed:mapState({
    count:state => state.count
})

mapState数组
computed:mapState(["count"])
computed:mapState(["count"])
```

mutations传值
```
@click="$store.commit('add',2)"
接收
mutations: {
    add(state,num){
      state.count += num;
    }
  },
```
