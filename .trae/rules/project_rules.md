# 项目开发规则与依赖管理

本文件为项目依赖与开发规则的唯一权威来源。后续所有开发严格基于当前已安装技术栈进行，新增/升级/移除依赖须先更新此文档。

## 依赖分组与安装命令（规范）

### 第一组：核心工具链 + 样式/类型/插件基础（开发依赖）
| 类别 | 技术栈 |
|------|--------|
| 状态管理 | pinia + pinia-plugin-persistedstate |
| CSS 样式 | unocss（含 attributify/mini/uno 预设） |
| 组件自动引入 | unplugin-vue-components + unplugin-auto-import |
| 类型支持 | @types/uni-app + @types/wechat-miniprogram + @uni-helper/uni-app-types |
| 代码质量 | @biomejs/biome |
| 样式预处理 | sass + sass-loader |
| 构建优化 | vite-plugin-restart + vite-plugin-compression + @vitejs/plugin-vue-jsx |
### 第二组：小程序业务工具（请求/路由/校验）（开发依赖）
| 类别 | 技术栈 |
|------|--------|
| HTTP 请求 | uni-ajax |
| 路由管理 | uni-simple-router@2.0.8-beta.4 |
| 表单校验 | @vuelidate/core + @vuelidate/validators |

- uview-plus
- luch-request

> 平台与框架（`@dcloudio/*`、`vue`、`vue-i18n`）由模板/插件统一管理，无需额外命令，版本调整需走变更流程。

## 开发约束
- 所有新增依赖必须记录到 `f:/share/lumikid/.trae/rules/project_rules.md` 文件中，形成项目依赖的唯一管理源。
- 开发过程中必须严格依据 `f:/share/lumikid/.trae/rules/project_rules.md` 中记录的依赖列表进行开发，不得偏离或擅自更改。
- 禁止自行安装任何依赖包。如需要使用新的库或工具，必须先在 `f:/share/lumikid/.trae/rules/project_rules.md` 中添加相应的依赖记录，然后才能基于该记录进行开发。
- 锁定策略：关键构件（`@dcloudio/*`、`vite`、`uni-*`）遵循固定版本或经评审的范围；`pnpm-lock.yaml` 必须提交，禁止手工修改。
- 包管理器统一使用 `pnpm`，禁止使用 `npm`、`yarn`。

## 一致性检查与运行
- 拉取代码后执行：`pnpm i`（与锁文件保持一致）。
- 类型检查：`pnpm run type-check`。
- 代码格式化：`pnpm biome check --write`。
- 微信小程序开发：`pnpm run dev:mp-weixin`；构建：`pnpm run build:mp-weixin`。

> 说明：本文件维护依赖的分组与安装命令及版本基线，任何依赖调整（新增/升级/替换/移除）需先更新此文档，再执行相应命令，确保团队协同一致。