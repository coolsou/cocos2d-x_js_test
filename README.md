#vega.常量

* winSize
```
= {width:640 height:960}
```

* winWidthHalf
```
= winSize.width/2
```
* winHeightHalf
```
= winSize.height/2
```
* director
```
= cc.Director.getInstance()
```


#vega.常用方法

* require(path)
```
path : 'src/view/connecting.js' ||  'view_connecting'
```

* define(moduleName, dependents, callbackToExports)
```
定义模块
~ 可避免污染全局变量
~ 自动加载依赖的模块
```
`例 src/view/layer/example_module.js`


* routeTo(nextDoWhat, tasksToExcute)
```
~ 执行tasksToExcute的同时，调用当前场景的退出动作
~ 当以上两个动作全部完成后，执行nextDoWhat
nextDoWhat : function
tasksToExcute : function(callbackOfAsync)
```

* addObj(obj,tag)
```
添加tag为boj的索引
obj: anything
tag: string
```
* getObj(tag)
```
添加tag为boj的索引
```
* removeSelf()  tryRemoveSelf()
```
从view中删除自己（请注意是否会自动移除相关事件）
```
* getRect(obj)
```
= (cc.rect) {x,y,width,height}
```
* atCenter(parent,child,args)
```
将child置于parent的中心
：可选 args = {x:10,y:10} 偏移
```
* alignTo(parent,child,args)
```
将child置于parent中
：可选 args = {
	x:10,y:10 //偏移
    to: 'right' || 'left' || 'top' || 'bottom' || 'center'
    }
```

* replaceScene(scene,cb)
```
替换场景
```

* trace()
```
打印函数执行位置（测试中）
需要在函数定位的位置写 var a = function()//___这里会打印出来___
```

* removeFromArray(array,obj)
```
从array中删除obj
```

* debug(str1,str2)
```
打印log
str1为tag或内容，会包含在[]中
: str2为内容
```

* json2str(json)
```
JSON.stringify
```

* str2json()
```
JSON.parse
```

* addToBase(str,zorder)
```
1 移除baseLayer上的所有view
2 添加eval(str)到baseLayer上
```

* assert(boolean,str)
```
如果boolean！==true
停止运行并打印str（有可能log太多，需要往上翻屏才能看到）
```

* addBlankLayer(parent)
```
添加一个空白layer在parent上
= this(blankLayer)
```



#vega.dict

* get(key)
* getKeys()
* hasKey(key)
* set(key,value)
* count
* delete
* clear(key)
* sortBy(keyOfItem)
* filterData(filter)


#vega.subpub
`对象内，对象间事件监听`
* on(eventName, callBack, obj=this)
```
注册监听方法和回调
当this.trigger(eventName)发生时，所有注册过的callBack会依次调用（注册顺序）
```

* off(eventName,callBack,obj=this)
```
删除监听对象和方法
```

* trigger(eventName,extra)
```
通知所有注册到this的eventName上的对象方法，附带extra作为执行参数
```

* lisenTo(obj, eventName, callBack)
```
当前对象监听 obj 的 eventName
当obj.trigger(eventName,extra?)时，this.callBack(extra)会被调用
```

* stopLisenTo(obj, eventName, callBack)
```
停止监听obj对象上的eventName事件的callBack方法
：callBack 为空时，删除自己所有注册到obj上的eventName 上的方法
：eventName 为空时，删除自己所有注册到obj上的监听方法
```

* removeSPOfSelf()
```
删除所有与自身有关的监听事件
```

* removeSPbyEvent(eventName)
```
删除自己的eventName事件
```


#vega.event
`全局事件监听`
* subscribe || sub || bind (eventName, obj, data)
```
将obj注册到eventName上
当eventName发生时（ vega.event.trigger(eventName,extra) ）
obj会被触发 ( obj['on_'+eventName](extra) )
```
* publish || pub || trigger (eventName, data)
```
触发 eventName
```
* fire(eventName, obj)
```
从 eventName 上删除 obj
```
* fireAll(eventName)
```
从 eventName 上删除 所有监听对象
```


#vega_layer
`例 src/view/layer/example.js`
```
需要继承 vega_layer
~ 可以实现屏蔽其他层的触摸事件
~ 通过 this.add_Child(obj)添加的obj对象，可以绑定 obj.onClick onDrag onDragEnd 方法
```


#vega_model
`例 src/mod/user_example.js`
```
需要继承 vega_model
~ 默认具备 vega.subpub 属性
```


#功能模块切换
```
建议主要进行layer层切换，速度快，资源需要手动释放
scene的切换耗时较长，场景过渡的效果现在还没处理
```



