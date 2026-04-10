# NexaPay 静态网站部署指南

## 文件说明

| 文件 | 说明 |
|------|------|
| `nexapay-static.tar.gz` | 静态网站文件压缩包 (5.3MB) |
| `nginx.conf.example` | Nginx 配置示例 |
| `out/` | 解压后的静态文件目录 |

## 部署步骤

### 1. 上传文件到服务器

```bash
# 解压文件
tar -xzvf nexapos-static.tar.gz

# 将 out 目录重命名并移动到网站目录
sudo mv out /var/www/nexapos
```

### 2. 配置 Nginx

```bash
# 复制配置文件
sudo cp nginx.conf.example /etc/nginx/sites-available/nexapos

# 创建软链接
sudo ln -s /etc/nginx/sites-available/nexapos /etc/nginx/sites-enabled/

# 测试配置
sudo nginx -t

# 重载 Nginx
sudo systemctl reload nginx
```

### 3. 配置 SSL (可选，推荐)

```bash
# 安装 Certbot
sudo apt install certbot python3-certbot-nginx

# 获取证书
sudo certbot --nginx -d nexapos.com -d www.nexapos.com
```

## 目录结构

```
/var/www/nexapos/
├── index.html              # 首页
├── about/index.html        # 关于我们
├── contact/index.html      # 联系我们
├── product/index.html      # 产品介绍
├── solutions/              # 解决方案
│   ├── restaurant/
│   ├── retail/
│   ├── grocery/
│   └── bakery/
├── docs/                   # API 文档
│   ├── api/               # API 接口文档
│   ├── quick-start/
│   └── authentication/
├── support/               # 技术支持
│   ├── developers/
│   ├── faq/
│   └── contact/
├── _next/static/          # 静态资源 (JS/CSS)
├── logo.png               # Logo
└── robots.txt             # 爬虫规则
```

## 服务器要求

- Nginx 1.18+
- 磁盘空间: 50MB+
- 内存: 最低 512MB

## 注意事项

1. **静态网站**: 此版本为纯静态导出，无需 Node.js 运行时
2. **表单提交**: 联系表单为模拟功能，需自行接入后端 API
3. **地图嵌入**: Google 地图需要网络访问
4. **图片优化**: 已禁用 Next.js 图片优化，使用原始图片

## 网站统计

- 总代码行数: 13,471 行
- 页面数量: 28 个
- API 接口文档: 188 个
- 静态文件大小: 15MB
