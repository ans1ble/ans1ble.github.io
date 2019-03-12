
---
layout: post
title: " 第三百九十六节，Django+Xadmin打造上线标准的在线教育平台—其他插件使用说，自定义列表页上传插件 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**第三百九十六节，Django+Xadmin打造上线标准的在线教育平台—其他插件使用说，自定义列表页上传插件**



**设置后台列表页面字段统计**

**在当前APP里的adminx.py文件里的数据表管理器里设置**

**aggregate_fields = {'字段名称':'sum为统计数，min为统计时间'}**

[code]

     class CourseAdmin(object):               # 自定义数据表管理器类
    
        # 设置xadmin后台显示字段
        list_display = ['name', 'desc', 'detail', 'degree', 'learn_times', 'students',
                        'fav_nums', 'image', 'click_nums', 'add_time']
    
        # 设置xadmin后台搜索字段，注意：搜索字段如果有时间类型会报错
        search_fields = ['name', 'desc', 'detail', 'degree', 'learn_times', 'students',
                         'fav_nums', 'image', 'click_nums']
    
        # 设置xadmin后台过滤器帅选字段，时间用过滤器来做
        list_filter = ['name', 'desc', 'detail', 'degree', 'learn_times', 'students',
                       'fav_nums', 'image', 'click_nums', 'add_time']
        model_icon = 'fa fa-clone'
        style_fields = {'detail':'ueditor'}
        # import_excel = True
        aggregate_fields = {'fav_nums':'sum'}
    
    xadmin.site.register(Course, CourseAdmin)     # 将数据表注册到xadmin后台显示
[/code]

![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170925173946214-1653676581.png)





**自定义列表页上传插件**

**![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170929133629419-880085366.png)**

**![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170929133934747-263348416.png)**



**注册插件APP**

[code]

    INSTALLED_APPS = [
         'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        'app_users',                        # 注册 APP
        'app_courses',
        'app_organization',
        'app_operation',
        'xadmin',                           # 注册xadmin的app
        'reversion',
        'crispy_forms',                     # 注册xadmin的依赖app
        'captcha',                          # 注册验证码app
        'pure_pagination',                  # 注册分页app
        'DjangoUeditor',                    # 注册DjangoUeditor的APP
        'wen_jian_shang_chuanpy',           # 注册上传插件app
    ]
[/code]



**配置插件上传URL路由逻辑**

[code]

     from extra_apps.wen_jian_shang_chuanpy.shang_chuan_wen_jian import Shang_chuan_wen_jian
    urlpatterns = [
        url(r'^xadmin/', xadmin.site.urls),
    
        url(r'^index.html', TemplateView.as_view(template_name='index.html'), name='index'),
    
        # 注册
        url(r'^register.html', zhu_ce.as_view(), name='register'),
        url(r'^captcha/', include('captcha.urls'), name='captcha'),
        url(r'^active/(?P<active_de>.*)/$', active_code.as_view(), name="user_active"),
    
        # 登录
        url(r'^login.html', TemplateView.as_view(template_name='login.html'), name='login'),
        url(r'^deng_lu', deng_lu.as_view(), name='deng_lu'),
        url(r'^logout', logout.as_view(), name='deng_lu'),
    
        # 授课机构
        url(r'^org_list.html', org_list.as_view(), name='org_list'),
    
        # 专门处理静态资源请求映射，也就是media上传文件夹里的请求映射
        url(r'media/(?P<path>.*)$', serve, {'document_root': MEDIA_ROOT}),
    
        # 配置静态文件访问
        # url(r'static/(?P<path>.*)$', serve, {'document_root': STATIC_ROOT}),
    
        url(r'course_comment.html', course_comment.as_view(), name='course_comment'),
        url(r'usercenter_info.html', usercenter_info.as_view(), name='usercenter_info'),
    
        # 上传头像
        url(r'touxiang/', touxiang.as_view(), name='touxiang'),
    
        # 配置DjangoUeditor富文本路由映射
        url(r'^ueditor/', include('DjangoUeditor.urls')),
    
        # 配置后台上传映射
        url(r'^shang_chuan_wen_jian/', Shang_chuan_wen_jian, name='Shang_chuan_wen_jian'),
    ]
