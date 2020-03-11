# PHP 代码规范

## 一、基本约定

### 1. 源文件

1. 纯 PHP 代码源文件只使用 `<?php` 标签，省略关闭标签 `?>`；
2. 源文件中 PHP 代码的编码格式必须是 无 BOM 的 UTF-8 格式；
3. 使用 Unix LF 作为行结束符；
4. 一个源文件只做一种类型的声明，即，文件 A.php 专门用来声明 Class，文件 B.php 专门用来设置配置信息，不允许混用；

### 2. 缩进

使用制表符来缩进，每个制表符长度设置为 4 个空格；

### 3. 行

单行推荐最多书写 120 个字符，多于这个字符数就应该换行书写；

### 4. 关键字 和 True / False / Null

PHP 的 关键字 必须小写，boolean 值：true、false、null 也必须小写；
以下是 PHP 的 关键字：

```
'__halt_compiler', 'abstract', 'and', 'array', 'as', 'break', 'callable', 'case', 'catch', 'class', 'clone', 'const', 'continue', 'declare', 'default', 'die', 'do', 'echo', 'else', 'elseif', 'empty', 'enddeclare', 'endfor', 'endforeach', 'endif', 'endswitch', 'endwhile', 'eval', 'exit', 'extends', 'final', 'for', 'foreach', 'function', 'global', 'goto', 'if', 'implements', 'include', 'include_once', 'instanceof', 'insteadof', 'interface', 'isset', 'list', 'namespace', 'new', 'or', 'print', 'private', 'protected', 'public', 'require', 'require_once', 'return', 'static', 'switch', 'throw', 'trait', 'try', 'unset', 'use', 'var', 'while', 'xor'
```

### 5. 命名

1. 类 使用 大驼峰（*StudlyCaps*）命名法 命名，如 `SampleClass`；

2. 类属性
	
	- `public`、`protected` 类型的，使用 小驼峰（*camelCase*）命名法 命名；
	
	- `private` 类型的，以 下划线 开头，使用 小驼峰（*camelCase*）命名法 命名；

3. 类方法
	
	- `public`、`protected` 类型的，使用 小驼峰（*camelCase*）命名法 命名；
	
	- `private` 类型的，以 下划线 开头，使用 小驼峰（*camelCase*）命名法 命名；

4. 类方法参数 使用 小驼峰（*camelCase*）命名法 命名；

5. 函数 使用 小写字母 + 下划线 命名，如 `function sample_func();`；

6. 函数参数 使用 小驼峰（*camelCase*）命名法 命名；

7. 变量 使用 小驼峰（*camelCase*）命名法 命名，如 `$camelCase`；

8. 常量 使用 大写字母 + 下划线 命名，如 `SAMPLE_CONSTANT`；

### 6. 代码注释标签

