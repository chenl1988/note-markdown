# ES6规范不建议用new来追寻基本类型的包装类

- "1".toString();为什么可以调用，这个语句运行过程中做了这样几件事情
  - var s = new Object("1");
  - s.toString();
  - s = null;

  - 第一步创建Object类实例。而不是String，由于Symbol和BigInt的出现，对它们调用new都会报错，目前ES6规范也不建议用new来创建基本类型的包装类
  - 调用实例方法
  - 执行完方法立即销毁这个实例

- 整个过程体现了基本包装类型的性质