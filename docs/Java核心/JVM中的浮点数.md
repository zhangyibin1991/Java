摘自《Java虚拟机规范(Java SE8版)》 2.3.2浮点类型、取值集合及浮点值<p/>
  <p style="text-indent:2em;">浮点类型包含<code>float</code>类型和<code>double</code>类型两种，他们在概念上与《IEEE Standard for Binary Floating-Point Arithmetic》(ANSI/IEEE Std.754-1985, New York)标准中定义的32位单精度和64位双精度IEEE-754格式的取值与操作是一致的。</p>
  <p style="text-indent:2em;"><u>IEEE 754 标准的内容不仅包括了正负的带符号量（sign-magnitude number），而且包括了正负零、正负无穷大的一个特殊的“非数字”标识（Not-a-Number，下午用NaN表示）。</u>NaN值用于表示某些无效的运算操作，例如除以0等情况。</p>
  <p style="text-indent:2em;">所有Java虚拟机的实现都必须支持两种标准的浮点数集合：<strong>单精度浮点数集合</strong>和<strong>双精度浮点数集合</strong>。另外，Java虚拟机实现可以自由选择是否支持<strong>单精度浮点数扩展指数集合</strong>和<strong>双精度浮点数扩展指数集合</strong>中的一种或者全部。这些扩展指数集合可能在某些特定情况下代替标准浮点数集合来表示<code>fload</code>和<code>double</code>类型的数值。</p>
