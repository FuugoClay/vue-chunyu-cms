## Project Introduction
Chunyu is a system designed for quickly building film and television websites. Its user-end is based on [nuxt3](https://nuxt.com/) and [element-ui](https://element.eleme.cn/#/zh-CN), the management-end on [vue3](https://cn.vuejs.org/) and [element-ui](https://element.eleme.cn/#/zh-CN), the backend on Node's framework [nestjs](https://docs.nestjs.cn/8/), using MySQL for the database, and Redis for caching.

## Online Experience
  - [User-end Demo](http://cms.yinchunyu.com)
  - [Management-end Demo](http://cms-admin.yinchunyu.com)
  - Source Code: [GitHub](https://github.com/yinMrsir/chunyu-cms) | [Gitee](https://gitee.com/chunyu-cms/chunyu-cms)
  - [Nuxt3 Tutorial Documentation](https://www.yinchunyu.com)
  - [Nuxt3 Video Tutorial](https://www.bilibili.com/video/BV1gu4y1R7Jt/?spm_id_from=333.999.0.0&vd_source=9dbe815ca79d8528e02be1a51583912a)

## Technical Requirements
  - [Vue](https://cn.vuejs.org/)
  - [Element-ui](https://element.eleme.cn/#/zh-CN)
  - [TypeScript](https://www.tslang.cn/index.html)
  - [Nestjs](https://docs.nestjs.cn/8/)
  - [TypeORM](https://typeorm.biunav.com/)
  - MySQL
  - Redis
  
## Technology Selection
  1. **Front-end Technology**
   - nuxt @3.6.5
   - vue @3.2.45
   - element-plus @2.2.21
   - axios @0.24.0
   - vuex @3.6.0
   - vue-router @3.4.9
   - sass-loader @10.1.1

  2. **Backend Technology**
   - nest @8.0
   - mysql2 @2.3.3
   - swagger-ui-express @4.2.0
   - typeorm @0.2.41
   - ioredis @4.28.2

## Before Development

If you have not installed MySQL and Redis, please do so first. MySQL 8 and Redis 7 are recommended. [Installation Guide](#related-links)

If nest-cli is not installed, execute `npm install -g @nestjs/cli` to install it globally.

For local development and service startup, see: [Related Video](https://www.douyin.com/user/MS4wLjABAAAAUKMCVZGbQl7etrdd36GBIG6OGxClOwoHci_-PIlxNvE?modal_id=7213009576487177504)

## Deployment

### Building the Server:

First, modify the database connection configuration in `Nest-server/src/config/config.production.ts`, then execute:

```shell
cd Nest-server
yarn
yarn build
```

### Building the User-end:
Create a `.env` file in the Nuxt-web directory and write `BASE_URL=server request address`

```shell
cd Nuxt-web
yarn
yarn build
```

### After building, deployment can be done using pm2. If not installed, execute npm install -g pm2 to install.
Execute the following command to start the service:

```shell
pm2 start pm2.config.cjs
```

### Building the Management-end
Execute the following commands to generate the `dist` directory, which can be pointed to using `nginx`:

```shell
cd Vue3-admin
yarn
yarn build:prod
```

### Single File Packaging
If you need to package into a single file or a pkg package, enter Nest-server and execute `yarn ncc:pkg`.
Since the bull library does not support single-file execution, you must remove the modules that imported the bull library before packaging!

## Updates
- [x] Support for back-end configuration of friendly links
- [x] User film and television rating
- [x] User check-in
- [x] User earns coins for check-in
- [x] Support for paid viewing of videos
- [x] Support for uploading images and videos to Alibaba Cloud OSS

### To Be Completed
- [ ] User purchases coins
- [ ] Video sending bullet comments

## Related Links

Windows Docker Installation: https://zhuanlan.zhihu.com/p/441965046

Docker Installation of Redis：https://www.yinchunyu.com/other/redis.html

Docker Installation of MySQL：https://www.runoob.com/docker/docker-install-mysql.html

Solving Navicat Database Connection Issue `client does not support authentication`：https://blog.csdn.net/lovedingd/article/details/106728292

## For Any Questions, Add WeChat:

<img height="120" src="https://gitee.com/chunyu-cms/chunyu-cms/raw/main/wx.jpg" width="120"/>

## How to Use Alibaba Cloud OSS for Uploading Files
Step One Modify `pm2.config.cjs` or directly modify the corresponding configuration file in the `Nest-server/src/config` directory:

// 1、pm2.config.js
module.exports = {
  apps : [
    {
      env: {
        // ...
        // Fill in the region where the Bucket is located. For example, for East China 1 (Hangzhou), fill in oss-cn-hangzhou for Region:
        REGION: '',
        // The Aliyun account AccessKey has access to all APIs and is very high risk. It is strongly recommended that you create and use a RAM user for API access or routine operations, please log in to the RAM console to create a RAM user:
        ACCESS_KEY_Id: '',
        ACCESS_KEY_SECRET: '',
        // Fill in the Bucket name:
        BUCKET: '',
        // Whether to support uploading with a custom domain:
        CNAME: false,
        // OSS access domain:
        ENDPOINT: ''
      }
    }
  ]
};
```
**Step Two** Go to the back-end system management - parameter configuration, and change the Whether to enable file upload to Alibaba Cloud parameter key value to `1`

> Note: The management-end has a cross-origin issue when capturing video covers, so you need to configure Alibaba Cloud to allow cross-origin.
