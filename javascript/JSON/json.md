## JSON

- JSON字符串化：JSON.stringify(..)将JSON对象序列化为字符串（在转换为字符串时调用了toString()方法）
  - 所有安全的JSON值（JSON-sage）都可以使用JSON.stringiffy(..)字符化。安全的JSON值是指能够呈现为有效的JSON格式的值。
  - 不安全的JSON值：undefined、function、symbol和包含循环引用（对象之间相互引用，形成一个无限循环）的对象都不符合JSON结构标准，其他支持JSON的语言无法处理它们
  - JSON.stringify(..)在对象中遇到undefined、function和symbol时会自动将其忽略，在数组中则会返回null（以保证单元位置不变）