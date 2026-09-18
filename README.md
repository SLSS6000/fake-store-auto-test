## 📖 项目简介

Fake Store API 是免费的电商模拟开放接口，提供商品、用户、购物车、登录鉴权等 REST 接口能力。
本项目使用 `pytest + requests` 完成电商业务流程自动化测试，模拟真实测试工程师工作：接口封装、夹具复用、正向 & 反向用例设计、识别第三方 API 存在的业务缺陷。

## 📁 项目目录参考

```
fake_store_api_test/
├── api_client/            # 请求封装模块
│   └── store_api.py      # Fake‑Store接口请求封装
├── test_case/             # 自动化测试用例
│   ├── test_product.py    # 商品相关用例
│   ├── test_cart.py       # 购物车相关用例
│   └── test_user.py       # 用户注册登录用例
├── conftest.py            # pytest fixture公共夹具
├── requirements.txt       # python依赖清单
├── report.html            # 生成后的html测试报告
└── README.md              # 项目说明文档
```

## 📂 环境要求

- Python 3.8+
- Pytest 7.4.2
- Requests 2.31.0

## 🚀 快速运行

### 1. 克隆项目到本地

```
git clone https://github.com/chuankangli007/fake_store_api_test.git
cd fake_store_api_test
```

### 2. 安装依赖包

```
pip install -r requirements.txt
```

### 3. 执行自动化测试

```
# 执行全部用例
pytest

# 指定执行购物车模块用例，打印详细日志
pytest test_cart.py -v -s

# 生成HTML可视化报告（需要提前安装pytest‑html）
pytest --html=report.html
```

## ✨ 项目亮点

- 🧩 **轻量化技术栈**：仅依赖 `pytest` + `requests`，无重型框架，代码简洁易懂，适合新手学习
- 🛒 **真实业务场景**：覆盖登录鉴权、商品 CRUD、购物车操作完整电商业务链路
- 📝 **用例设计思维**：正向业务场景 + 异常负向场景结合，共 11 个测试点，12 条自动化用例
- 📌 **缺陷识别处理**：识别 Mock 接口本身存在的多处业务缺陷，使用`xfail`标记预期失败用例，区分业务 Bug 与正常用例
- 📄 **可视化报告支持**：终端输出执行结果，可扩展 `pytest‑html` 生成 HTML 可视化测试报告
- 📂 **工程化规范**：接口请求封装、pytest fixture 夹具复用、日志打印、清晰代码注释

## 🧪 测试业务与执行统计

- 测试点总数：`11`
- 自动化用例总数：`12`
- 正常通过用例：`10`
- 预期失败（API 本身缺陷）：`2`

> 测试覆盖场景：商品新增、查询、用户注册、登录鉴权、购物车增删改、非法参数、不存在 ID 查询、非法入参校验。

### 🚨 Fake Store API 已知问题（本项目识别出的接口缺陷）

1. 查询不存在 ID 资源，接口返回 `200`，而非标准 404，返回空内容，解析 JSON 抛出`ValueError`；项目中通过`try‑except`捕获处理异常。
2. 创建商品传入负数价格，接口返回`201`创建成功，没有返回 400 参数错误，不符合接口参数校验规范；使用`@pytest.mark.xfail`标记为预期失败用例。
3. 用户注册数据服务端不会持久保存；注册账号无法直接登录获取 Token，只能使用官方预置账号登录，也不会返回用户 id；项目中采用合法 id 模拟完成后续业务链路测试。

## 📚 学习收获

1. requests 库完成 HTTP 接口 GET/POST/PUT/DELETE 请求封装
2. pytest 框架、fixture 夹具复用、`‑v‑s`执行参数、`xfail`预期失败标记
3. 正向、反向测试用例设计思路，识别第三方接口业务缺陷
4. try‑except 捕获接口异常，处理非标准响应格式
5. HTML 测试报告生成，自动化项目基础工程结构