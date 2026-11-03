<p align="center">
  <img src="logo.svg" alt="PDF 文档签章工具" width="110" />
</p>

# PDF 文档签章工具 | PDF Signature & Stamp Tool

[在线使用 / Open the tool](https://yinxi800.github.io/)

在浏览器中为 PDF、JPG 或 PNG 添加签名与印章图像，调整位置和尺寸，导出扫描效果 PDF。工具不提供电子认证服务；使用范围请以网站内免责声明为准。

A browser-based PDF signature and stamp tool. Add visual signature and stamp images to PDF documents or images, adjust placement, and export a scanned-look PDF. This tool does not create certificate-based digital signatures.

[![在线使用](https://img.shields.io/badge/在线使用-GitHub%20Pages-brightgreen)](https://yinxi800.github.io/)
[![React](https://img.shields.io/badge/React-19-blue)](https://react.dev/)
[![TypeScript](https://img.shields.io/badge/TypeScript-6.0-blue)](https://www.typescriptlang.org/)
[![Vite](https://img.shields.io/badge/Vite-8-purple)](https://vite.dev/)
[![Ant Design](https://img.shields.io/badge/Ant%20Design-6-blue)](https://ant.design/)
[![pdf.js](https://img.shields.io/badge/pdf.js-render-red)](https://mozilla.github.io/pdf.js/)
[![pdf-lib](https://img.shields.io/badge/pdf--lib-write-red)](https://github.com/Hopding/pdf-lib)
[![Fabric.js](https://img.shields.io/badge/Fabric.js-7-orange)](https://fabricjs.com/)
[![浏览器处理](https://img.shields.io/badge/文件处理-浏览器内-success)](#隐私与安全)

文档解析、签章合成和 PDF 导出在浏览器中完成：pdf.js 解析页面、Fabric.js 承载签章，pdf-lib 逐页写出扫描版 PDF。可调整墨迹、纸张纹理、页面倾斜和扫描噪声，生成**扫描件观感**文件。

---

## 其他工具

[<img src="assets/weee-icon.svg?v=20261029-de-electronics" width="64" alt="德国 WEEE 产品分类" />](https://yinxi800.github.io/german-weee-classification/)

**[德国 WEEE 产品分类](https://yinxi800.github.io/german-weee-classification/)** · [GitHub 仓库](https://github.com/Yinxi800/german-weee-classification)

支持中文产品名称查询和条件引导，查看分类建议及参考依据。

---

## 核心能力

- **📄 输入格式**：PDF（含扫描版 / 图片型 PDF）、JPG、PNG 扫描图片。

- **🔍 页面识别**：自动读取每一页的物理尺寸、方向、分辨率与色彩模式，缩略图按需渲染。

- **✍🏻 签章定位**：在原始页面上直接拖拽、缩放、旋转放置；支持多页、多枚印章与签名混排。

- **📏 物理尺寸**：印章按**毫米**管理（直径或长宽），自动换算显示像素，落位即真实比例。

- **🎨 印章墨迹**：5 档质感预设（清晰原印 / 均匀实印 / 自然盖印 / 轻压浅印 / 缺墨旧印），可微调墨水浓度、墨迹自然度、边缘柔化。

- **🖋️ 签字同源**：签名走**与印章完全相同的墨迹管线**，仅对侵蚀、缺墨、虚化三类强度施加笔画保真系数，避免细笔画断裂。

- **🖨️ 扫描质感**：3 档预设（轻微 / 中等 / 明显，默认轻微），可微调模糊、噪声、亮度、对比度、纹理、暗角与泛黄，支持黑白输出。

- **📐 页面形态**：整页倾斜（统一旋转角 + 每页随机抖动，模拟纸张没放正）、统一页面尺寸、纸边两档处理。

- **⚡ 大文件保护**：超过 15 MB 或渲染像素超限时，导入前弹窗确认并自动下调渲染精度，防止浏览器内存打爆。

- **🔒 本地优先**：印章 / 签名库保存在浏览器 IndexedDB；文档解析、签章和导出在浏览器中处理。

- **🌐 双语界面**：中文 / English 一键切换。

---

## 使用流程

```text
上传文档 → 放置签章 → 调整墨迹与尺寸 → 生成预览 → 导出扫描版 PDF
```

1. **上传**：拖入或选择 PDF / 图片。大文件会先弹出压缩确认框，确认后按更低渲染精度处理。
2. **放置**：在右侧印章 / 签名库里选中素材，到中间页面点击落位；拖动移动，控制点缩放旋转。
3. **编辑**：右侧面板可调物理尺寸（mm）与旋转角度；`Delete` / `Backspace` 删除选中，`Esc` 退出放置模式。
4. **预览**：页头「生成预览」打开弹窗，左侧看图、右侧调参，参数实时生效。
5. **导出**：弹窗底部「生成签署扫描版」逐页流式写出 PDF，预览与导出共用同一套渲染管线，所见即所得。

---

## 印章与签名

印章与签名共用同一组墨迹参数，保证是"同一支墨"的观感：

| 处理环节 | 印章 | 签名 |
| --- | --- | --- |
| 墨色浓淡、颗粒纹理、不透明度 | 全额 | **同参不变** |
| 边缘侵蚀幅度 | ×1 | ×0.45 |
| 局部缺墨概率 | ×1 | ×0.45 |
| 边缘虚化 | ×1 | ×0.725 |

签名的保真系数（0.45）只削弱会**打断细笔画**的三类力量，墨色与质感保持一致，因此签字不会退化成"完全不处理"，也不会出现笔画断裂。

### 印章质感预设

| 预设 | 说明 |
| --- | --- |
| 清晰原印 | 保留上传素材细节，只增加极轻微的墨色变化 |
| 均匀实印 | 墨色较实、边缘清楚，适合印泥充足且受力均匀 |
| 自然盖印 | 轻微浓淡、飞白和毛边，适合日常办公盖章 |
| 轻压浅印 | 整体偏淡、边缘略散，模拟按压力度不足 |
| 缺墨旧印 | 缺墨和斑驳更明显，适合印泥偏干或印面较旧 |

---

## 隐私与安全

- 文档解析、签章合成和 PDF 写出在浏览器内完成。
- 印章 / 签名素材保存在当前浏览器的 IndexedDB；清除浏览器站点数据后需重新导入。
- 页面使用第三方不蒜子访问统计服务，浏览器加载页面时会向该服务发起请求。

---

## 仓库内容 / Repository contents

此公开仓库存放供 GitHub Pages 使用的**已构建网页文件**，不包含开发用的 `frontend/` 源码目录。

This public repository contains the built website for GitHub Pages. The `frontend/` development source directory is not included here.

```text
index.html    # 网页入口 / website entry point
assets/       # 构建后的脚本、样式和资源 / built assets
README.md     # 项目说明 / project documentation
LICENSE       # 许可说明 / license
```

---

## 常见问题

**导出的文件和预览看起来一样吗？**
一致。预览与导出调用同一条渲染管线、同一组参数，区别只是预览渲染单页、导出逐页流式写出。

**签字看起来比印章"干净"一些，是没处理吗？**
已处理。签字与印章共用同一套墨迹参数，只是侵蚀、缺墨、虚化强度被降到 45%，用来保住细笔画——这是刻意设计，不是漏处理。

**换台电脑印章库还在吗？**
不在。印章 / 签名保存在当前浏览器的 IndexedDB 里，换浏览器或清缓存后需要重新导入素材。
