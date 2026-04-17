# 🚀 MemFire 超简单配置（3步完成）

## 📋 第一步：注册MemFire（3分钟）

1. **打开浏览器**，访问：**https://www.memfiredb.com/**
2. 点击 **"免费开始使用"**
3. **注册账号**：用邮箱注册，查收验证邮件
4. **登录**：进入控制台

## 🛠️ 第二步：创建项目和获取凭证（2分钟）

1. 点击 **"新建项目"**
2. 填写信息：
   - **项目名称**：`community-group-buy`
   - **数据库名称**：`group-buy-db`
   - **区域**：选择离你最近的
3. 点击 **"创建项目"**
4. **记录两个信息**（等会要用）：
   - **项目URL**：类似 `https://xxx.memfiredb.com`
   - **Anon Key**：类似 `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...`

## 📊 第三步：创建数据表（5分钟）

### 3.1 创建商品表（Product）
1. 点击左侧 **"表编辑器"**
2. 点击 **"新建表"**
3. 填写表信息：
   - **表名**：`product`
   - **描述**：商品表
4. 添加字段（点击"添加字段"按钮）：
   - `id`：类型 `uuid`，主键，勾选"默认值"，填入 `gen_random_uuid()`
   - `name`：类型 `text`，勾选"非空"
   - `description`：类型 `text`
   - `price`：类型 `numeric`，勾选"非空"
   - `stock`：类型 `integer`
   - `image`：类型 `text`
   - `specs`：类型 `jsonb`
   - `active`：类型 `boolean`，勾选"默认值"，填入 `true`
   - `created_at`：类型 `timestamptz`，勾选"默认值"，填入 `now()`
5. 点击 **"保存"**

### 3.2 创建订单表（Order）
1. 同样点击 **"新建表"**
2. **表名**：`order`
3. 添加字段：
   - `id`：类型 `uuid`，主键，勾选"默认值"，填入 `gen_random_uuid()`
   - `nickname`：类型 `text`，勾选"非空"
   - `items`：类型 `jsonb`，勾选"非空"
   - `total`：类型 `numeric`，勾选"非空"
   - `remark`：类型 `text`
   - `status`：类型 `text`，勾选"默认值"，填入 `'pending'`
   - `created_at`：类型 `timestamptz`，勾选"默认值"，填入 `now()`
4. 点击 **"保存"**

### 3.3 创建配置表（Config）
1. 同样点击 **"新建表"**
2. **表名**：`config`
3. 添加字段：
   - `id`：类型 `uuid`，主键，勾选"默认值"，填入 `gen_random_uuid()`
   - `key`：类型 `text`，勾选"非空"，勾选"唯一"
   - `value`：类型 `jsonb`
   - `created_at`：类型 `timestamptz`，勾选"默认值"，填入 `now()`
4. 点击 **"保存"**

## 🔐 第四步：设置权限（重要！）

### 4.1 启用行级安全
1. 对每个表（product、order、config）点击表名
2. 找到 **"行级安全(RLS)"**，点击 **"启用"**

### 4.2 创建访问策略
1. 点击左侧 **"认证"** → **"策略"**
2. 点击 **"新建策略"**
3. 选择表，选择 **"自定义策略"**
4. 策略名称：`Allow public access`
5. 策略定义：`true`
6. 操作：勾选 **SELECT、INSERT、UPDATE、DELETE**
7. 点击 **"保存"**

**重复以上步骤，为三个表都创建策略**

## ✏️ 第五步：配置HTML文件（1分钟）

1. 打开 `index-memfire.html` 文件
2. 按 **Ctrl + F** 搜索 `MEMFIRE_CONFIG`
3. 找到这段代码：
```javascript
const MEMFIRE_CONFIG = {
    url: '你的MemFire项目URL',  // 例如：https://xxx.memfiredb.com
    anonKey: '你的Anon Key'     // 例如：eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
};
```

4. 把刚才记录的两个信息填进去：
```javascript
const MEMFIRE_CONFIG = {
    url: 'https://xxx.memfiredb.com',  // 你的项目URL
    anonKey: 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...'  // 你的Anon Key
};
```

5. **保存文件**（Ctrl + S）

## 🎉 配置完成！

现在你可以：
1. **刷新页面**：应该显示"加载中..."（不是"需要配置"）
2. **进入管理端**：访问链接加 `#admin`，输入密码 `admin123`
3. **添加商品**：在管理端添加商品
4. **分享链接**：把链接发到微信群

## 🔍 配置验证

**配置成功标志：**
1. ✅ 刷新页面后显示 **"加载中..."**（不是"需要配置"）
2. ✅ 进入管理端能看到 **"商品管理"**、**"订单管理"**、**"系统设置"**
3. ✅ 在管理端添加商品后，下单端能看到商品
4. ✅ 能成功提交测试订单

## ❓ 常见问题

**Q: 还是显示"需要配置"怎么办？**
A: 检查MemFire配置是否正确，特别是URL和Anon Key。

**Q: 显示"加载商品失败"怎么办？**
A: 检查数据表是否创建，权限是否设置。

**Q: 数据表权限怎么设置？**
A: 在MemFire控制台，对每个表启用行级安全，创建访问策略。

## 📞 需要帮助？

1. 查看 **`MemFire配置指南.md`** 详细说明
2. 打开 **`index-memfire.html`** 测试配置
3. 检查浏览器控制台错误信息（F12）

---

**配置就是这么简单！🛒🎉**