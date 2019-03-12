
---
layout: post
title: " 第三百九十节，Django+Xadmin打造上线标准的在线教育平台—Django+cropper插件头像裁剪上传 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**第三百九十节，Django+Xadmin打造上线标准的在线教育平台—Django+cropper插件头像裁剪上传**



****实现原理****

****前台用 **cropper插件
，将用户上传头像时裁剪图片的坐标和图片，传到逻辑处理函数里，在逻辑处理函数里接收原始图片进行保存，然后接收用户的裁剪坐标，利用python的Pillow模块图像处理模块里的PIL(图像库)，将原始图片根据用户裁剪坐标进行裁剪******

******有两个重点：****** ** ** **第一要准备好 **cropper头像裁剪插件，******** ** ** ** **第二 ** **
**python环境要安装好 ** ** **Pillow模块********************



********************htnl页面********************

********************编写htnl页面，引入 ** **
**cropper插件相关的css和js文件**************************

**************************注意：下面
红色背景的地方不要忘记设置，否则表单无法提交到后台**************************

[code]

    <!DOCTYPE html>
    <html lang="en">
    {% load staticfiles %} {# 启用静态文件引用#}
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <link href="{% static 'tou_xiang/bootstrap/css/bootstrap.min.css' %}" rel="stylesheet">
        <link href="{% static 'tou_xiang/font-awesome/css/font-awesome.min.css' %}" rel="stylesheet">
        <link href="{% static 'tou_xiang/cropper/cropper.min.css' %}" rel="stylesheet">
        <link href="{% static 'tou_xiang/sitelogo/sitelogo.css' %}" rel="stylesheet">
    </head>
    <body>
    {# 头像上传开始----------------------------------- #}
    {# 头像区块 #}
    <div class="ibox-content">
        <div class="row">
            <div id="crop-avatar" class="col-md-6">
                <div class="avatar-view" title="点击上传头像">
                    <img src="{{ MEDIA_URL }}{% for ch in ch_username %}{{ ch.image }}{% endfor %}"
                         data-am-popover="{content: '点击上传头像', trigger: 'hover focus'}">
                </div>
            </div>
        </div>
    </div>
    {# 上传弹出框 #}
    <div class="modal fade" id="avatar-modal" aria-hidden="true" aria-labelledby="avatar-modal-label" role="dialog"
         tabindex="-1">
        <div class="modal-dialog modal-lg">
            <div class="modal-content">
                <form class="avatar-form" action="{% url 'touxiang' %}" enctype="multipart/form-data" method="post">
                    <div class="modal-header">
                        <button class="close" data-dismiss="modal" type="button">&times;</button>
                        <h4 class="modal-title" id="avatar-modal-label">上传图片</h4>
                    </div>
                    <div class="modal-body">
                        <div class="avatar-body">
                            <div id="avatar-upload" class="avatar-upload">
                                <input class="avatar-src" name="avatar_src" type="hidden">
                                <input class="avatar-data" name="avatar_data" type="hidden">
                                <label for="avatarInput">
                                    <input class="avatar-input" id="avatarInput" name="avatar_file" type="file">
                                    <div class="tup btn btn-primary" dir="ltr">
                                        <span class="glyphicon glyphicon-cloud"></span>
                                        上传文件
                                    </div>
                                </label>
                            </div>
                            <div class="row">
                                <div class="col-md-9">
                                    <div class="avatar-wrapper"></div>
                                </div>
                                <div class="col-md-3">
                                    <div class="avatar-preview preview-lg"></div>
                                    {#<div class="avatar-preview preview-md"></div>#}
                                    {#<div class="avatar-preview preview-sm"></div>#}
                                </div>
                            </div>
                            <div class="row avatar-btns">
                                <div class="col-md-4">
                                    <div class="btn-group">
                                        <button class="btn btn-primary" data-method="rotate" data-option="-90" type="button"
                                                title="Rotate -90 degrees"><i class="fa fa-undo"></i> 向左旋转
                                        </button>
                                    </div>
                                    <div class="btn-group">
                                        <button class="btn btn-primary" data-method="rotate" data-option="90" type="button"
                                                title="Rotate 90 degrees"><i class="fa fa-repeat"></i> 向右旋转
                                        </button>
                                    </div>
                                </div>
                                <div class="col-md-5" style="text-align: right;">
                                    <button class="btn btn-primary fa fa-arrows" data-method="setDragMode" data-option="move"
                                            type="button" title="移动">
                                    </button>
                                    <button type="button" class="btn btn-primary fa fa-search-plus" data-method="zoom"
                                            data-option="0.1" title="放大图片">
                                    </button>
                                    <button type="button" class="btn btn-primary fa fa-search-minus" data-method="zoom"
                                            data-option="-0.1" title="缩小图片">
                                    </button>
                                    <button type="button" class="btn btn-primary fa fa-refresh" data-method="reset"
                                            title="重置图片">
                                    </button>
                                </div>
                                <div class="col-md-3">
                                    <button id="txiangform" class="btn btn-primary btn-block avatar-save" type="submit">
                                        <i class="fa fa-save"></i> 保存修改
                                    </button>
                                </div>
                            </div>
                        </div>
                    </div>
                {% csrf_token %}
                </form>
            </div>
        </div>
    </div>
    {# 头像上传结束------------------------------------- #}
    <script src="{% static 'tou_xiang/jquery.min.js' %}"></script>
    <script src="{% static 'tou_xiang/bootstrap/js/bootstrap.min.js' %}"></script>
    <script src="{% static 'tou_xiang/cropper/cropper.min.js' %}"></script>
    <script src="{% static 'tou_xiang/sitelogo/sitelogo.js' %}"></script>
    </body>
    </html>
[/code]

**效果图**

**![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170922091321931-1012627667.png)**





**专门给上传头像配置一个url路由映射**

[code]

    urlpatterns = [
    
        url(r 'usercenter_info.html', usercenter_info.as_view(), name='usercenter_info'),
    
        # 上传头像
        url(r'touxiang/', touxiang.as_view(), name='touxiang')
    
    ]
[/code]





**forms.py文件编写头像表单验证**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    from django import forms                             # 导入Django的表单验证模块
    from app_users.models import Users       # 导入数据库表类
    
    
    class touxiangForm(forms.Form):
        avatar_file = forms.ImageField()
[/code]





**views.py编写逻辑**

[code]

     import json
    from django.shortcuts import render, HttpResponse, redirect  # 导入django向浏览器返回方法
    from django.views.generic.base import Viewfrom pure_pagination import Paginator, EmptyPage, PageNotAnInteger
    
    from app_organization.models import CityDict, CourseOrg  # 数据库表
    from app_users.models import Users
    from app_organization.forms import touxiangForm
    from utils.uploadfile import Uploadfile
    
    
    class touxiang(View):
        def post(self, request):
            usern = request.session.get("username")                 # 获取用户登录名称
            us = Users.objects.filter(username=usern)               # 到数据库查找用户
            yanzh = touxiangForm(request.POST, request.FILES)       # 验证表单
            if yanzh.is_valid():                                    # 表单验证通过
                erf = request.FILES['avatar_file']                  # 获取上传图片
                jetu = request.POST['avatar_data']
                # 将上传图片传入一个自定义函数里裁剪，返回图片路径
                fanhui = Uploadfile('image', erf, jetu)
    
                us.update(image=fanhui)                             # 将图片路径修改到当前会员数据库
                # 向前台返回一个json，result值是图片路径
                return HttpResponse(json.dumps({'result': '/media/' + fanhui}))
            else:
                return HttpResponse("验证失败")
[/code]





**编写Uploadfile截图函数**

[code]

     #!/usr/bin/env python
    # -*- coding:utf8 -*-
    import os
    import time
    import random                                                   # 引入随机模块文件
    import re
    import json
    
    from PIL import Image
    
    from MxOnline.settings import MEDIA_ROOT                        # 导入配置文件里的上传资源路径
    
    
    def Uploadfile(mu_lu, wen_jian, jetu):
        """
        第一参数，上传头像数据库models里指定的目录名称【字符串类型】
        第二参数，接收文件上传对象inMemoryUploadedFile对象【inMemoryUploadedFile对象】
        第三参数，接收头像要截图的坐标，x.y.width.height【json类型】
        裁剪成功返回图片路径
        """
        if not MEDIA_ROOT:
            return '请在settings.py配置上传文件目录'
    
        try:
            nian_yue = time.strftime('%Y/%m/')
            pj_mu_lu = os.path.abspath(os.path.join(MEDIA_ROOT, mu_lu, nian_yue))                           # 拼接上传路径
            pd_mu_lu = os.path.exists(pj_mu_lu)
            if pd_mu_lu:                                                                                    # 判断上传目录是否存在
                pass
            else:
                os.makedirs(pj_mu_lu)                                                                       # 创建上传目录
    
            # 接收文件上传对象inMemoryUploadedFile对象
            wenjian = wen_jian
            name = wenjian.name                                                                             # 获取文件名称
            size = wenjian.size                                                                             # 文件大小(字节)
    
            # 调用随机函数(随机数开始范围,随机数结束范围)
            f1 = str(random.randrange(1, 99999999))
            f2 = str(time.strftime('%Y%m%d%H%M%S'))
            f3 = str(f2 + f1)
            houzh = re.findall('.*\.(.*)', name)[0]
            wj_name = f3 + '.' + houzh
            xie_ru_lu_jing = pj_mu_lu + '/' + wj_name
            # print(xie_ru_lu_jing)
    
            # 以读写字节模式打开，存在覆盖没有创建
            gshi = 'BMP,PNG,GIF,JPG,JPEG'
            pd_gshi = re.findall(houzh.upper(), gshi)
            if pd_gshi:
                xieru = open(xie_ru_lu_jing, 'wb')
                for chunk in wenjian.chunks():                                                  # 循环文件数据块
                    xieru.write(chunk)                                                          # 写入文件
                xieru.close()                                                                   # 关闭
            else:
                return '上传的不是图片文件'
    
            # 判断文件是否写入成功返回布尔值
            pd_xieru = os.path.exists(xie_ru_lu_jing)
    
            if pd_xieru:
    
                # 开始根据前台提供的坐标截图
                zuo_biao = json.loads(jetu)
    
                # 获取坐标
                t_x = int(zuo_biao['x'])
                t_y = int(zuo_biao['y'])
                t_width = t_x + int(zuo_biao['width'])
                t_height = t_y + int(zuo_biao['height'])
    
                # 打开要截图的图片
                im = Image.open(xie_ru_lu_jing)
                # print(xie_ru_lu_jing)
                # 裁剪图片,裁剪尺寸为200*200，可以在resize()设置
                crop_im = im.convert("RGBA").crop((t_x, t_y, t_width, t_height)).resize((200, 200), Image.ANTIALIAS)
    
                # 设置背景颜色为白色
                out = Image.new('RGBA', crop_im.size, (255, 255, 255))
                out.paste(crop_im, (0, 0, 200, 200), crop_im)
    
                # 保存图片
                crop_im.save(xie_ru_lu_jing)
    
                # 返回图片路径，从第一个参数目录开始的
                wj_lj = mu_lu + '/' + nian_yue + wj_name
                return wj_lj
    
        except Exception as e:
            return e
[/code]



**最终效果**

**![](https://images2017.cnblogs.com/blog/955761/201709/955761-20170922094603525-1589165139.png)**



