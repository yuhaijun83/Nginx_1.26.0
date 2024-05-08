# Nginx_1.26.0
Nginx_1.26.0

一、Source:</br>
http://hg.nginx.org/nginx/archive/release-1.26.0.tar.gz</br>
</br>
二、Components:</br>
https://www.openssl.org/source/openssl-3.0.13.tar.gz</br>
https://zlib.net/zlib-1.3.1.tar.gz</br>
https://github.com/PCRE2Project/pcre2/releases/download/pcre2-10.39/pcre2-10.39.tar.gz</br>
</br>
三、Build Tools:</br>
https://github.com/msys2/msys2-installer/releases/download/2024-05-07/msys2-x86_64-20240507.exe</br>
https://github.com/StrawberryPerl/Perl-Dist-Strawberry/releases/download/SP_53822_64bit/strawberry-perl-5.38.2.2-64bit.msi</br>
https://www.mercurial-scm.org/release/tortoisehg/windows/tortoisehg-6.6.3-x64.msi</br>
</br>
四、Modify Source:</br>
(1).</br>
Nginx_1.26.0\auto\cc\msvc</br>
</br>
A.Line 11</br>
</br>
= # MSVC 2010 (10.0)                        cl 16.00</br>
= # MSVC 2015 (14.0)                        cl 19.00</br>
⇒</br>
= # MSVC 2010 (10.0)                        cl 16.00</br>
= # MSVC 2015 (14.0)                        cl 19.00</br>
= # MSVC 2022 (17.9.6)                      cl 19.39.33523</br>
</br>
B.Line 131</br>
</br>
= # MSVC 2005 supports C99 variadic macros</br>
= if [ "$ngx_msvc_ver" -ge 14 ]; then</br>
⇒</br>
= ngx_msvc_ver=17</br>
= # MSVC 2005 supports C99 variadic macros</br>
= if [ "$ngx_msvc_ver" -ge 14 ]; then</br>
</br>
(2).</br>
Nginx_1.26.0\src\http\modules\ngx_http_upstream_ip_hash_module.c:</br>
</br>
Line 124、Line 137</br>
</br>
iphp->addrlen = 3;</br>
⇒</br>
iphp->addrlen = 4;</br>
</br>

五、Configure:</br>
user@hostname MSYS ~/Nginx_1.26.0</br>
$ auto/configure \\</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    --with-cc=cl \\</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    --with-debug \\</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    --prefix= \\</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    --conf-path=conf/nginx.conf \\</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    --pid-path=logs/nginx.pid \\</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    --http-log-path=logs/access.log \\</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    --error-log-path=logs/error.log \\</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    --sbin-path=nginx.exe \\</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    --http-client-body-temp-path=temp/client_body_temp \\</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    --http-proxy-temp-path=temp/proxy_temp \\</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    --http-fastcgi-temp-path=temp/fastcgi_temp \\</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    --http-scgi-temp-path=temp/scgi_temp \\</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    --http-uwsgi-temp-path=temp/uwsgi_temp \\</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    --with-cc-opt=-DFD_SETSIZE=1024 \\</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    --with-pcre=objs/lib/pcre2-10.39 \\</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    --with-zlib=objs/lib/zlib-1.3.1 \\</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    --with-openssl=objs/lib/openssl-3.0.13 \\</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    --with-openssl-opt=no-asm \\</br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    --with-http_ssl_module</br>
checking for OS</br>
 + MSYS_NT-10.0-22631 3.5.3.x86_64 x86_64</br>
 + using Microsoft Visual C++ compiler</br>
 + cl version:</br>
checking for MSYS_NT-10.0-22631 specific features</br>
creating objs/Makefile</br>
</br>
Configuration summary</br>
  + using PCRE2 library: objs/lib/pcre2-10.39</br>
  + using OpenSSL library: objs/lib/openssl-3.0.13</br>
  + using zlib library: objs/lib/zlib-1.3.1</br>
</br>
  nginx path prefix: ""</br>
  nginx binary file: "/nginx.exe"</br>
  nginx modules path: "/modules"</br>
  nginx configuration prefix: "/conf"</br>
  nginx configuration file: "/conf/nginx.conf"</br>
  nginx pid file: "/logs/nginx.pid"</br>
  nginx error log file: "/logs/error.log"</br>
  nginx http access log file: "/logs/access.log"</br>
  nginx http client request body temporary files: "temp/client_body_temp"</br>
  nginx http proxy temporary files: "temp/proxy_temp"</br>
  nginx http fastcgi temporary files: "temp/fastcgi_temp"</br>
  nginx http uwsgi temporary files: "temp/uwsgi_temp"</br>
  nginx http scgi temporary files: "temp/scgi_temp"</br>
</br>
</br>
user@hostname MSYS ~/Nginx_1.26.0</br>
$</br>
</br>
六、Build:(Windows 11 Pro 23H2 + Visual Studio 2022 Enterprise)</br>
**********************************************************************</br>
** Visual Studio 2022 Developer Command Prompt v17.9.6</br>
** Copyright (c) 2022 Microsoft Corporation</br>
**********************************************************************</br>
[vcvarsall.bat] Environment initialized for: 'x86'</br>
</br>
C:\Program Files\Microsoft Visual Studio\2022\Enterprise>cd C:\msys64\home\user\Nginx_1.26.0</br>
</br>
C:\msys64\home\user\Nginx_1.26.0>nmake</br>
</br>

