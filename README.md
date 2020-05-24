# BEAR.Sample04

手動コンパイルしたリソースオブジェクトが再生成される現象

## 手順

1. BEAR.Sunday の雛形をインストール

```bash
composer create-project -n bear/skeleton BEAR.Sample04 --no-dev
```

結果

```
Installing bear/skeleton (1.7.5)
  - Installing bear/skeleton (1.7.5): Downloading (100%)
Created project in BEAR.Sample04
```

2. リクエスト確認

```bash
curl http://localhost
```

実行結果

```json
{
    "greeting": "Hello BEAR.Sunday",
    "_links": {
        "self": {
            "href": "/index"
        }
    }
}
```

3. オンデマンドコンパイルでファイルが生成されたことを確認

```bash
ls -la var/tmp/prod-hal-app/di/
```

実行結果

```
-rw-r--r-- 1 apache apache    141  5月 24 15:54 BEAR_Package_Provide_Router_HttpMethodParamsInterface-.php
-rw-r--r-- 1 apache apache    169  5月 24 15:54 BEAR_Resource_HalLink-.php
-rw-r--r-- 1 apache apache    214  5月 24 15:54 BEAR_Resource_RenderInterface-.php
-rw-r--r-- 1 apache apache    213  5月 24 15:54 BEAR_Resource_ReverseLinkInterface-.php
-rw-r--r-- 1 apache apache    221  5月 24 15:54 BEAR_Sunday_Extension_Router_RouterInterface-.php
-rw-r--r-- 1 apache apache    338  5月 24 15:54 Doctrine_Common_Annotations_Reader-.php
-rw-r--r-- 1 apache apache    145  5月 24 15:54 Doctrine_Common_Annotations_Reader-annotation_reader.php
-rw-r--r-- 1 apache apache    455  5月 24 15:54 Doctrine_Common_Cache_Cache-.php
-rw-r--r-- 1 apache apache    270  5月 24 15:54 MyVendor_MyProject_Resource_Page_Index-.php
-rw-r--r-- 1 apache apache 879548  5月 24 15:54 aop.txt
-rw-r--r-- 1 apache apache 964251  5月 24 15:54 module.txt
```

4. 手動コンパイル

```bash
php ./vendor/bin/bear.compile 'MyVendor\MyProject' prod-hal-app /var/www/vhosts/bear/BEAR.Sample04
```

実行結果

```

Compile Log: /var/www/vhosts/bear/BEAR.Sample04/var/log/prod-hal-app/compile.log
autoload.php: /var/www/vhosts/bear/BEAR.Sample04/autoload.php
preload.php: /var/www/vhosts/bear/BEAR.Sample04/preload.php
```

5. 手動コンパイルでファイルが生成されたことを確認

```bash
ls -l var/tmp/prod-hal-app/di/
```

実行結果

```
-rw-r--r-- 1 root root    141  5月 24 15:58 BEAR_Package_Provide_Router_HttpMethodParamsInterface-.php
-rw-r--r-- 1 root root    169  5月 24 15:58 BEAR_Resource_HalLink-.php
-rw-r--r-- 1 root root    291  5月 24 15:58 BEAR_Resource_NamedParamMetasInterface-.php
-rw-r--r-- 1 root root    192  5月 24 15:58 BEAR_Resource_NamedParameterInterface-.php
-rw-r--r-- 1 root root    214  5月 24 15:58 BEAR_Resource_RenderInterface-.php
-rw-r--r-- 1 root root    213  5月 24 15:58 BEAR_Resource_ReverseLinkInterface-.php
-rw-r--r-- 1 root root    221  5月 24 15:58 BEAR_Sunday_Extension_Router_RouterInterface-.php
-rw-r--r-- 1 root root    196  5月 24 15:58 Doctrine_Common_Annotations_AnnotationReader-.php
-rw-r--r-- 1 root root    134  5月 24 15:58 Doctrine_Common_Annotations_DocParser-.php
-rw-r--r-- 1 root root    338  5月 24 15:58 Doctrine_Common_Annotations_Reader-.php
-rw-r--r-- 1 root root    196  5月 24 15:58 Doctrine_Common_Annotations_Reader-annotation_reader.php
-rw-r--r-- 1 root root    445  5月 24 15:58 Doctrine_Common_Cache_Cache-.php
-rw-r--r-- 1 root root    270  5月 24 15:58 MyVendor_MyProject_Resource_Page_Index-.php
-rw-r--r-- 1 root root 879548  5月 24 15:58 aop.txt
-rw-r--r-- 1 root root 195020  5月 24 15:58 module.txt
```

6. 再度、リクエスト確認

```bash
curl http://localhost
```

実行結果

```json
{
    "greeting": "Hello BEAR.Sunday",
    "_links": {
        "self": {
            "href": "/index"
        }
    }
}
```

~~7. 4番でコンパイルしたリソースオブジェクトのタイムスタンプが変わっている~~

7. 4番でコンパイルしたファイルのタイムスタンプから更新されていない

```bash
ls -l var/tmp/prod-hal-app/di/
```

```
-rw-r--r-- 1 root root    141  5月 24 15:58 BEAR_Package_Provide_Router_HttpMethodParamsInterface-.php
-rw-r--r-- 1 root root    169  5月 24 15:58 BEAR_Resource_HalLink-.php
-rw-r--r-- 1 root root    291  5月 24 15:58 BEAR_Resource_NamedParamMetasInterface-.php
-rw-r--r-- 1 root root    192  5月 24 15:58 BEAR_Resource_NamedParameterInterface-.php
-rw-r--r-- 1 root root    214  5月 24 15:58 BEAR_Resource_RenderInterface-.php
-rw-r--r-- 1 root root    213  5月 24 15:58 BEAR_Resource_ReverseLinkInterface-.php
-rw-r--r-- 1 root root    221  5月 24 15:58 BEAR_Sunday_Extension_Router_RouterInterface-.php
-rw-r--r-- 1 root root    196  5月 24 15:58 Doctrine_Common_Annotations_AnnotationReader-.php
-rw-r--r-- 1 root root    134  5月 24 15:58 Doctrine_Common_Annotations_DocParser-.php
-rw-r--r-- 1 root root    338  5月 24 15:58 Doctrine_Common_Annotations_Reader-.php
-rw-r--r-- 1 root root    196  5月 24 15:58 Doctrine_Common_Annotations_Reader-annotation_reader.php
-rw-r--r-- 1 root root    445  5月 24 15:58 Doctrine_Common_Cache_Cache-.php
-rw-r--r-- 1 root root    270  5月 24 15:58 MyVendor_MyProject_Resource_Page_Index-.php
-rw-r--r-- 1 root root 879548  5月 24 15:58 aop.txt
-rw-r--r-- 1 root root 195020  5月 24 15:58 module.txt
```