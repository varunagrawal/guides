# Ruby

## RVM

When installing a new Ruby with `rvm`, set the `openssl` directory to be the system one, else the Postgres `pg` gem freaks out.

```shell
rvm install <latest-version> --with-openssl-dir=/usr
```

## Bower with Rails

[This](http://joelencioni.com/blog/2014/01/03/integrating-bower-with-rails/) blog post explains how to integrate `bower` with `rails`.
