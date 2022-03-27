## Vuex 相关
### Vuex 定义
* 状态管理模式
* 集中式存储所有组件的状态的小仓库
* 保持我们存储的状态以一种可以预测的方式发生变化
### Vuex 简单使用 （vue 2.x）
* const store = new Vuex.Store({state: {<!-- 放置全局属性 -->},});
* this.$store.state.name <!-- 使用方法1（官方建议computed里调用）-->
* ...mapState(['name']) <!-- 使用方法2 从vuex中导入mapState 对stroe.xx进行结构 -->
### Vue api
#### getters 修饰器
*  getters: {
        getMessage(state) { // 获取修饰后的name，第一个参数state为必要参数，必须写在形参上
            return `hello${state.name}`;
        }
    },
* this.$store.getters.getMessage <!-- 使用方法1 -->
* ...mapGetters(['getMessage'])	<!-- 使用方法2 -->
* ...mapGetters({ aliasName: 'getMessage' }), <!-- 使用方法3 该写法用来取别名-->
#### Mutation 专用修改方法(不能异步)
* mutations: { // 增加nutations属性
    setNumber(state,payload) {  // 增加一个mutations的方法，方法的作用是让num从0变成5，state是必须默认参数
        state.number = payload.number;
    }
},
* this.$store.commit('setNumberIsWhat', { number: 666 }); <!-- 使用方法 -->
#### Actions 异步操作（异步放这）
* actions: {   // 增加actions属性
        setNum(content) {  // 增加setNum方法，默认第一个参数是content，其值是复制的一份store
            return new Promise(resolve => {  // 我们模拟一个异步操作，1秒后修改number为888
                setTimeout(() => {
                    content.commit('setNumberIsWhat', { number: 888 });
                    resolve();
                }, 1000);
            });
        }
    }
* await this.$store.dispatch('setNum', { number: 611 });  <!-- 使用方法 -->
#### module 拆分store