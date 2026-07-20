# 📺 自定义影视仓 APK 构建器

> 无需开发环境，全程 GitHub 网页操作，3 步生成专属 App

---

## 🚀 快速开始（3 步）

### 第 1 步：Fork 本仓库

点击右上角 **Fork** 按钮，复制到你自己的 GitHub 账号下。

### 第 2 步：触发构建

进入你 Fork 后的仓库，点击：

```
Actions → 构建自定义影视仓 APK → Run workflow
```

填写以下参数：

| 参数 | 说明 | 示例 |
|------|------|------|
| **App 显示名称** | 安装后桌面显示的名字 | `追剧神器` |
| **包名** | 唯一标识，全小写+点 | `com.myapp.video` |
| **默认配置接口** | App 启动后自动加载的源 | `https://jihulab.com/z-blog/xh2/-/raw/main/t3.json` |
| **版本号** | 自定义版本 | `1.0.0` |

### 第 3 步：下载 APK

等待 5～10 分钟，构建完成后在 **Actions → 对应任务 → Artifacts** 处下载 APK。

---

## 📡 推荐配置接口（直接复制填入）

### 多仓（推荐，包含所有线路）

```
# 运输车多仓（国内快）
https://jihulab.com/z-blog/xh2/-/raw/main/t3.json

# 砂锅多仓（秒开）
https://agit.ai/ddx/TVBox/raw/branch/master/d.json

# 欧歌多仓（线路全）
http://m.nxog.top/nxog/ou1.php?url=http://tv.nxog.top&b=欧歌

# 香雅情多仓
https://github.moeyy.xyz/https://raw.githubusercontent.com/xyq254245/xyqonlinerule/main/XYQTVBox.json
```

### 单线路

```
# 饭太硬（老牌稳定）
http://饭太硬.top/tv

# 骚零接口
https://xhdwc.tk/0

# 4K 极速电影
https://agit.ai/ddx/TVBox/raw/branch/master/t4.json
```

---

## ❓ 常见问题

**Q: 构建失败怎么办？**
A: 点进失败的 Action，展开报错步骤查看日志。最常见原因是上游源码结构变化，可在 Issues 中反馈。

**Q: 可以换图标吗？**
A: 可以。Fork 后，替换 `app/src/main/res/mipmap-*/` 目录下的 `ic_launcher.png`（各尺寸），再触发构建即可。图标尺寸：`mdpi=48px`, `hdpi=72px`, `xhdpi=96px`, `xxhdpi=144px`, `xxxhdpi=192px`。

**Q: 包名有什么要求？**
A: 格式为 `com.xxx.xxx`，只能用小写字母、数字和点，不能以点开头或结尾，每段至少一个字母。同一手机上包名不同的 App 可以共存。

**Q: APK 安全吗？**
A: 构建过程完全开源透明，签名密钥在构建时随机生成（临时自签名），仅用于安装。如需统一签名密钥，可在仓库 Secrets 中配置自己的 keystore。

**Q: 源码来自哪里？**
A: 基于 [FongMi/TV](https://github.com/FongMi/TV) 开源项目修改，遵循原项目 GPL 协议。

---

## 🔑 自定义签名密钥（可选，多设备保持同一签名）

1. 本地执行生成 keystore：
```bash
keytool -genkeypair -v \
  -keystore my.jks \
  -keyalg RSA -keysize 2048 -validity 36500 \
  -alias mykey \
  -storepass 你的密码 \
  -keypass 你的密码 \
  -dname "CN=你的名字, O=你的组织, C=CN"
```

2. 将 `my.jks` 转 Base64：
```bash
base64 -w0 my.jks > my.jks.b64
cat my.jks.b64
```

3. 在 GitHub 仓库 → Settings → Secrets → Actions 中添加：
   - `KEYSTORE_BASE64` = base64 内容
   - `KEY_ALIAS` = mykey
   - `KEY_PASSWORD` = 你的密码
   - `STORE_PASSWORD` = 你的密码

---

## 📄 License

基于上游开源项目，遵循 GPL-3.0 协议。接口来源于网络，仅供学习研究使用。
