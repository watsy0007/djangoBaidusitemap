djangoBaidusitemap
==================

django动态生成百度地图。大体使用方法与django自带googlesitemap相同。  

使用方法  
1.下载导入工程  
2.在setting配置INSTALLED_APPS中加入'baidusitemap',  
3.新建1个bdsitemap.py文件，示例代码如下  
    
    #coding: utf-8
    __author__ = 'watsy'

    from django.contrib.sitemaps import Sitemap
    from models import *
    from django.db.models import Sum
    from baidusitemap import BaiduSitemap

    class ZnanrenSitemaps(BaiduSitemap):
        changefreq = 'daily'
        priority = 0.5

        def items(self):
            return News.objects.all()


        def lastmod(self , obj):
            if obj.update_date:
                return obj.update_date
            return obj.created_date
            
            
        def html5_url(self, obj):
        
            return '/html5_demo/'


        def wml_url(self, obj):
        
            return '/wml_url_demo/'
            
            
        def xhtml_url(self, obj):
        
            return 'xhtml_url_demo'

4.urls.py中添加url解析支持  

    from sitemapsClass import ZnanrenSitemaps
    sitemaps = {
        'static' : ZnanrenSitemaps
    }
    ....
    (r'^bdsitemap\.xml$','baidusitemap.views.sitemap',{'sitemaps': sitemaps}),

5.浏览器中打开http://127.0.0.1:8000/bdsitemap.xml查看效果  
