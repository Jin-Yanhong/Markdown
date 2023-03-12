# jQuery tmpl

jquery.tmpl 的几种常用标签分别有：

${}, {{each}}, {{if}}, {{else}}, {{html}}

不常用标签

{{=}},{{tmpl}} and {{wrap}}.

${}等同与{{=}}是输出变量 ${}里面还可以放表达式 （=和变量之间一定要有空格，否则无效）

## {{ each }} 循环遍历数组节点

```html
<div id="div_each"></div>
<script id="each" type="text/x-jquery-tmpl">
	<h3>users</h3>
	{{each(i,user) users}}
	    <div>${i+1}:{{= user.name}}</div>
	    {{if i==0}}
	        <h4>group</h4>
	        {{each(j,group) groups}}
	            <div>${group.name}</div>
	        {{/each}}
	    {{/if}}
	{{/each}}
	<h3>depart</h3>
	{{each departs}}
	    <div>{{= $value.name}}</div>
	{{/each}}
</script>
<script type="text/javascript">
	var eachData = {
		users: [{ name: 'jerry' }, { name: 'john' }],
		groups: [{ name: 'mingdao' }, { name: 'meihua' }, { name: 'test' }],
		departs: [{ name: 'IT' }],
	};
	$('#each').tmpl(eachData).appendTo('#div_each');
</script>
```

## {{ if}} {{ else }}

```html
<div id="div_ifelse"></div>
<script id="ifelse" type="text/x-jquery-tmpl">
	<div style="margin-bottom:10px;"><span>${ID}</span><span style="margin-left:10px;">{{= Name}}</span>
	    {{if Status}}
	        <span>Status${Status}</span>
	    {{else App}}
	        <span>App${App}</span>
	    {{else}}
	        <span>None</span>
	    {{/if}}
	</div>
</script>
<script type="text/javascript">
	var users = [
		{ ID: 'think8848', Name: 'Joseph Chan', Status: 1, App: 0 },
		{ ID: 'aCloud', Name: 'Mary Cheung', App: 1 },
		{ ID: 'bMingdao', Name: 'Jerry Jin' },
	];
	$('#ifelse').tmpl(users).appendTo('#div_ifelse');
</script>
```

## {{ html }} 渲染 HTML 内容

```html
<div id="div_html"></div>
<script id="html" type="text/x-jquery-tmpl">
	<div style="margin-bottom:10px;">　　　　<span>${ID}</span>　　　　<span style="margin-left:10px;">{{= Name}}</span>
	　　${html}
	　　{{html html}}
	</div>
</script>
<script type="text/javascript">
	var user = {
		ID: 'think8848',
		Name: 'Joseph Chan',
		html: '<button>html</button>',
	};
	$('#html').tmpl(user).appendTo('#div_html');
</script>
```

## {{= }} 变量模板

## {{ tmpl }} 模板嵌套

```html
<div id="tmpl"></div>
<script id="tmpl1" type="text/x-jquery-tmpl">
	<div style="margin-bottom:10px;">
	　　<span>${ID}</span>
	　　<span style="margin-left:10px;">{{tmpl($data) '#tmpl2'}}</span>
	</div>
</script>
<script id="tmpl2" type="type/x-jquery-tmpl">
	{{each Name}}${$value}  {{/each}}
</script>
<script type="text/javascript">
	var users = [
		{ ID: 'think8848', Name: ['Joseph', 'Chan'] },
		{ ID: 'aCloud', Name: ['Mary', 'Cheung'] },
	];
	$('#tmpl1').tmpl(users).appendTo('#tmpl');
</script>
```

## {{ wrap }}

```html
<div id="wrapDemo"></div>
<script id="myTmpl" type="text/x-jquery-tmpl">
	The following wraps and reorders some HTML content:
	{{wrap "#tableWrapper"}}
	    <h3>One</h3>
	    <div>
	        First <b>content</b>
	    </div>
	    <h3>Two</h3>
	    <div>
	        And <em>more</em> <b>content</b>...
	    </div>
	{{/wrap}}
</script>
<script id="tableWrapper" type="text/x-jquery-tmpl">
	<table cellspacing="0" cellpadding="3" border="1"><tbody>
	    <tr>
	        {{each $item.html("h3", true)}}
	            <td>
	                ${$value}
	            </td>
	        {{/each}}
	    </tr>
	    <tr>
	        {{each $item.html("div")}}
	            <td>
	                {{html $value}}
	            </td>
	        {{/each}}
	    </tr>
	</tbody></table>
</script>
<script type="text/javascript">
	$(function () {
		$('#myTmpl').tmpl().appendTo('#wrapDemo');
	});
</script>
```

## $.tmpl() 用法

> **`$.tmpl(temp, data).appendTo(target)`**

> **` $(temp).tmpl(data).appendTo(target);`**

```js
let articleTemp = `
<div class="panel-heading">
    <h4>{{= title}}</h4>
    <span>{{= dateTime}}</span>
    <span>作者: {{= author}}</span>
    <span>
        <i class="iconfont icon-attentionfill"></i>
        <span id="hits"></span>
    </span>
</div>
<div class="panel-body">
    {{html contect}}
</div>
`;
// {{html XXX}} 在 此处输出 Html
export default articleTemp;
```

```html
<script type="module">
	// 使用 文章模板
	import articleTemp from '/template/article/content.js';
	$(document).ready(function () {
		let articleData = {
			title: '购物流程',
			author: 'FSD',
			dateTime: '2019-06-28 00:00:25',
			// 富文本
			contect: `<p></p>`,
		};
		//
		$.tmpl(articleTemp, articleData).appendTo('.article-content');
	});
</script>
```
