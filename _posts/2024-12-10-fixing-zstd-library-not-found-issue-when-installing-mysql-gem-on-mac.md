---
layout: post
title: Fixing zstd library not found issue when installing mysql gem on mac
date: 2024-12-10
---

I mostly work with mysql with my rails app and recently when I tried installing mysql gem to my project, I got an error with the following detail.

‌

```
Gem::Ext::BuildError: ERROR: Failed to build gem native extension.

    current directory: /Users/workstation/.rbenv/versions/3.2.2/lib/ruby/gems/3.2.0/gems/mysql2-0.5.6/ext/mysql2
/Users/workstation/.rbenv/versions/3.2.2/bin/ruby extconf.rb
checking for rb_absint_size()... yes
checking for rb_absint_singlebit_p()... yes
checking for rb_gc_mark_movable()... yes
checking for rb_wait_for_single_fd()... yes
checking for rb_enc_interned_str() in ruby.h... yes
-----
Using --with-openssl-dir=/opt/homebrew/opt/openssl@3
-----
-----
Using mysql_config at /opt/homebrew/bin/mysql_config
-----
checking for mysql.h... yes
checking for errmsg.h... yes
checking for SSL_MODE_DISABLED in mysql.h... yes
checking for SSL_MODE_PREFERRED in mysql.h... yes
checking for SSL_MODE_REQUIRED in mysql.h... yes
checking for SSL_MODE_VERIFY_CA in mysql.h... yes
checking for SSL_MODE_VERIFY_IDENTITY in mysql.h... yes
checking for MYSQL.net.vio in mysql.h... yes
checking for MYSQL.net.pvio in mysql.h... no
checking for MYSQL_DEFAULT_AUTH in mysql.h... yes
checking for MYSQL_ENABLE_CLEARTEXT_PLUGIN in mysql.h... yes
checking for SERVER_QUERY_NO_GOOD_INDEX_USED in mysql.h... yes
checking for SERVER_QUERY_NO_INDEX_USED in mysql.h... yes
checking for SERVER_QUERY_WAS_SLOW in mysql.h... yes
checking for MYSQL_OPTION_MULTI_STATEMENTS_ON in mysql.h... yes
checking for MYSQL_OPTION_MULTI_STATEMENTS_OFF in mysql.h... yes
checking for my_bool in mysql.h... no
checking for mysql_ssl_set() in mysql.h... no
-----
Don't know how to set rpath on your system, if MySQL libraries are not in path mysql2 may not load
-----
-----
Setting libpath to /opt/homebrew/Cellar/mysql/9.0.1_4/lib
-----
creating Makefile

current directory: /Users/workstation/.rbenv/versions/3.2.2/lib/ruby/gems/3.2.0/gems/mysql2-0.5.6/ext/mysql2
make DESTDIR\= sitearchdir\=./.gem.20241210-15583-19z5n1 sitelibdir\=./.gem.20241210-15583-19z5n1 clean

current directory: /Users/workstation/.rbenv/versions/3.2.2/lib/ruby/gems/3.2.0/gems/mysql2-0.5.6/ext/mysql2
make DESTDIR\= sitearchdir\=./.gem.20241210-15583-19z5n1 sitelibdir\=./.gem.20241210-15583-19z5n1
compiling client.c
In file included from client.c:15:
./mysql_enc_name_to_ruby.h:43:1: warning: a function definition without a prototype is deprecated in all versions of C and is
not supported in C2x [-Wdeprecated-non-prototype]
mysql2_mysql_enc_name_to_rb_hash (str, len)
^
./mysql_enc_name_to_ruby.h:86:1: warning: a function definition without a prototype is deprecated in all versions of C and is
not supported in C2x [-Wdeprecated-non-prototype]
mysql2_mysql_enc_name_to_rb (str, len)
^
2 warnings generated.
compiling infile.c
compiling mysql2_ext.c
compiling result.c
result.c:304:35: warning: implicit conversion loses integer precision: 'unsigned long' to 'int' [-Wshorten-64-to-32]
        precision = field->length - (field->decimals > 0 ? 2 : 1);
                  ~ ~~~~~~~~~~~~~~^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
1 warning generated.
compiling statement.c
linking shared-object mysql2/mysql2.bundle
ld: warning: ignoring duplicate libraries: '-lruby.3.2'
ld: library 'zstd' not found
clang: error: linker command failed with exit code 1 (use -v to see invocation)
make: *** [mysql2.bundle] Error 1

make failed, exit code 2

Gem files will remain installed in /Users/workstation/.rbenv/versions/3.2.2/lib/ruby/gems/3.2.0/gems/mysql2-0.5.6 for
inspection.
Results logged to
/Users/workstation/.rbenv/versions/3.2.2/lib/ruby/gems/3.2.0/extensions/arm64-darwin-24/3.2.0/mysql2-0.5.6/gem_make.out

  /Users/workstation/.rbenv/versions/3.2.2/lib/ruby/3.2.0/rubygems/ext/builder.rb:119:in `run'
  /Users/workstation/.rbenv/versions/3.2.2/lib/ruby/3.2.0/rubygems/ext/builder.rb:51:in `block in make'
  /Users/workstation/.rbenv/versions/3.2.2/lib/ruby/3.2.0/rubygems/ext/builder.rb:43:in `each'
  /Users/workstation/.rbenv/versions/3.2.2/lib/ruby/3.2.0/rubygems/ext/builder.rb:43:in `make'
  /Users/workstation/.rbenv/versions/3.2.2/lib/ruby/3.2.0/rubygems/ext/ext_conf_builder.rb:41:in `build'
  /Users/workstation/.rbenv/versions/3.2.2/lib/ruby/3.2.0/rubygems/ext/builder.rb:187:in `build_extension'
  /Users/workstation/.rbenv/versions/3.2.2/lib/ruby/3.2.0/rubygems/ext/builder.rb:221:in `block in build_extensions'
  /Users/workstation/.rbenv/versions/3.2.2/lib/ruby/3.2.0/rubygems/ext/builder.rb:218:in `each'
  /Users/workstation/.rbenv/versions/3.2.2/lib/ruby/3.2.0/rubygems/ext/builder.rb:218:in `build_extensions'
  /Users/workstation/.rbenv/versions/3.2.2/lib/ruby/3.2.0/rubygems/installer.rb:843:in `build_extensions'
/Users/workstation/.rbenv/versions/3.2.2/lib/ruby/gems/3.2.0/gems/bundler-2.4.13/lib/bundler/rubygems_gem_installer.rb:72:in
`build_extensions'
/Users/workstation/.rbenv/versions/3.2.2/lib/ruby/gems/3.2.0/gems/bundler-2.4.13/lib/bundler/rubygems_gem_installer.rb:28:in
`install'
/Users/workstation/.rbenv/versions/3.2.2/lib/ruby/gems/3.2.0/gems/bundler-2.4.13/lib/bundler/source/rubygems.rb:198:in
`install'
/Users/workstation/.rbenv/versions/3.2.2/lib/ruby/gems/3.2.0/gems/bundler-2.4.13/lib/bundler/installer/gem_installer.rb:54:in
`install'
/Users/workstation/.rbenv/versions/3.2.2/lib/ruby/gems/3.2.0/gems/bundler-2.4.13/lib/bundler/installer/gem_installer.rb:16:in
`install_from_spec'
/Users/workstation/.rbenv/versions/3.2.2/lib/ruby/gems/3.2.0/gems/bundler-2.4.13/lib/bundler/installer/parallel_installer.rb:156:in
`do_install'
/Users/workstation/.rbenv/versions/3.2.2/lib/ruby/gems/3.2.0/gems/bundler-2.4.13/lib/bundler/installer/parallel_installer.rb:147:in
`block in worker_pool'
  /Users/workstation/.rbenv/versions/3.2.2/lib/ruby/gems/3.2.0/gems/bundler-2.4.13/lib/bundler/worker.rb:62:in `apply_func'
/Users/workstation/.rbenv/versions/3.2.2/lib/ruby/gems/3.2.0/gems/bundler-2.4.13/lib/bundler/worker.rb:57:in `block in
process_queue'
  /Users/workstation/.rbenv/versions/3.2.2/lib/ruby/gems/3.2.0/gems/bundler-2.4.13/lib/bundler/worker.rb:54:in `loop'
  /Users/workstation/.rbenv/versions/3.2.2/lib/ruby/gems/3.2.0/gems/bundler-2.4.13/lib/bundler/worker.rb:54:in `process_queue'
/Users/workstation/.rbenv/versions/3.2.2/lib/ruby/gems/3.2.0/gems/bundler-2.4.13/lib/bundler/worker.rb:90:in `block (2
levels) in create_threads'

An error occurred while installing mysql2 (0.5.6), and Bundler cannot continue.

In Gemfile:
  mysql2
```

 As you can see, the error is mentioning that it wasn’t able to find zstd library in this line

‌

```
ld: library 'zstd' not found
clang: error: linker command failed with exit code 1 (use -v to see invocation)
make: *** [mysql2.bundle] Error 1
```

zstd is an compression library which was actually installed in my mac. But gem installer couldn’t find it by default. So to fix the error, the solution i used is give the path when installing the gem

‌

Solution:

```
gem install mysql2 -v '0.5.6' -- --with-opt-dir=$(brew --prefix openssl) --with-ldflags=-L/opt/homebrew/opt/zstd/lib
```
        