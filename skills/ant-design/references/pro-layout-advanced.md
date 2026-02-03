# 布局（Pro Layout）复杂场景参考

## 适用范围

- 多级菜单与动态路由配置
- 带权限的菜单渲染与面包屑
- 多布局壳（如登录页/工作台/管理区）

## 关键原则

- 路由配置是菜单与面包屑的单一来源，避免手工拼装导航数据。
- 权限控制应集中在 `access` 层，页面级优先于按钮级。
- 布局壳保持最小状态，不在布局层耦合业务数据请求。

## 常见实践

- 菜单权限：结合 `access` 与路由元信息决定是否展示菜单项。
- 多布局：通过路由分组或配置不同 layout，隔离登录/异常页与主应用。
- Tab/KeepAlive：需要缓存的页面在路由层标记，避免页面内部实现缓存逻辑。

## 参考文档

- `https://pro.ant.design/docs/layout`
- `https://pro.ant.design/docs/advanced-menu`
- `https://pro.ant.design/docs/authority-management`
