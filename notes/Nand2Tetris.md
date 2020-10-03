<img src="C:\Users\Philip\AppData\Roaming\Typora\typora-user-images\image-20201003094317907.png" alt="image-20201003094317907" style="zoom:200%;" />

- 只看f=1的行，即1，3，5行
- 每一行我们都用NOT和AND来表示一个式子，如第二行NOT(X) AND Y AND NOT(Z)
- 然后OR

![计算机生成了可选文字: TruthTabletoBooleanExpression (NOT(x)ANDNOT(y)ANDNOT(z)) (NOT(x)ANDYANDN0T(z)) （×ANDN0T(y)ANDNOT(z)) OR OR (NOT(x)ANDNOT(z))OR(xANDNOT(y)ANDNOT(z)) (NOT(x)ANDNOT(z))OR(NOT(Y)ANDNOT(z)) NOT(z)AND(NOT(x)ORNOT(y))](file:///C:/Users/Philip/AppData/Local/Temp/msohtmlclip1/01/clip_image001.png)

把这个式子不断化简，就得到NOT(Z) AND ((NOT(X)) OR NOT(y))

![计算机生成了可选文字: Theorem AnyBooleanfunctionCanberepresentedusinganexpression contamingANDandNOToperatlons. Proof: (xORy)=NOT(NOT(x)ANDNOT(y))](file:///C:/Users/Philip/AppData/Local/Temp/msohtmlclip1/01/clip_image002.png)

用NOT和AND就可以表示所有的boolean function，因为OR是可以被NOT和AND表示的