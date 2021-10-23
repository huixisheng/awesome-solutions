# awesome-solutions

> 记录研发过程中碰到问题的解决方案，很多思路来源于互联网。取之于民用之于民，将相关的问题做个简单的解决方案的总结输出。
> 推荐文章: 解决问题发现的不错的总结内容。
> 相关参考: 灵感来源，做了更多的扩展阅读。

## Error: Unable to download sentry-cli binary from https://downloads.sentry-cdn.com/sentry-cli/1.69.1/sentry-cli-Linux-x86_64.
```
error /home/jenkins/agent/workspace/project-MJJYNKLOXR5K/developer-dashboard/node_modules/@sentry/cli: Command failed.
Exit code: 1
Command: node scripts/install.js
Arguments: 
Directory: /home/jenkins/agent/workspace/project-MJJYNKLOXR5K/developer-dashboard/node_modules/@sentry/cli
Output:
info sentry-cli Downloading from https://downloads.sentry-cdn.com/sentry-cli/1.69.1/sentry-cli-Linux-x86_64
Error: Unable to download sentry-cli binary from https://downloads.sentry-cdn.com/sentry-cli/1.69.1/sentry-cli-Linux-x86_64.
Error code: ETIMEDOUT
script returned exit code 1
```

配置 `.npmrc`  `sentrycli_cdnurl="https://npm.taobao.org/mirrors/sentry-cli"`

附上一个比较完整的 `npmrc` 的镜像配置
```
@intranetScope:registry=https://registry.your.custom
# https://cnodejs.org/topic/61405b76fe0c5109a7aea0ed
registry="https://registry.npmmirror.com"
disturl="https://npm.taobao.org/dist"
nvm_nodejs_org_mirror="https://npm.taobao.org/mirrors/node"
nodejs_org_mirror="https://npm.taobao.org/mirrors/node"
sass_binary_site="https://npm.taobao.org/mirrors/node-sass"
electron_mirror="https://npm.taobao.org/mirrors/electron/"
SQLITE3_BINARY_SITE="https://npm.taobao.org/mirrors/sqlite3"
profiler_binary_host_mirror="https://npm.taobao.org/mirrors/node-inspector/"
node_inspector_cdnurl="https://npm.taobao.org/mirrors/node-inspector"
selenium_cdnurl="https://npm.taobao.org/mirrors/selenium"
puppeteer_download_host="https://npm.taobao.org/mirrors"
chromedriver_cdnurl="https://npm.taobao.org/mirrors/chromedriver"
operadriver_cdnurl="https://npm.taobao.org/mirrors/operadriver"
phantomjs_cdnurl="https://npm.taobao.org/mirrors/phantomjs"
fse_binary_host_mirror="https://npm.taobao.org/mirrors/fsevents"
sqlite3_binary_host_mirror="https://npm.taobao.org/mirrors/sqlite3"
canvas_binary_host_mirror="https://npm.taobao.org/mirrors/node-canvas-prebuilt"
sentrycli_cdnurl="https://npm.taobao.org/mirrors/sentry-cli/"
# https://segmentfault.com/a/1190000022875865
sharp_dist_base_url="https://npm.taobao.org/mirrors/sharp-libvips/"
python_mirror="https://npm.taobao.org/mirrors/python/"
# https://github.com/cnpm/binary-mirror-config/blob/01832e6a6da40584dc3360a2c7a8b2f8a3d3c134/package.json
ELECTRON_BUILDER_BINARIES_MIRROR="https://npm.taobao.org/mirrors/electron-builder-binaries/"
SWC_BINARY_SITE="https://cdn.npm.taobao.org/dist/node-swc"
FLOW_BINARY_MIRROR="https://github.com/facebook/flow/releases/download/v"
NWJS_URLBASE="https://cdn.npm.taobao.org/dist/nwjs/v"
npm_config_sharp_binary_host="https://cdn.npm.taobao.org/dist/sharp"
npm_config_sharp_libvips_binary_host="https://npm.taobao.org/mirrors/sharp-libvips"
npm_config_robotjs_binary_host="https://cdn.npm.taobao.org/dist/robotjs"
```

