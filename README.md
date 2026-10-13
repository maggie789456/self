# 麦杞岐对接服务站（男装外套夹克 / 衬衫亨利衫）

面向商家的款式与素材参考站点，由 **麦杞岐（maggie.xie）· OBM2** 维护。

---

## ⭐ 本次更新（重点）

**【🔥 市场需求（高优）】板块已整体更换为「图片压缩包」内容。**

- 原「市场需求」页面（按区域展示的款式编号 + SPU 表格）已替换为**图片参考墙**；
- 图片按两大类分组：**🧥 外套夹克（169 张）**、**👕 衬衫（118 张）**，共 **287 张**；
- 每张图片下方显示 **图片编号**（= 图片文件名去掉扩展名，例如 `22797051`），并带 **复制** 按钮；
- 提示语：**点击复制，发给麦杞岐操作**；
- 支持 **点击图片放大查看**（可左右切换、键盘 ← → 切换、Esc 关闭）；
- 支持 **按图片编号搜索**（顶部搜索框输入编号片段即可筛选）；
- 支持 **搜索图片同款**（图片放大后点击「🔍 搜索图片同款」，站点部署到线上后可跳转以图搜图）。

---

## 一、站点板块一览

| 序号 | 板块 | 入口 | 说明 |
|---|---|---|---|
| 1 | 类目指引 | 首页 `sec-category` | 类目分类与路径，读取 `data/category_guide.json` |
| 2 | 视觉优化 | 首页 `sec-visual` | 市场视觉需求 PDF + AI 指令快速生成入口 |
| 3 | 标题优化 | `title-optimization.html` | 按维度选词生成中英文标题 |
| 4 | **市场需求（高优）** | `market-demand.html` | **图片编号参考墙（本次已更换）** |
| 5 | 企划需求 | `plan-demand.html` | 各风格企划款式参考 PDF |
| 6 | 去年热销 | `top-products.html` | 去年热销商品参考 |
| 7 | 9月Top热销 | `sept-topsale.html` | 2026 年 9 月各品类热销参考 |
| 8 | 近期资讯 | 首页 `sec-info` | 国家站点热搜词、近期通知（txt 维护） |
| 9 | 最新款式资讯 | 首页 `sec-latest` | 资讯列表，点击加载对应 PDF |

---

## 二、目录结构

```
.
├── index.html                    # 首页（各板块入口）
├── market-demand.html            # 【市场需求（高优）】图片墙页面 ★本次重写
├── title-optimization.html
├── plan-demand.html
├── top-products.html
├── sept-topsale.html
├── image-optimization.html
├── README.md
├── data/                         # 数据文件
│   ├── category_guide.json
│   ├── keyword_library.json
│   ├── title_keywords.json
│   ├── top_products.json
│   ├── sept_topsale.json
│   ├── hot-words.txt
│   └── notifications.txt
└── assets/
    ├── css/style.css
    ├── js/
    │   ├── app.js                # 首页交互
    │   └── demand-images.js      # ★市场需求图片编号清单
    ├── pdf/                      # 各板块 PDF 文档
    └── images/
        └── demand/               # ★市场需求图片
            ├── jacket/           # 外套夹克图片（文件名 = 图片编号.png）
            └── shirt/            # 衬衫图片（文件名 = 图片编号.png）
```

---

## 三、市场需求图片区更新方法

### 1. 新增 / 更换图片

1. 把新图片放进对应目录，**文件名就是「图片编号」**，扩展名为 `.png`：
   - 外套夹克 → `assets/images/demand/jacket/`
   - 衬衫 → `assets/images/demand/shirt/`
2. 打开 `assets/js/demand-images.js`，在对应数组里补上/修改编号（编号 = 文件名去掉 `.png`）：

```js
window.DEMAND_IMAGES = {
  "jacket": ["22797051", "22937515", ...],   // 外套夹克
  "shirt":  ["28789674", "30683945", ...]    // 衬衫
};
```

3. 保存后页面会自动按清单渲染，数量统计（Tab 上的括号数字）也会自动更新。

> 说明：图片命名必须与清单编号一致，否则会出现「图片加载失败」。

### 2. 删除图片

从对应目录删除图片文件，并在 `demand-images.js` 的数组中删除该编号。

---

## 四、其他数据更新方法

| 内容 | 更新方式 |
|---|---|
| 类目指引 | 替换 `data/category_guide.json` |
| 标题优化词库 | 替换 `data/title_keywords.json` / `data/keyword_library.json` |
| 去年热销 | 替换 `data/top_products.json` |
| 9月Top热销 | 替换 `data/sept_topsale.json` |
| 热搜词 / 近期通知 | 直接编辑 `data/hot-words.txt`、`data/notifications.txt` |
| 各板块 PDF | 覆盖 `assets/pdf/` 下同名 PDF 文件即可 |

---

## 五、本地预览

- 直接双击 `index.html` 即可在浏览器中预览（图片墙板块使用脚本清单，本地可直接显示图片）；
- 其余板块的部分数据通过 `data/*.json` 读取，**建议用本地服务器预览**（如 VS Code Live Server）以保证数据正常加载。

---

## 六、部署到 GitHub Pages

1. 解压本压缩包，得到网站全部文件；
2. 打开 GitHub 仓库页面，将全部文件（含 `assets/`、`data/` 目录）上传覆盖；
   - ⚠️ 注意上传后确认 `assets/images/demand/`、`data/` 目录结构正确，避免文件被放到根目录导致 404；
3. 若已开启 Pages（Deploy from a branch），等待构建完成即可访问。

---

## 七、注意事项

- 本页面展示的图片**仅为款式参考**，不可直接复制或侵权使用，所有图片版权归原品牌所有；
- 本网页所有功能只提供建议，不负任何法律责任，所有资源来源于互联网；
- 如有功能更新需求，请联系 **麦杞岐（maggie.xie）**。