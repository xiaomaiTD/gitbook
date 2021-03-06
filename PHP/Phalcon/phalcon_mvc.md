# phalcon tool

1. `phalcon project {name} --type=`
2. 設定 db , 規劃好 scheme
3. 使用 `phalcon model {table_name}` 建立 model 
	- 更新 model : 
		1. 更新 db {table_name} info
		2. `phalcon model {table_name} --force`

# model 

1. 使用 model 設定的 find 進行查找動作
	- `$user  = User::find('email="max@gmail.com"');`  : 不可以有空格
	- `$email = $user[0]->email;`
	- `$this->view->postId = $email;`

# controlller

1. 測試用，關閉 view : `$this->view->disable();`，如此一來可直接看到 echo 參數
2. 選擇其他的 .volt 或其他視圖文件 : `$this->view->pick("test");`

# view

- `<?php $this->partial("index/api"); ?>` : 直接指定部份渲染

# 紀錄 log
file_put_contents('log.txt', print_r(debug_backtrace(), true), FILE_APPEND);

# 資源管理
<https://docs.phalconphp.com/zh/latest/reference/assets.html>
- css
- js

# image
<https://docs.phalconphp.com/en/latest/reference/tags.html>
1. 必須要在 controller
```
echo $this->tag->image("img/1.jpg");
```
2. 在 view
```
{{ image("img/1.jpg") }}
```

# favicon

<link rel="shortcut icon" type="image/png" href="{{ url('img/1.jpg') }}"/>


# 基本使用

## 1 
在 controller 中，`$this->view->postId = '????'`
在 view 中，無論是 phtml , volt , html 中，輸入 `<?php echo $postId; ?>` ，即可顯示

# 其他應用

- activationTemplates = template folder
	- 以 app/view 底下的 folder 為主
	- 主要以 di 註冊 view 時，註冊時的預設路徑
- default = 在該路徑下的頁面
- parameters : 帶入該頁面的參數
- function($view)

- LEVEL_LAYOUT 可以根據 https://docs.phalconphp.com/zh/latest/reference/views.html 查詢要渲染的級別 共分五級

```
return $this->view->getRender('activationTemplates', 'default', $parameters, function($view){
			$view->setRenderLevel(View::LEVEL_LAYOUT);
		});
```

# 渲染的參數使用上

{% if debug_info!=null %}
	{{ debug_info['debug_msg'] }}
{% endif%}

變數用 {{ }}
帶入邏輯用 {% %}

# json

{{ debug_info|json_encode }}

# for 迴圈

```
{% for name, value in debug_info %}		    
    {{ name|e }} => {{ value|e }}<br>
{% endfor %}
```

## view

### 觀念
phalcon 的 control 與 view 的關係
透過 `Phalcon\Mvc\Controller` 建立而成

controllers -> class IndexController -> indexAction
自動對應到
views -> index.* 的檔案

### 要在 controller 中顯示 echo / var_dump

在結尾中使用 exit 中斷 phalcon 繼續執行下去

### controller 中的變化
在 uri 中的規則是

{host}/{controller}/{action}/{arg}

所以當在 indexController 中，要找尋 testAction，則必須下
{host}/index/test

至於要給 test 參數的話，則依序放在後方

### 如何建立一個 view 的 phtml

規則為
1. 建立 controller => MapController.php
2. 建立 views/map/index.phtml

### 在 controller 中，指定要渲染的 view
$this->view->partial('map/index');
這會去找尋在 views/map/index.phtml