如 函数注释、变量注释 等，必须遵守 [phpDocument 标签规则](https://docs.phpdoc.org/latest/references/phpdoc/tags/index.html "phpDocument Tag reference")，不允许创造新的标签；

### 7. 业务模块

1. 涉及到多个数据表 更新 / 添加 操作时，最外层要用 事务，保证数据库操作的原子性；

2. Model 层只做简单的数据表的查询；

3. 业务逻辑统一封装到 Logic 层；

4. 控制器只做 URL 路由，不当作 业务方法 调用；

5. 控制器层不能出现 SQL 操作语句，如 ThinkPHP 框架的 `where()`、`order()` 等模型方法，即，控制器中不允许出现类似这样的 SQL 语句：`D('XXX')->where()->order()->limit()->find();`，`where()`、`order()`、`limit()` 等 SQL 方法只能出现在 Model 层、业务层；

## 二、代码样式风格

### 1. 命名空间（*Namespace*）和 导入（*Use*）声明

1. 命名空间（*Namespace*）的声明下方必须空一行；

2. 所有的 导入（*Use*）声明必须放在 命名空间（*Namespace*）声明的下方；

3. 一句声明中，必须只有一个 导入（*Use*）关键字；

4. 在 导入（*Use*）声明代码块下方必须空一行；

	```php
	<?php
	namespace Lib\Databases; // 下方必须空一行
	
	class Mysql {
		
	}
	```
	
	namespace 下方空一行，才能使用 use，再空一行，才能声明 class；
	
	```php
	<?php
	namespace Lib\Databases; // 下方必须空一行
	
	use FooInterface; // use 必须在 namespace 下方声明
	use BarClass as Bar;
	use OtherVendor\OtherPackage\BazClass; // 下方必须空一行
	
	class Mysql {
		
	}
	```

### 2. 类（*class*）、属性（*property*）和 方法（*method*）声明

1. 继承（*extends*）和 实现（*implements*）必须和 类名（*class name*）写在同一行；
	
	```php
	<?php
	namespace Lib\Database;
	
	class Mysql extends ParentClass implements \PDO, \DB { // 写在同一行
		
	}
	```

2. 属性（*property*）必须声明其可见性，到底是 `public` 还是 `protected` 还是 `private`，不能省略，也不能使用 `var`，`var` 是 PHP 老版本中的方式，等同于 `public`；
	
	```php
	<?php
	namespace Lib\Database;
	
	class Mysql extends ParentClass implements \PDO, \DB { // 写在同一行
		public $foo = null;
		private $name = 'name';
		protected $age = '18';
	}
	```

3. 方法（*method*），必须声明其可见性，到底是 `public` 还是 `protected` 还是 `private`，不能省略；如果有多个参数，第一个参数后紧接 ","，再加一个空格：`function_name ($par, $par2, $pa3)`；如果参数有默认值，"=" 左右各有一个空格分开；
	
	```php
	<?php
	namespace Lib\Databaes;
	
	class Mysql extends ParentClass implements \PDO, \DB { // 写在同一行
		public getInfo($name, $age, $gender = 1) { // 参数之间有一个空格，默认参数的 "=" 左右各有一个空格，")" 与 "{" 之间有一个空格
			
		}
	}
	```

4. 当用到 抽象（*abstract*）和 终结（*final*）来做类声明时，它们必须放在可见性声明（public或 protected 或 private）的左方；而当用到 静态（*static*）来做类声明时，则必须放在可见性声明的右方；
	
	```php
	<?php
	namespace Vendor\Package;
	
	abstract class ClassName {
		protected static $foo; // static 放右方
		abstract protected function zim(); // abstract 放左方
		
		final public static function bar() { // final 放左方，static 放右方
			// 方法主体部分
		}
	}
	```

### 3. 控制结构

1. `if`、`elseif`、`else` 的规范写法
	
	```php
	<?php
	if ($expr1) { // if 与 "(" 之间有一个空格，")" 与 "{" 之间有一个空格
		
	} elseif ($expr2) { // elesif 连写，与 "(" 之间有一个空格，")" 与 "{" 之间有一个空格
		
	} else { // else 左右各有一个空格
		
	}
	```

2. `switch`、`case` 的规范写法
	
	```php
	<?php
	switch ($expr) { // switch 与 "(" 之间有一个空格，")" 与 "{" 之间有一个空格
		case 0:
			echo 'First case, with a break'; // 对齐
			break; // break 换行书写，并对齐
		case 1:
			echo 'Second case, which falls through';
			// no break
		case 2:
		case 3:
		case 4:
			echo 'Third case, return instead of break';
			return;
		default:
			echo 'Default case';
			break;
	}
	```

3. `while`、`do while` 的规范写法
	
	```php
	<?php
	while ($expr) { // while 与 "(" 之间有一个空格， ")" 与 "{" 之间有一个空格
		
	}
	
	do { // do 与 "{" 之间有一个空格
		
	} while ($expr); // while 左右各有一个空格
	```

4. `for` 的规范写法
	
	```php
	<?php
	for ($i = 0; $i < 10; $i++) { // for 与 "(" 之间有一个空格，二元操作符 "="、"<" 左右各有一个空格，")" 与 "{" 之间有一个空格
		
	}
	```

5. `foreach` 的规范写法
	
	```php
	<?php
	foreach ($iterable as $key => $value) { // foreach 与 "(" 之间有一个空格，"=>" 左右各有一个空格，) 与 { 之间有一个空格
		
	}
	```

6. `try catch` 的规范写法
	
	```php
	try { // try 右方有一个空格
		
	} catch (FirstExceptionType $e) { // catch 与 "(" 之间有一个空格，")" 与 "{" 之间有一个空格
		
	} catch (OtherExceptionType $e) { // catch 与 "(" 之间有一个空格，")" 与 "{" 之间有一个空格
		
	}
	```

7. `array` 的规范写法
	
	只有一个键值对时，写成一行；
	
	```php
	$where = array('id' => 123);
	```
	
	有多个（二个或二个以上）键值对时，写成多行；
	
	```php
	$where = array(
		'id' => 123,
		'user_name' => 'xiaoxi'
	);
	```

### 4. 注释

1. 行注释
	
	- "//" 后方需要加一个空格；
	
	- 如果 "//" 左方有非空字符，则 "//" 左方需要加一个空格；

2. 函数注释
	
	- 参数名、属性名、标签的文本 上下要对齐；
	
	- 第一个标签上方必须空一行；
	
	```php
	<?php
	/**
	 * This is a sample function to illustrate additional PHP
	 * formatter options.
	 *
	 * @param        $one   The first parameter
	 * @param int    $two   The second parameter
	 * @param string $three The third parameter with a longer
	 *                      comment to illustrate wrapping.
	 * @return void
	 * @author  soraharu.com
	 * @license GPL
	 */
	function foo($one, $two = 0, $three = "String") {
		
	}
	```

### 5. 空格

1. 赋值操作符（=、+= 等）、逻辑操作符（&&、||）、等号操作符（==、!=）、关系运算符（<、>、<=、>=）、按位操作符（&、|、^）、连接符（.）左右各有一个空格；

2. `if`、`else`、`elseif`、`while`、`do`、`switch`、`for`、`foreach`、`try`、`catch`、`finally` 等，与紧挨的左括号 "(" 之间有一个空格；

3. 函数、方法的各个参数之间，逗号 "," 后面有一个空格；

### 6. 空行

1. 所有左花括号 "{" 都不换行，并且 "{" 紧挨着的下方一定不是空行；

2. 同级代码（缩进相同）的注释（行注释 / 块注释）左方必须有一个空行；

3. 各个 方法 / 函数 之间有一个空行；

4. namespace 语句、use 语句、 class 语句 之间有一个空行；

5. return 语句
	
	- 如果 return 语句 之前只有一行 PHP 代码，return 语句 之前不需要空行；
	
	- 如果 return 语句 之前有至少二行 PHP 代码，return 语句上方必须空一行；

6. `if`、`while`、`switch`、`for`、`foreach`、`try` 等代码块之间以及与其他代码之间必须空一行；