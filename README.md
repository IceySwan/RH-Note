# Riemann-Hilbert 笔记

个人硕士期间学习 RH 的笔记, 包括零边界, 非零边界, 非局部 NLS 方程的解法

因仓促完成, 难免有很多错误, 如有发现请提 [issue](https://github.com/IceySwan/RH-Note/issues)

This is my RH notebook, about RHP, NLS second and third order equation and corresponding reductions. 

You can find the calculate code on `MMA-Code.nb`. 

## Todo

1. 增加解的分析
2. 增加插图

## 写作规范

1. 标点统一使用半角, 中英文之间增加一个半角空格, 禁止使用 `~` 强制空格
2. 标签使用 `chN-type-xxx` 的命名方式, 
   - 其中 `chN `为第 N 章, 
   - `type` 为类型, 例如`eq`, `def`, `thm`, `lemma`, `fig`, `table` 等
   - `xxx` 为名字, 示例 `ch1-eq-NLS-Lax-pair` 

3. 多层级括号默认使用 `\left(` `\right)` 自动匹配大小
4. 引用统一使用 `\cref{}`, 已有 `\xxref` 会逐渐舍弃
5. 数学符号加粗使用 `\bm{x}`
6. 行内分数使用 x/y 的形式, 不要使用 `frac` 或 display style
7. 提交前使用 latexindent 格式化
8. 应使用 XeLaTeX 编译

以下为数学符号规范

```latex
% 行内公式无空格输入
$x$ 
% 符号统一使用先下标后上标, 且均使用大括号包裹
$x_{a}^{b}$
% 行间公式统一使用 `equation` 环境, 且公式末尾应增加标点符号
\begin{equation}
	a^{2} + b^{2} = c^{2},
\end{equation} 
% 重音符号仅作用于本身, 而不作用于上下标
$\hat{z}_{1}$
% 虚数 i, 微分符号 d 采用直立体, 本文已自定义
\rmi \rmd 
% 公式运算符(或其他符号)间应保持空格, 
$x + y = 1$, $x \times y = 1$, $f(x,y) = x \ln(y) $
```

本文自定义符号如下

```latex
\RequirePackage[capitalize]{cleveref} % 必须放在 hyperref 之后

% 数学常数与微分符号 (直立体)
\newcommand{\rme}{\mathrm{e}}
\newcommand{\rmi}{\mathrm{i}}
\newcommand{\rmd}{\mathop{}\!\mathrm{d}} % \mathop{}\! 能自动处理微分符号前的间距

% 算符定义
\DeclareMathOperator*{\tr}{tr}
\DeclareMathOperator*{\Res}{Res}
\renewcommand{\Re}{\operatorname{Re}} % 推荐用 \operatorname 替代 \mathrm 以获得正确间距
\renewcommand{\Im}{\operatorname{Im}}
\newcommand{\diag}{\operatorname{diag}}
```

## License

除特别说明外，本仓库中由作者编写的构建脚本、转换工具和项目样式代码使用 MIT License 发布。

笔记正文内容使用 Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License
（CC BY-NC-SA 4.0）发布，包括 `content/`、`typst/content/` 以及由这些源码生成的 PDF 文档。

`elegantbook.cls` 遵循上游的 LPPL 1.3c；该许可证不受本仓库其他 MIT 或 CC 声明覆盖。
