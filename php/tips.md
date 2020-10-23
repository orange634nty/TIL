php tips
---

## mac で php を実行したときに dyld: Library not loaded: /usr/local/opt/libiconv/lib/libiconv.2.dylib というエラーが出た

こんな感じのエラーが出ました

```
dyld: Library not loaded: /usr/local/opt/libiconv/lib/libiconv.2.dylib
  Referenced from: /usr/local/opt/php@7.1/bin/php
  Reason: Incompatible library version: php requires version 9.0.0 or later, but libiconv.2.dylib provides version 7.0.0
```

これと同様に解決した: https://stackoverflow.com/questions/52795110/php-dyld-library-not-loaded-for-libldap

```
$ brew install openldap
$ brew install libiconv
$ brew link openldap --force
$ echo 'export PATH="/usr/local/opt/openldap/bin:$PATH"' >> ~/.bashrc
$ echo 'export PATH="/usr/local/opt/openldap/sbin:$PATH"' >> ~/.bashrc
```