推荐文章
- 聊聊NPM镜像那些险象环生的坑 - 掘金 https://juejin.cn/post/6844904192247595022


## K8S PM2 error: Trace: Error: spawn E2BIG
```
2021-09-30T16:11:10: PM2 log: Launching in no daemon mode
9/30/2021 4:11:10 PM 2021-09-30T16:11:10: PM2 log: App [baiying-apollo:0] starting in -cluster mode-
9/30/2021 4:11:10 PM 2021-09-30T16:11:10: PM2 error: Trace: Error: spawn E2BIG
9/30/2021 4:11:10 PM     at ChildProcess.spawn (internal/child_process.js:394:11)
9/30/2021 4:11:10 PM     at spawn (child_process.js:540:9)
9/30/2021 4:11:10 PM     at fork (child_process.js:108:10)
9/30/2021 4:11:10 PM     at createWorkerProcess (internal/cluster/master.js:130:10)
9/30/2021 4:11:10 PM     at EventEmitter.cluster.fork (internal/cluster/master.js:164:25)
9/30/2021 4:11:10 PM     at Object.nodeApp (/usr/local/node-v12.14.0-linux-x64/lib/node_modules/lib/node_modules/pm2/lib/God/ClusterMode.js:48:21)
9/30/2021 4:11:10 PM     at Object.executeApp (/usr/local/node-v12.14.0-linux-x64/lib/node_modules/lib/node_modules/pm2/lib/God.js:236:9)
9/30/2021 4:11:10 PM     at inject (/usr/local/node-v12.14.0-linux-x64/lib/node_modules/lib/node_modules/pm2/lib/God.js:150:18)
9/30/2021 4:11:10 PM     at Object.injectVariables (/usr/local/node-v12.14.0-linux-x64/lib/node_modules/lib/node_modules/pm2/lib/God.js:577:10)
9/30/2021 4:11:10 PM     at /usr/local/node-v12.14.0-linux-x64/lib/node_modules/lib/node_modules/pm2/lib/God.js:148:9 {
9/30/2021 4:11:10 PM   errno: 'E2BIG',
9/30/2021 4:11:10 PM   code: 'E2BIG',
9/30/2021 4:11:10 PM   syscall: 'spawn'
9/30/2021 4:11:10 PM }
9/30/2021 4:11:10 PM     at Object.God.logAndGenerateError (/usr/local/node-v12.14.0-linux-x64/lib/node_modules/lib/node_modules/pm2/lib/God/Methods.js:34:15)
9/30/2021 4:11:10 PM     at Object.nodeApp (/usr/local/node-v12.14.0-linux-x64/lib/node_modules/lib/node_modules/pm2/lib/God/ClusterMode.js:50:11)
9/30/2021 4:11:10 PM     at Object.executeApp (/usr/local/node-v12.14.0-linux-x64/lib/node_modules/lib/node_modules/pm2/lib/God.js:236:9)
9/30/2021 4:11:10 PM     at inject (/usr/local/node-v12.14.0-linux-x64/lib/node_modules/lib/node_modules/pm2/lib/God.js:150:18)
9/30/2021 4:11:10 PM     at Object.injectVariables (/usr/local/node-v12.14.0-linux-x64/lib/node_modules/lib/node_modules/pm2/lib/God.js:577:10)
9/30/2021 4:11:10 PM     at /usr/local/node-v12.14.0-linux-x64/lib/node_modules/lib/node_modules/pm2/lib/God.js:148:9
9/30/2021 4:11:10 PM     at /usr/local/node-v12.14.0-linux-x64/lib/node_modules/lib/node_modules/pm2/node_modules/_async@3.1.0@async/internal/map.js:22:9
9/30/2021 4:11:10 PM     at replenish (/usr/local/node-v12.14.0-linux-x64/lib/node_modules/lib/node_modules/pm2/node_modules/_async@3.1.0@async/internal/eachOfLimit.js:81:17)
9/30/2021 4:11:10 PM     at /usr/local/node-v12.14.0-linux-x64/lib/node_modules/lib/node_modules/pm2/node_modules/_async@3.1.0@async/internal/eachOfLimit.js:86:9
9/30/2021 4:11:10 PM     at _asyncMap (/usr/local/node-v12.14.0-linux-x64/lib/node_modules/lib/node_modules/pm2/node_modules/_async@3.1.0@async/internal/map.js:20:12)
9/30/2021 4:11:10 PM 2021-09-30T16:11:10: PM2 error: 0 application started (no apps to run on /data/pm2.config.js)
9/30/2021 4:11:10 PM 2021-09-30T16:11:10: PM2 log: PM2 successfully stopped
```

