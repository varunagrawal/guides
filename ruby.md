# Ruby

## RVM

When installing a new Ruby with `rvm`, set the `openssl` directory to be the system one, else the Postgres `pg` gem freaks out.

```shell
rvm install <latest-version> --with-openssl-dir=/usr
```