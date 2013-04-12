# Basic Auth Module by mod_mruby

Basic Auth Moudle using mod_mruby

## How to Use

- Copy conf

```
cp mod_mruby_basic_auth.conf ${HTTPD_ROOT}/conf.d/.
```

- Change mod_mruby_basic_auth.conf for you

```
<IfModule mruby_module>
#  <Location /basic/>
#    AuthType basic
#    AuthName "Message for clients"
#    AuthBasicProvider mruby
#    mrubyAuthnCheckPassword /path/to/mruby_basic_auth.rb
#    require valid-user
#  </Location>
</IfModule>
```

- Change /path/to/mruby_basic_auth.rb for you

```
user_list = {
  "bilbo" => "foo",
  "frodo" => "bar",
  "samwise" => "baz",
  "aragorn" => "qux",
  "legolas" => "quux",
  "gimli" => "corge",
}

anp = Apache::AuthnProvider.new

if user_list[anp.user] == anp.password
  Apache.return(Apache::AuthnProvider::AUTH_GRANTED)
else
  Apache.return(Apache::AuthnProvider::AUTH_DENIED)
end
```

- httpd restart

```
service httpd restart
```