可以把 `exec_mode` 改成 `fork`，但终归不是最优解。

```
module.exports = {
  name: 'yourAppName',
  exec_mode: 'cluster',
  script: 'dist/apps/main/src/main.js',
  // pm2 默认会加载 sourcemap，解决 sentry sourcemap 不生效的问题
  source_map_support: false,
  watch: false,
  // 如果有定时任务要特别注意，会推送两次
  instances: 2,
  // 含义理解反了
  // filter_env: ['APP_ENV', 'MYSQL_', 'K8S_', 'FE_'],
  filter_env: ['_HOST_', '_PORT_'],
  env: {
    NODE_ENV: 'production',
    API_ENV: process.env.API_ENV,
  }
};
```

![l2BhFM_hzsTbF](https://cdn.byai.com/static/images/l2BhFM_hzsTbF.png)

**注意📢:** `pm2@4.2.1` 不支持 `filter_env` 配置。

![7Z3HLa_wecom-temp-84775837c6d62e57982f939756d86b56](https://cdn.byai.com/static/images/7Z3HLa_wecom-temp-84775837c6d62e57982f939756d86b56.png)


推荐文章

- pm2-runtime: env spawn E2BIG · Issue #4725 · Unitech/pm2 [https://github.com/Unitech/pm2/issues/4725](https://github.com/Unitech/pm2/issues/4725)
- 一次环境变量引发的血案 | 深红结界 [https://anata.me/2019/11/01/一次环境变量引发的血案/](https://anata.me/2019/11/01/%E4%B8%80%E6%AC%A1%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F%E5%BC%95%E5%8F%91%E7%9A%84%E8%A1%80%E6%A1%88/)


相关参考

- 当K8S遇到PM2 | 好好学习的郝 [https://www.voidking.com/dev-k8s-pm2/](https://www.voidking.com/dev-k8s-pm2/)
- 记一次NodeJS测试集群全线瘫痪的解决思路 - 知乎 [https://zhuanlan.zhihu.com/p/74056339](https://zhuanlan.zhihu.com/p/74056339)
- yaoyanhuo [http://www.yaoyanhuo.com/blog/pm2/](http://www.yaoyanhuo.com/blog/pm2/)
- PM2 - Ecosystem File [https://pm2.keymetrics.io/docs/usage/application-declaration/](https://pm2.keymetrics.io/docs/usage/application-declaration/)
- pm2的cluster模式与fork模式的区别 · Issue #19 · mopduan/team [https://github.com/mopduan/team/issues/19](https://github.com/mopduan/team/issues/19)
- PM2 - 掘金 [https://juejin.cn/post/6844904202460905485#heading-2](https://juejin.cn/post/6844904202460905485#heading-2)
- node.js - 在 pm2 中从 fork 切换到集群模式 - IT工具网 [https://www.coder.work/article/1393691](https://www.coder.work/article/1393691)
- 想要飞得高，那就把地平线忘掉 [https://libin1991.github.io/2019/01/03/Pm2-常用配置及命令/](https://libin1991.github.io/2019/01/03/Pm2-%E5%B8%B8%E7%94%A8%E9%85%8D%E7%BD%AE%E5%8F%8A%E5%91%BD%E4%BB%A4/)
- (……) 关于pm2的fork启动模式和cluster模式的区别 - SegmentFault 思否 [https://segmentfault.com/q/1010000005972763](https://segmentfault.com/q/1010000005972763)



## denied: requested access to the resource is denied 登录 harbor 报错。

因为使用连接的 `mac` 机器使用了 `shell` 登录， 需要重新登录。

- harbor解决docker push镜像时denied: requested access to the resource is denied : docker | 少将全栈 [https://www.whatled.com/post-6459.html](https://www.whatled.com/post-6459.html)


## Error saving credentials: error storing credentials - err: exit status 1, out: `error storing credentials - err: exit status 1, out: `User interaction is not allowed.


~~使用命令 `security unlock-keychain`~~

删除钥匙串里面的 docker 相关的内容， `rm /usr/local/bin/docker-credential-osxkeychain`  就可以登录成功了。

![xIT3g4_RyavTg](https://cdn.byai.com/static/images/xIT3g4_RyavTg.png)


> Go to you OSX keychains (through spotlight). Search for docker and delete all saved credentials under the login keychains. Delete the config.json and try to login again
> https://stackoverflow.com/questions/45713562/docker-push-to-docker-hub-unauthorized-error-on-mac

- 无法在远程Mac上进行Docker登录(保存凭据时出错) | 码农家园 [https://www.codenong.com/af6adef956b4447c90c2/](https://www.codenong.com/af6adef956b4447c90c2/)
- https://github.com/docker/for-mac/issues/2295#issuecomment-370588420


## Error: connect EADDRNOTAVAIL 172.16.x.x:389 - Local (10.10.x.x:0)

`netstat -an | grep -e tcp -e udp | wc -l` 查看相关的连接数，一台服务器作为client最大 tcp 连接数为 65535。

![tGdLa1_x7C05X](https://cdn.byai.com/static/images/tGdLa1_x7C05X.png)

测试发现 LDAP 的连接数一直狂增。

![AORkVM_wecom-temp-026d08d485ff4c518c1ef3d335bd8e8c](https://cdn.byai.com/static/images/AORkVM_wecom-temp-026d08d485ff4c518c1ef3d335bd8e8c.png)


推荐文章

- Node.js抛异常ECONNRESET退出｜YYGCui's blog [http://blog.cuicc.com/blog/2017/03/26/nodejs-ECONNRESET/](http://blog.cuicc.com/blog/2017/03/26/nodejs-ECONNRESET/)


参考文章
  
- 单服务器最大tcp连接数及调优汇总 - duanxz - 博客园 [https://www.cnblogs.com/duanxz/p/4464178.html](https://www.cnblogs.com/duanxz/p/4464178.html)
- 服务器最大TCP连接数及调优汇总_走向程序的康庄大道-CSDN博客_服务器最大连接数怎么设置 [https://blog.csdn.net/OiteBody/article/details/111640298](https://blog.csdn.net/OiteBody/article/details/111640298)
- 一台Linux服务器可以负载多少个连接？ - 掘金 [https://juejin.cn/post/6844903937187774477](https://juejin.cn/post/6844903937187774477)
- 详解Linux服务器最大tcp连接数 - 陌上归人的博客 - 博客园 [https://www.cnblogs.com/fjping0606/p/4729389.html](https://www.cnblogs.com/fjping0606/p/4729389.html)
- 一台机器最多能撑多少个TCP连接? 今天掰扯清楚！ - 知乎 [https://zhuanlan.zhihu.com/p/290651392](https://zhuanlan.zhihu.com/p/290651392)
- 漫画 | 一台Linux服务器最多能支撑多少个TCP连接？ - 文章详情 [https://z.itpub.net/article/detail/6CE774C020CABC43FB0B9C79C97C2C4D](https://z.itpub.net/article/detail/6CE774C020CABC43FB0B9C79C97C2C4D)
- 高并发下场景下，使用nodejs产生的问题 - CNode技术社区 [https://cnodejs.org/topic/5d303e32b2b9222961dabe89](https://cnodejs.org/topic/5d303e32b2b9222961dabe89)
