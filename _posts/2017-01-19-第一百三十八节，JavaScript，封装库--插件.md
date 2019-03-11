第一百三十八节，JavaScript，封装库--插件

**JavaScript，封装库--插件**

**库主要是用来封装一般JavaScript的常规操作代码，而拖拽这种特效代码属于功能性代码，并不是必须的，所以这种类型的代码，我们建议另外封装，在需要的时候作为插件形式引入到库中，作为扩展。**



**在基础库设置一个extend()方法，来扩展插件**

    
    
     /** 插件入口，简单的理解就是通过extend()方法，向此基础库添加一个原型方法
     *  此extend()方法，一般是给插件文件使用的，插件就是通过extend()方法，将插件方法添加到基础库原型的
     *  接收两个参数
     *  参数1是传入要添加的方法名称
     *  参数2是此方法的执行函数（包含代码）
     **/
    feng_zhuang_ku.prototype.extend = function (name,fn) {
        feng_zhuang_ku.prototype[name] = fn;
    };



**插件扩展方式，如:拖拽为列**

    
    
     /** tuo_zhuai()方法，将一个弹窗元素实现拖拽功能
     * 注意：有参设置拖拽点区块，只有弹窗的这个拖拽点区块才能拖拽，无参整个弹窗可以拖拽
     * 注意：一般需要在css文件将弹窗元素里的某一个区块光标设置成提示可以拖拽，如：cursor: move; （设置拖拽点）
     * 有一个参数，参数是弹窗元素里的拖拽点区块的字符串class值（设置拖拽点的class值）设置后弹窗元素里的这个拖拽点区块才能拖拽
     **/
    //调用基础库extend()方法，创建基础库原型tuo_zhuai()方法
    $().extend('tuo_zhuai', function (tuo_zhuai_dian) {
        if (this.jie_dian.length == 1) {
            var yan_su = null;
            var sum = arguments.length;
            for (var i = 0; i < this.jie_dian.length; i++) {
                yan_su = this.jie_dian[i];
            }
            addEvent(yan_su, 'mousedown', function (e) {
                if (trim(yan_su.innerHTML).length == 0)e.preventDefault();
                var e1 = getEvent(e);  //getEvent()函数库函数，跨浏览器获取事件对象,事件event对象,
                var diffx = e1.clientX - yan_su.offsetLeft;
                var diffy = e1.clientY - yan_su.offsetTop;
                if (sum == 1) {
                    if (e.target.className === tuo_zhuai_dian) {
                        addEvent(document, 'mousemove', move);
                        addEvent(document, 'mouseup', up);
                    }
                } else if (sum == 0) {
                    addEvent(document, 'mousemove', move);
                    addEvent(document, 'mouseup', up);
                }
                function move(e) {
                    var e2 = getEvent(e);
                    var left = e2.clientX - diffx;
                    var top = e2.clientY - diffy;
                    if (left < 0) {
                        left = 0;
                    } else if (left > getInner().width - yan_su.offsetWidth) {
                        left = getInner().width - yan_su.offsetWidth;
                    }
                    if (top < 0) {
                        top = 0;
                    } else if (top > getInner().height - yan_su.offsetHeight) {
                        top = getInner().height - yan_su.offsetHeight;
                    }
                    yan_su.style.left = left + 'px';
                    yan_su.style.top = top + 'px';
                    if (typeof yan_su.setCapture != 'undefined') {
                        yan_su.setCapture();
                    }
                }
    
                function up() {
                    removeEvent(document, 'mousemove', move);
                    removeEvent(document, 'mouseup', up);
                    if (typeof yan_su.releaseCapture != 'undefined') {
                        yan_su.releaseCapture();
                    }
                }
            });
        } else {
            alert("将一个弹窗元素实现拖拽功能,只能设置一个弹窗元素，目前jie_dian数组里是多个元素请检查！")
        }
        return this;
    });



**插件说明**

    
    
    **/**------------------------------------------------插件说明--------------------------------------------**/**  
     **/** 插件是通过基础库的extend()方法，向基础库原型添加的插件方法**  
     ***  前台使用说明：**  
     ***  1.获取到目标对象，执行插件方法，如：$().huo_qu_id('login');**  
     ***  2.页面引入插件js文件，如： <script type="text/javascript" src="feng_zhuang_ku/cha_jian/tuo_zhuai.js" charset="utf-8"></script>**  
     ****/**  
     **/**------------------------------------------------插件说明--------------------------------------------**/**  
     **tuo_zhuai()方法，将一个弹窗元素实现拖拽功能**