[/code]



**models.py里 **要上传文件** 的类里自定义函数，函数里执行插件里的一个函数**

[code]

    class CourseResource(models.Model):
        course = models.ForeignKey(Course, verbose_name='外键课程表')
        name = models.CharField(max_length=100, verbose_name='课程资源名称')
        download = models.FileField(upload_to='course/resource/%Y/%m', storage=ImageStorage(), verbose_name='资源文件', max_length=100)
        add_time = models.DateTimeField(default=datetime.now, verbose_name='添加日期')
    
        class Meta:
            verbose_name = '课程资源表'
            verbose_name_plural = verbose_name
    
            # 自定义列
    
        def xiougai(self):
            from extra_apps.wen_jian_shang_chuanpy.shang_chuan_wen_jian import book_hanshu
            book = book_hanshu(self.download, self.id, 'app_courses', 'CourseResource', 'download')
            return book  # 返回HTML显示到页面
        xiougai.short_description = '修改文件'
    
        def __str__(self):
            return self.name
[/code]



**adminx.py里开启插件**

[code]

     class CourseResourceAdmin(object):
        list_display = ['course', 'name', 'download', 'add_time', 'xiougai']
        search_fields = ['course', 'name', 'download']
        list_filter = ['course', 'name', 'download', 'add_time']
        model_icon = 'fa fa-hdd-o'
        # list_editable = ['download']
        # show_detail_fields = ['download']
        shang_chuan_wen_jian = True
    
    xadmin.site.register(CourseResource, CourseResourceAdmin)
[/code]



**插件文件shang_chuan_wen_jian.py**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    import json
    from django.shortcuts import render, HttpResponse, redirect
    from django.views.decorators.csrf import csrf_exempt,csrf_protect
    from django.utils.safestring import mark_safe                       # 允许执行html代码
    
    from xadmin.sites import site
    from xadmin.views import BaseAdminPlugin, ListAdminView, CommAdminView, ModelAdminView
    
    from MxOnline import settings
    from apps.utils.uploadfile import Uploadfile
    
    
    def book_hanshu(download, id, app, models_biao, ziduan):
        """
        :第一个参数，接收上传数据字段的数据库数据
        :第二个参数，接收上传数据字段的数据库数据id
        :第三个参数，接收当前的APP名称
        :第四个参数，接收当前数据表的类名
        :第五个参数，接收，当前上传字段名称
        :return:
        """
        book = """
        <div class="modal fade" id="myModal">
            <div class="modal-dialog">
                <div class="modal-content">
                    <div class="modal-header">
                        <button type="button" class="close" data-dismiss="modal">
                            <span>&times;</span></button>
                        <h4 class="modal-title">上传文件</h4></div>
                    <div class="modal-body">
                        <form method="post" enctype="multipart/form-data">
                            <div id="yuan_shi" class="alert alert-success"></div>
                            <div id="tishi" class="alert alert-success">请选择您要上传的文件</div>
                            <input id="file" class="btn btn-default" type="file" name="file"/>
                            <input id='app' value="" type="hidden" name="app"/>
                            <input id='models_biao' value="" type="hidden" name="models_biao"/>
                            <input id='n_id' value="" type="hidden" name="n_id"/>
                            <input id='ziduan' value="" type="hidden" name="ziduan"/>
                            <span id="daxiao"></span><br/>
                            <span id="daxiao2"></span><br/>
                            <div id="jdt" class="progress">
                                <div id="prog" class="progress-bar" style="min-width:20px; width: 0%;">0%</div>
                            </div>
                        </form>
                    </div>
                    <div class="modal-footer">
                        <button id="shch_anllou" type="button" class="btn btn-primary">
                            上传文件
                        </button>
                    </div>
                </div>
            </div>
        </div>
        <!--data-toggle="modal"声明事件切换类型，modal表示模态框类型(Bootstrap)-->
        <!--data-target="#myModal">声明事件操作对象，#myModal表示点击后关闭id为#myModal的元素(Bootstrap)-->
        <span></span>
        <button n_nr="{download}" n_id='{n_id}' app='{app}' models_biao='{models_biao}' ziduan='{ziduan}' class="btn btn-primary btn-xs xiou_gai" data-toggle="modal" data-target="#myModal">
            点击修改
        </button>
        """.format(download=download, n_id=id, app=app, models_biao=models_biao, ziduan=ziduan)
        return mark_safe(book)
    
    # 上传逻辑
    @csrf_exempt
    def Shang_chuan_wen_jian(request):
        if request.method == "POST":
            file = request.FILES.get('file')                    # 获取上传文件对象
            xieru_wjian = Uploadfile('course/resource',file)
    
            app = request.POST.get('app')                       # 获取前台传过来的APP名称
            models_biao = request.POST.get('models_biao')       # 获取前台传过来的数据表名称
            n_id = request.POST.get('n_id')                     # 获取前台传过来的数据id
            ziduan = request.POST.get('ziduan')                 # 获取要修改的字段
    
            # 动态导入数据库模块
            orm = __import__('{0}.models'.format(app),models_biao,fromlist=True)
            pd_models_biao = hasattr(orm,models_biao)           # 判断当前数据表是否存在
            if pd_models_biao and xieru_wjian:
                hq_models_biao = getattr(orm,models_biao)       # 如果存在，找到数据表类
                xieru = {ziduan:xieru_wjian}
                biao = hq_models_biao.objects.filter(id=n_id).update(**xieru)
                if biao:
                    return HttpResponse(json.dumps({'url':xieru_wjian}))
            else:
                return HttpResponse('数据表不存在')
    
        return HttpResponse('')
    
    
    class EditablePlugin(BaseAdminPlugin):
        shang_chuan_wen_jian = False
    
        def init_request(self, *args, **kwargs):
            return bool(self.shang_chuan_wen_jian)
    
        # 在网页头部注入js[列表页，内容页]
        def block_extrahead(self, context, nodes):
            js = '<script type="text/javascript" src="{0}"></script>'.format(settings.STATIC_URL + 'shang_chuan_wen_jian.js')
            # js += '<script type="text/javascript" src="{0}"></script>'.format(settings.STATIC_URL + 'jquery.form.js')
            nodes.append(js)
    
    
    site.register_plugin(EditablePlugin, ListAdminView)         # 列表逻辑
