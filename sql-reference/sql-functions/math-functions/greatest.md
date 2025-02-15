# greatest

## 功能

返回多个输入参数中的最大值。

通常情况下，返回值的数据类型与输入值相同。

该函数进行对比时遵循以下原则：

- 如果任何一个输入参数为 NULL，则返回 NULL。

- 如果输入参数中有 DOUBLE 类型的值，则所有值按照 DOUBLE 类型进行比较，并返回 DOUBLE 类型的值。DECIMAL 和 FLOAT 类型也遵循相同规则。

- 如果输入参数中既有数值类型又有字符串类型，且字符串可以转换为数值，则按照数值类型进行比较。如果字符串无法转换为数值，则按照字符串类型进行比较。

- 如果输入参数全部为字符类型，则按照每个参数的首字母在字母表中的先后顺序进行比较。

## 语法

```Haskell
greatest(expr1,...);
```

## 参数说明

`expr1`: 支持的数据类型为 SMALLINT、TINYINT、INT、BIGINT、LARGEINT、FLOAT、DOUBLE、DECIMALV2、DECIMAL32、DECIMAL64、DECIMAL128、DATETIME、VARCHAR。

## 示例

示例一：输入值为单值。

```Plain
select greatest(3);
+-------------+
| greatest(3) |
+-------------+
|           3 |
+-------------+
1 row in set (0.01 sec)
```

示例二：返回一组数值中的最大值。

```Plain
select greatest(3,4,5,5,6);
+-------------------------+
| greatest(3, 4, 5, 5, 6) |
+-------------------------+
|                       6 |
+-------------------------+
1 row in set (0.00 sec)
```

示例三：输入值中包含 DOUBLE 类型值，所有值按照 DOUBLE 类型进行比较，并返回 DOUBLE 类型的值。

```Plain
select greatest(7,4.5);
+------------------+
| greatest(7, 4.5) |
+------------------+
|              7.0 |
+------------------+
1 row in set (0.05 sec)
```

示例四：输入值包含数值和字符串类型且字符串可以转换为数值，按照数值进行比较。

```Plain
select greatest(7,'9');
+------------------+
| greatest(7, '9') |
+------------------+
| 9                |
+------------------+
1 row in set (0.04 sec)
```

示例五：输入值包含数值和字符串类型且字符串**不可以**转换为数值，按照字符串进行比较。字符串 `'1'` 小于`'at'`。

```SQL
select greatest(1,'at');
+-------------------+
| greatest(1, 'at') |
+-------------------+
| at                |
+-------------------+
```

示例六：输入值全部为字符型，最大值为字母表最后一位 `Z`。

```Plain
select greatest('A','B','Z');
+-------------------------+
| greatest('A', 'B', 'Z') |
+-------------------------+
| Z                       |
+-------------------------+
1 row in set (0.00 sec)
```
