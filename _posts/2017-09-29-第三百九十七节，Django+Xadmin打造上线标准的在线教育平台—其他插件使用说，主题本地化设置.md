
---
layout: post
title: " 第三百九十七节，Django+Xadmin打造上线标准的在线教育平台—其他插件使用说，主题本地化设置 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**第三百九十七节，Django+Xadmin打造上线标准的在线教育平台—其他插件使用说，主题本地化设置**



**主题设置是在xadmin\plugins\themes.py这个文件**

**默认xadmin是通过下面这个json文件来动态加载的。所以我们可以到它加载的 **json文件里下载好主题****

******themes.py** 修改方式****



[code]

    #coding:utf-8
    from __future__ import print_function
    import httplib2
    from django.template import loader
    from django.core.cache import cache
    from django.utils import six
    from django.utils.translation import ugettext as _
    from xadmin.sites import site
    from xadmin.models import UserSettings
    from xadmin.views import BaseAdminPlugin, BaseAdminView
    from xadmin.util import static, json
    import six
    if six.PY2:
        import urllib
    else:
        import urllib.parse
    
    THEME_CACHE_KEY = 'xadmin_themes'
    
    
    class ThemePlugin(BaseAdminPlugin):
    
        enable_themes = False
        # {'name': 'Blank Theme', 'description': '...', 'css': 'http://...', 'thumbnail': '...'}
        user_themes = None
        use_bootswatch = False
        default_theme = static('xadmin/css/themes/bootstrap-xadmin.css')
        bootstrap2_theme = static('xadmin/css/themes/bootstrap-theme.css')
    
        # 将主题本地化，下载好主题设置下载好的主题样式文件
        Solar_theme = static("xadmin/css/themes/Solar_theme.css")
        Cerulean_theme = static("xadmin/css/themes/Cerulean_theme.css")
        Cosmo_theme = static("xadmin/css/themes/Cosmo_theme.css")
        Cyborg_theme = static("xadmin/css/themes/Cyborg_theme.css")
        Darkly_theme = static("xadmin/css/themes/Darkly_theme.css")
        Flatly_theme = static("xadmin/css/themes/Flatly_theme.css")
        Journal_theme = static("xadmin/css/themes/Journal_theme.css")
        Lumen_theme = static("xadmin/css/themes/Lumen_theme.css")
        Paper_theme = static("xadmin/css/themes/Paper_theme.css")
        Readable_theme = static("xadmin/css/themes/Readable_theme.css")
        Sandstone_theme = static("xadmin/css/themes/Sandstone_theme.css")
        Simplex_theme = static("xadmin/css/themes/Simplex_theme.css")
        Slate_theme = static("xadmin/css/themes/Slate_theme.css")
        Spacelab_theme = static("xadmin/css/themes/Spacelab_theme.css")
        Superhero_theme = static("xadmin/css/themes/Superhero_theme.css")
        United_theme = static("xadmin/css/themes/United_theme.css")
    
    
        def init_request(self, *args, **kwargs):
            return self.enable_themes
    
        def _get_theme(self):
            if self.user:
                try:
                    return UserSettings.objects.get(user=self.user, key="site-theme").value
                except Exception:
                    pass
            if '_theme' in self.request.COOKIES:
                if six.PY2:
                    func = urllib.unquote
                else:
                    func = urllib.parse.unquote
                return func(self.request.COOKIES['_theme'])
            return self.default_theme
    
        def get_context(self, context):
            context['site_theme'] = self._get_theme()
            return context
    
        # Media
        def get_media(self, media):
            return media + self.vendor('jquery-ui-effect.js', 'xadmin.plugin.themes.js')
    
        # Block Views
        def block_top_navmenu(self, context, nodes):
    
            themes = [
                {'name': _(u"Default"), 'description': _(u"Default bootstrap theme"), 'css': self.default_theme},
                # {'name': _(u"Bootstrap2"), 'description': _(u"Bootstrap 2.x theme"), 'css': self.bootstrap2_theme},
    
                # 设置主题静态加载样式
                {'name': _(u"深绿"), 'description': _(u"深绿"), 'css': self.Solar_theme},
                {'name': _(u"天蓝"), 'description': _(u"天蓝"), 'css': self.Cerulean_theme},
                {'name': _(u"蓝黑"), 'description': _(u"蓝黑"), 'css': self.Cosmo_theme},
                {'name': _(u"黑色"), 'description': _(u"黑色"), 'css': self.Cyborg_theme},
                {'name': _(u"绿黑"), 'description': _(u"绿黑"), 'css': self.Darkly_theme},
                {'name': _(u"绿蓝"), 'description': _(u"绿蓝"), 'css': self.Flatly_theme},
                {'name': _(u"粉红"), 'description': _(u"粉红"), 'css': self.Journal_theme},
                {'name': _(u"白色"), 'description': _(u"白色"), 'css': self.Lumen_theme},
                {'name': _(u"深蓝"), 'description': _(u"深蓝"), 'css': self.Paper_theme},
                {'name': _(u"白蓝"), 'description': _(u"白蓝"), 'css': self.Readable_theme},
                {'name': _(u"草绿"), 'description': _(u"草绿"), 'css': self.Sandstone_theme},
                {'name': _(u"红色"), 'description': _(u"红色"), 'css': self.Simplex_theme},
                {'name': _(u"灰黑"), 'description': _(u"灰黑"), 'css': self.Slate_theme},
                {'name': _(u"灰蓝"), 'description': _(u"灰蓝"), 'css': self.Spacelab_theme},
                {'name': _(u"深灰"), 'description': _(u"深灰"), 'css': self.Superhero_theme},
                {'name': _(u"橙色"), 'description': _(u"橙色"), 'css': self.United_theme},
                ]
    
            select_css = context.get('site_theme', self.default_theme)
    
            if self.user_themes:
                themes.extend(self.user_themes)
    
            if self.use_bootswatch:
                ex_themes = cache.get(THEME_CACHE_KEY)
                if ex_themes:
                    themes.extend(json.loads(ex_themes))
                else:
                    ex_themes = []
                    try:
                        pass
    
                        # 默认xadmin是通过下面这个json文件来动态加载的,将它注释掉将不会动态加载主题
    
                        # h = httplib2.Http()
                        # resp, content = h.request("https://bootswatch.com/api/3.json", 'GET', '',
                        #     headers={"Accept": "application/json", "User-Agent": self.request.META['HTTP_USER_AGENT']})
                        # if six.PY3:
                        #     content = content.decode()
                        # watch_themes = json.loads(content)['themes']
                        # ex_themes.extend([
                        #     {'name': t['name'], 'description': t['description'],
                        #         'css': t['cssMin'], 'thumbnail': t['thumbnail']}
                        #     for t in watch_themes])
                    except Exception as e:
                        print(e)
    
                    cache.set(THEME_CACHE_KEY, json.dumps(ex_themes), 24 * 3600)
                    themes.extend(ex_themes)
    
            nodes.append(loader.render_to_string('xadmin/blocks/comm.top.theme.html', {'themes': themes, 'select_css': select_css}))
    
    
    site.register_plugin(ThemePlugin, BaseAdminView)
[/code]