[/code]



**js文件**

[code]

     /**
     * Created by admin on 2017/9/26.
     */
    jQuery(function ($) {
    
        var totalSize = 0;
    
    
        //初始化隐藏进度条
        $('#jdt').hide();
    
        //绑定所有type=file的元素的onchange事件的处理函数
        //当选定文件时触发函数
        $(':file').change(function () {
            var file = this.files[0]; //假设file标签没打开multiple属性，那么只取第一个文件就行了
            name = file.name;
            size = file.size;
            type = file.type;
            url = window.URL.createObjectURL(file); //获取本地文件的url，如果是图片文件，可用于预览图片
    
            //$(this).next().html("文件名：" + name + " 文件类型：" + type + " 文件大小：" + size + " url: " + url);
    
            totalSize += size;//字节
            var mb = parseInt(totalSize / 1024 / 1024);
            $("#daxiao").html("总大小: " + totalSize + "-字节");
            $("#daxiao2").html("总大小: " + mb + "-mb");
    
        });
    
    
        //点击修改按钮时触发函数
        $('.xiou_gai').click(function () {
            //获取需要传递到后台的参数
            var n_nr = $(this).attr('n_nr');
            var n_id = $(this).attr('n_id');
            var app = $(this).attr('app');
            var models_biao = $(this).attr('models_biao');
            var ziduan = $(this).attr('ziduan');
            //将参数填充到表单以便提交后台
            $('#yuan_shi').text('原始文件：' + n_nr);
            $('#n_id').val(n_id);
            $('#app').val(app);
            $('#models_biao').val(models_biao);
            $('#ziduan').val(ziduan);
        });
    
    
        //向表单区域添加一个form标签
        $('#myModal').wrap('<form id="form" method="post" enctype="multipart/form-data">');
        $('#form').wrap('<div id="form_zhuti">');
    
    
        //点击上传按钮后触发函数
        $('#shch_anllou').click(function () {
            var file_zhi = $('#file').val();
            if (file_zhi){
                upload()
            }else {
                $('#tishi').attr('class','alert alert-danger')
            }
    
        });
    
    
        //点击选择框后恢复提示框颜色
        $('#file').click(function () {
            $('#tishi').attr('class','alert alert-success');
            $('#tishi').text('请选择您要上传的文件')
        });
    
    
        //ajax提交函数
        function upload() {
            //创建FormData对象，初始化为form表单中的数据。需要添加其他数据可使用formData.append("property", "value");
            var formData = new FormData($('#form_zhuti form')[0]);
            $('#jdt').show();
            $.ajax({
                url: "/shang_chuan_wen_jian/",
                type: "POST",
                data: formData,
                dataType: 'json',
                //获取ajaxSettings中的xhr对象，为它的upload属性绑定progress事件的处理函数
                xhr: function () {
                    myXhr = $.ajaxSettings.xhr();
                    //检查upload属性是否存在
                    if (myXhr.upload) {
                        //绑定progress事件的回调函数
                        myXhr.upload.addEventListener('progress', progressHandlingFunction, false);
                    }
                    return myXhr; //xhr对象返回给jQuery使用
                },
                success: function (result) {
                    //返回json格式，里面是上传成功后的URL
                    // alert(result.url);
                    $('#yuan_shi').text(result.url);
                    $('#tishi').text('恭喜上传成功！');
                    $('#tishi').attr('class','alert alert-info');
                    $('#tishi').attr({'style':'font-size:20px;font-weight:bold;'});
    
                    //睡眠
                    setTimeout(function () {
                        // window.location.reload();   //刷新浏览器
                        top.location.reload();   //刷新页面
                    }, 2000);
    
                },
                contentType: false,  //必须false才会自动加上正确的Content-Type
                processData: false,  //必须false才会避开jQuery对 formdata 的默认处理
                error:function (xhr, status, info){
                    $('#tishi').attr('class','alert alert-danger');
                    $('#tishi').text('遗憾上传出错了')
                }
            });
        }
    
    
        //上传进度回调函数：
        function progressHandlingFunction(e) {
            if (e.lengthComputable) {
                var percent = e.loaded / e.total * 100;
                var bfbi = percent.toFixed(2) + "%";
                $('#prog').attr("style", 'width:' + bfbi); //更新数据到进度条
                $('#prog').html(bfbi);
                // $('#daxiao3').html(e.loaded + "/" + e.total+" bytes. " + percent.toFixed(2) + "%");
            }
        }
    
    
        //当上传框关闭后触发
        $('#myModal').on('hide.bs.modal', function () {
            //当模态框关闭是清空表单和参数
            $('#yuan_shi').text('');
            $('#n_id').val('');
            $('#app').val('');
            $('#models_biao').val('');
            $('#file').val('');
            $('#daxiao').text('');
            $('#daxiao2').text('');
            $('#jdt').hide();
            $('#prog').attr("style", {'width': 0}); //更新数据到进度条
            $('#prog').html(0);
            $('#tishi').attr('class','alert alert-success');
            $('#ziduan').val('');
        });
    
    
    
    
    
    });
[/code]



**最终效果**

**![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170929140229950-802863403.png)**



补充： **adminx.py 注册管理器，接收每次后台提交的请求，进行逻辑处理**

[code]

     # 录音作品
    class app_zuopinAdmin(object):
    
        # 设置xadmin后台显示字段
        list_display = ['id', 'title', 'psrc', 'lu_yin_shang_chuan', 'yangsrc', 'yamg_yin_shit', 'shen_chen_yang_yin']
    
        # 设置xadmin后台搜索字段，注意：搜索字段如果有时间类型会报错
        search_fields = ['id', 'title', 'des', 'key', 'psrc']
    
        # # 设置xadmin后台过滤器帅选字段，时间用过滤器来做
        list_filter = ['title', 'des', 'key', 'xing_bie', 'yu_zhong', 'ti_cai', 'shi_jian']
        
        def post(self, request, *args, **kwargs):
       
            逻辑处理  
      
    
            # 一定要这样返回，否则会出错
            return super(app_zuopinAdmin, self).post(request, *args, **kwargs)
    
    # 管理器重写后重新注册
    xadmin.site.register(Zuopin, app_zuopinAdmin)
[/code]



