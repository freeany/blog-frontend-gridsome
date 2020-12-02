### 管理后台 Strapi

> 通用的内容管理系统，轻松的实现内容管理，这个内容可以是千变万化的，可以管理博客的文章，可以管理商品，管理用户的评论，管理用户....

- 特点

  - 自定义内容结构
  - 开发者友好的api
  - 支持角色、权限的管理
  - 支持插件系统，扩展更多功能
  - 更自定义的自定义

- 流程

  - 创建集合，添加数据，使用resultful API查找数据， 要将item的state置为publish。 (用publish角色的权限去查找)

    `https://strapi.io/documentation/v3.x/content-api/api-endpoints.html#endpoints`

  - 用指定用户的权限去 做一些操作。

    - 先登录， 获取到返回的token。

      ```js
      .post('http://localhost:1337/auth/local', {
          identifier: 'user@strapi.io',
          password: 'strapiPassword',
        })
      ```

    - ```js
      http://localhost:1337/posts， {
          headers: {
          	Authorization: `Bearer ${token}`,
          },
      }
      ```

- 用户 -- 角色 -- 权限 的关系

  1. 每个用户都i有一个角色。
  2. 每个角色都有对应的权限，每个集合都有不同的权限。
  3. 当接口带了 Authorization 的header的话， 这个接口就相当于代表了某个用户(其实内部是通过角色访问的)。否则就是publish角色.

- GraphQL在strapi中的使用

  `npm install graphql`  使用`http://localhost:1337/graphql` 地址访问graphQL界面。