# BEAR.Sample04

BEAR.Skeleton + BEAR.Middleware 

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

2. `production` で動くように、 `bin/page.php` を修正

変更前

```php
exit((require dirname(__DIR__) . '/bootstrap.php')(PHP_SAPI === 'cli' ? 'cli-hal-app' : 'hal-app'));
```

変更後

```php
exit((require dirname(__DIR__) . '/bootstrap.php')('prod-cli-hal-app'));
```

3. リクエスト確認

```bash
php ./bin/page.php get /
```

結果

```
200 OK
Content-Type: application/hal+json

{
    "greeting": "Hello BEAR.Sunday",
    "_links": {
        "self": {
            "href": "/index"
        }
    }
}
```

4. オンデマンドでファイルが生成されたことを確認

```bash
ls -l var/tmp/prod-cli-hal-app/di/MyVendor_MyProject_Resource_Page_Index-.php
```

```
-rw-r--r-- 1 root root 270  5月 16 10:39 var/tmp/prod-cli-hal-app/di/MyVendor_MyProject_Resource_Page_Index-.php
```

5. 手動コンパイル

```bash
php ./vendor/bin/bear.compile 'MyVendor\MyProject' prod-cli-hal-app /var/www/vhosts/bear/BEAR.Sample04
```

6. 手動コンパイルでファイルが生成されたことを確認

```bash
ls -l var/tmp/prod-cli-hal-app/di/MyVendor_MyProject_Resource_Page_Index-.php
```

```
-rw-r--r-- 1 root root 270  5月 16 10:41 var/tmp/prod-cli-hal-app/di/MyVendor_MyProject_Resource_Page_Index-.php
```

7. リクエスト確認

```bash
php ./bin/page.php get /
```

8. コンパイル済みおんリソースオブジェクトのタイムスタンプが変わっている

```
-rw-r--r-- 1 root root 270  5月 16 10:42 var/tmp/prod-cli-hal-app/di/MyVendor_MyProject_Resource_Page_Index-.php
```