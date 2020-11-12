---
layout:     post   				    # 使用的布局（不需要改）
title:      OpenResty测试框架使用    # 标题
subtitle:                           #副标题
date:       2020-11-12 				# 时间
author:     DYD 				    # 作者
header-img: img/post-bg-debug.png 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - OpenResty
---

[春哥自己写的说明文档](https://openresty.gitbooks.io/programming-openresty/content/testing/)

上边的文档说的比较清楚，有时间可以看下。

---
自己实践

```bash
#安装测试框架
sudo cpan Test::Nginx
```


- 我使用zsh，使用bash的把zsh换成bash
- openresty目录没有使用默认，在/opt/openresty

go.sh脚本
```bash
#!/usr/bin/env zsh

export PATH=/opt/openresty/nginx/sbin:$PATH

exec prove "$@"
```

```bash
#创建t目录
mkdir t
```

最简单的测试用例001-test.t
```bash
use Test::Nginx::Socket 'no_plan';

run_tests();

__DATA__

=== TEST 1: hello, world
This is just a simple demonstration of the
echo directive provided by ngx_http_echo_module.

--- config
location = /t {
    echo "hello, world!";
}

--- request
GET /t

--- response_body
hello, world!

--- error_code: 200

```
002-test.t
```bash
use Test::Nginx::Socket 'no_plan';

run_tests();

__DATA__
=== TEST 1: dying in init_by_lua_block
--- http_config
    init_by_lua_block {
        error("I am dying!")
    }
--- config
--- must_die
--- error_log
I am dying!
```

```bash
#执行测试
./go.sh t/*.t

#verbose模式输出
./go.sh -v t/

#指定单个文件
./go.sh t/001-test.t

#递归测试
./go.sh -r 
```

```bash
t/001-test.t .. ok
t/002-test.t .. nginx: [error] init_by_lua error: init_by_lua:2: I am dying!
stack traceback:
        [C]: in function 'error'
        init_by_lua:2: in main chunk
t/002-test.t .. ok
All tests successful.
Files=2, Tests=4,  2 wallclock secs ( 0.03 usr  0.11 sys +  0.57 cusr  0.50 csys =  1.21 CPU)
Result: PASS
```