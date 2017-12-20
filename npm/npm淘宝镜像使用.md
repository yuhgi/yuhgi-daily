# 使用NPM淘宝镜像

- [使用NPM淘宝镜像](#%E4%BD%BF%E7%94%A8npm%E6%B7%98%E5%AE%9D%E9%95%9C%E5%83%8F)
    - [1.使用--registry参数指定仓库地址](#1%E4%BD%BF%E7%94%A8--registry%E5%8F%82%E6%95%B0%E6%8C%87%E5%AE%9A%E4%BB%93%E5%BA%93%E5%9C%B0%E5%9D%80)
    - [2.通过config命令设置仓库地址](#2%E9%80%9A%E8%BF%87config%E5%91%BD%E4%BB%A4%E8%AE%BE%E7%BD%AE%E4%BB%93%E5%BA%93%E5%9C%B0%E5%9D%80)
    - [3.通过cnpm使用](#3%E9%80%9A%E8%BF%87cnpm%E4%BD%BF%E7%94%A8)
    - [4.修改.npmrc文件](#4%E4%BF%AE%E6%94%B9npmrc%E6%96%87%E4%BB%B6)

## 1.使用--registry参数指定仓库地址

```shell
npm --registry https://registry.npm.taobao.org install express
```

## 2.通过config命令设置仓库地址

```shell
npm config set registry https://registry.npm.taobao.org
```

配置后可通过下面方式来验证是否成功

```shell
npm info express
```

## 3.通过cnpm使用

```shell
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

## 4.修改.npmrc文件

在`$node_home\node_modules\npm\.npmrc`找到`.npmrc`文件,添加如下配置

```file
registry = https://registry.npm.taobao.org
```
