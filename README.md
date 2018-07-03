# LibrarySystem
4.	简易图书管理系统

需求分析：
图书管理系统其实是一个很复杂的信息管理系统，它包括很多分类、检索等方面的内容。因为其复杂性，本实验只要实现一个简化的图书管理系统的功能。
1.	基本功能需求：
（1）管理员模块 
主要功能是对图书信息的添加，修改，删除；读者的添加，删除，修改；以及对读者权限登录的控制 
（2）信息录入功能
1）添加新图书信息。只有管理员有权限操作
2）添加读者信息。用于登记新读者信息。只有管理员有权限操作。
3）借阅信息。用于登记读者的借阅情况信息。
（3）逻辑功能要求
1）修改和删除图书信息。图书被借出时，系统需要更新图书信息的可借数量，当可借数量为0时，表示该图书都已被借出。当输入的图书信息有错误或需要进行必要更新时，可以修改图书信息；当一种图书所有馆藏图书都已损毁或遗失并且不能重新买到时，该图书信息需要删除。
2）修改和删除读者信息。如某读者毕业了可删除该读者的信息
3）还书处理。读者归还图书时，更新图书借阅信息表中的归还日期，读者信息表中的已借数量及ISBN类别信息表中该图书的可借数量。当图书期限过期，自动计算罚款。
4）借书限制。当读者有罚款时，不能借书。可提示是否要交罚款，交完之后即可借书。
（4）查询功能
1）图书查询功能。根据图书的各种已知条件来查询图书的详细信息，如书名、作者、ISBN书号等支持模糊查询。
2）读者信息查询。输入读者的借书证号、姓名等信息，查询读者的基本信息。对查询到的每一个读者，能够显示其未归还的图书编号和书名。
3）查询所有到期未归还的图书信息。要求结果显示图书编号、书名、读者姓名、借书证号码、借出日期等信息。
2.数据表的创建
根据功能要求的说明创建下列数据表：
（1）登陆表
登陆表包括以下字段：
账号，密码，权限（判断管理员还是读者）
（2）图书信息表
图书信息表包括以下字段：
ISBN书号、书名、出版社、作者、馆藏数量、可借数量、是否可借。
（3）读者信息表
读者信息表包括以下字段：
借书证号、姓名、性别、职称、可借数量、已借数量、工作部门、联系电话。
（4）借阅信息表（图书-读者关系）
借阅信息表包括以下字段：
借书证号、借阅书号、借出日期、借阅期限、归还日期、罚款。
3.数据库完整性设计
设计者应认真分析和思考各个表之间的关系，合理设计和实施数据完整性原则。
1）给每个表实施主键及外键约束。
2）设定缺省约束。如性别。
3）设置非空约束如图书信息表中的书名。
4）实施CHECK约束。
4.SQL Server数据库对象设计（此建议可选）
1）设计一个存储过程，以图书编号为输入参数，返回借阅该图书但未归还的读者姓名和借书证号。
2）读者资料查询：设计一个有多个输入参数的存储过程，返回读者的详细信息。设计另一存储过程并以读者借书证号为输入参数，返回该读者未归还的图书名称和图书编号。
3）到期图书查询：设计一个视图，返回所有逾期未归还的图书的编号、书名、读者姓名等信息。
5）加快数据检索速度，用图书编号为图书信息表建立索引。
6）为读者信息表创建一个删除触发器，当一个读者毕业或者请他情况时，将此读者的资料从读者信息表中删除。注意实施业务规则：有借阅书的读者不得从读者信息表中删除。
7）借阅处理：为借阅信息表设计INSERT触发器，在读者借阅时更改ISBN类别信息表，且可借数量减1，图书信息表是否可借列的值变为“不可借”，读者信息表中该类读者已借阅数加1。
8）还书处理：为借阅信息表设计UPDATE触发器，在该表的归还日期列被更改后，将图书信息表的是否可借列的值变为“可借”，读者信息表中已借数量减1及ISBN类别信息表中可借数量加1。
备注：该题目不能随意删除表的字段，可相应增加相关字段，除了上述的基本功能之外，可另外添加其他功能。
