# Curl library build for dockzen-launcher  
> Dockzen-launcher uses curl library to communicate with docker daemon  
> Refer the build options to make static libraries  
> Souce is based on Ver.7.54.1  
## for arm (Cross Build - static library)  
<pre>
curl$ ./buildconf
curl$ ./configure --without-ssl --without-zlib --enable-shared=no --enable-static=yes --prefix=$(pwd)/install/arm --build=x86_64-linux --host=arm-linux-gnueabi CC=arm-linux-gnueabi-gcc
curl$ make
curl$ make install
</pre>      
### outputs
<pre>
install
├── arm
    ├── bin
    │   └── curl
    ├── include
    │   └── curl
    │       ├── curl.h
    │       ├── curlrules.h
    │       ├── curlver.h
    │       ├── easy.h
    │       ├── mprintf.h
    │       ├── multi.h
    │       ├── stdcheaders.h
    │       ├── system.h
    │       └── typecheck-gcc.h
    └── lib
        └── pkgconfig
</pre> 

## for amd64 (install curl library into Linux Host PC)  
<pre>
curl$ ./buildconf
curl$ ./configure
curl$ make
curl$ sudo make install
</pre>      
  
## Errata
### 1. Refer different header files relative to ARCH    
You may experience build error if you use legacy installed library.  
It is caused from different architecture of 32bit and 64bit  
So, you can't do arm cross build in host pc of amd64
<pre>
$ arm-linux-gnueabi-gcc ...
In file included from /usr/include/curl/curl.h:35:0,
	from rest-curl.c:3:
	/usr/include/curl/curlrules.h:142:3: error: size of array ‘__curl_rule_01__’ is negative
	__curl_rule_01__
	^
	/usr/include/curl/curlrules.h:152:3: error: size of array ‘__curl_rule_02__’ is negative
	__curl_rule_02__
</pre>
As like above, the header files are generated relative to ARCH in build time.  
<br>
<br>
### 2. <amd64> after installation, git push can be broken.    
You may experience build error if you use legacy installed library.  
It is caused from different architecture of 32bit and 64bit  
So, you can't do arm cross build in host pc of amd64
<pre>
$ git push origin xxx 
git-remote-https: error while loading shared libraries: libcurl-gnutls.so.4: cannot open shared object file: No such file or directory
</pre>
As like above, libcurl-gnutls doesn't exist.. it may be removed..  
libcurl-gnutls should be installed manually as belows
<pre>
$ apt-get download libcurl3-gnutls
$ sudo dpkg -i libcurl3-gnutls_7.47.0-1ubuntu2.2_amd64.deb
</pre>
<br>
<br>
 
