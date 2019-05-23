摘自《Java虚拟机规范(Java SE8版)》 2.3.2浮点类型、取值集合及浮点值<p/>
	<p>浮点类型包含<code>float</code>类型和<code>double</code>类型两种，他们在概念上与《IEEE Standard for Binary Floating-Point Arithmetic》(ANSI/IEEE Std.754-1985, New York)标准中定义的32位单精度和64位双精度IEEE-754格式的取值与操作是一致的。</p>
	<p><u>IEEE 754 标准的内容不仅包括了正负的带符号量（sign-magnitude number），而且包括了正负零、正负无穷大的一个特殊的“非数字”标识（Not-a-Number，下午用NaN表示）。</u>NaN值用于表示某些无效的运算操作，例如除以0等情况。</p>
	<p>所有Java虚拟机的实现都必须支持两种标准的浮点数集合：<strong>单精度浮点数集合</strong>和<strong>双精度浮点数集合</strong>。另外，Java虚拟机实现可以自由选择是否支持<strong>单精度浮点数扩展指数集合</strong>和<strong>双精度浮点数扩展指数集合</strong>中的一种或者全部。这些扩展指数集合可能在某些特定情况下代替标准浮点数集合来表示<code>fload</code>和<code>double</code>类型的数值。</p>
	<p>任意一个非零的、可数的任意浮点值都可以表示为 s x m x 2<sup><small>(e-N+1)</small></sup>的形式，其中s可以+1或者-1，m可以是一个小于2<sup><small>N</small></sup>的正整数，e是一个介于E<sub><small>min</small></sub>=-(2<sup><small>K-1</small></sup>-2)和E<sub><small>max</small></sub>=2<sup><small>K-1</small></sup>-1之间的整数（包括E<sub><small>min</small></sub>和<sub><small>max</small></sub>）。这里的 N 和 K 两个参数的取值范围决定于当前采用的浮点数值集合。部分浮点数使用这种规则得到的表现形式可能不是唯一的，例如，在指定的数值集合内，可以存在一个数字 v，它能找到特定的s 、m 和 e 值来表示，使得其中 m 是偶数，并且 e 小于 2<sup><small>K-1</small></sup>，这样我们就能够通过把 m 的值减半再将 e 的值增加1的方式来得到 v 的另外一种不同的表示形式。在这些表示形式中，如果其中某种表现形式中 m 的值满足条件 m >= 2<sup><small>N-1</small></sup>，那就称这种表示为<b>标准表示</b>（normalized representation），你满足这个条件的其他表现形式就称为非标准表示（denormalized representation）。如果某个数值不存在任何满足 m >= 2<sup><small>N-1</small></sup>的表现形式，即不存在任何标准表示，那就称这个数字为非标准值（denormalized value）。</p>
<table>
	<tr>
		<th>参数</th>
		<th>单精度浮点数集合</th>
		<th>单精度扩展指数集合</th>
		<th>双精度浮点数集合</th>
		<th>双精度扩展指数集合</th>
	</tr>
	<tr>
		<td>N</td>
		<td>24</td>
		<td>24</td>
		<td>53</td>
		<td>53</td>
	</tr>
	<tr>
		<td>K</td>
		<td>8</td>
		<td>&ge;11</td>
		<td>11</td>
		<td>&ge;15</td>
	</tr>
	<tr>
		<td>E<sub><small>max</small></sub></td>
		<td>+127</td>
		<td>&ge;+1023</td>
		<td>+10.23</td>
		<td>&ge;+16383</td>
	</tr>
	<tr>
		<td>E<sub><small>min</small></sub></td>
		<td>-126</td>
		<td>&le;-1022</td>
		<td>-1022</td>
		<td>&le;-16382</td>
	</tr>
</table>
<p>
	如果虚拟机实现支持了（无论是支持一种还是支持全部）扩展指数集合，那每一种支持的扩展指数集合都有一个由具体虚拟机实现决定的参数 K，上表中给出了这个参数的约束范围（&ge;11 或 &ge;15），这个参数也决定了 E<sub><small>max</small></sub> 和 E<sub><small>min</small></sub> 两个衍生参数的取值范围。</p>
