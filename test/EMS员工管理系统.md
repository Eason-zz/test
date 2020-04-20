# EMS员工管理系统

简介：

1. 简单的信息管理

2. 列表的基础应用

3. 只有简单逻辑，如添加员工信息、删除员工信息等

   ```python
   print('-'*20 , '欢迎使用员工管理系统', '-'*20)
   sys_list = ['孙悟空\t19\t男\t花果山\t业务能力强','猪八戒\t25\t男\t高老庄\t业务能力弱','唐僧\t23\t男\t大唐\t业务能力弱','沙僧\t27\t男\t流沙河\t业务能力一般']
   while True:
   # 显示用户的选项
   	print('请选择要做的操作：')
   	print('\t1.查询员工信息')
   	print('\t2.添加员工信息')
   	print('\t3.删除员工信息')
   	print('\t4.更新员工信息')
   	print('\t5.退出系统')
   	user_choose = input('请选择[1-5]:')
   	print('-'*62)
   # 根据用户的选择做相关的操作
   	if user_choose == '1' :
   #查询员工
   		print('\t序号\t姓名\t年龄\t性别\t住址\t能力')
   		n = 1
   		for i in sys_list:
   			print(f'\t{n}\t{i}')
   			n +=1
   	elif user_choose == '2' :
   		name = input('请输入员工的姓名： ')
   		age = input('请输入员工的年龄： ')
   		gender = input('请输入员工的性别： ')
   		address = input('请输入员工的住址： ')
   		ability_level = input('请输入员工的能力水平： ')
   		emp = f'{name}\t{age}\t{gender}\t{address}\t{ability_level}'
   		print(f'以下员工将被添加到列表中：{emp}')
   		user_confirm = input('是否确认此次操作[Y/N]:') 
   		if user_confirm == 'Y' or user_confirm == 'y' or user_confirm =='yes':
   			sys_list.append(emp) 
   			print('操作成功!')
   		else:
   			print('操作已取消！')
   	elif user_choose == '3':
   #删除员工，根据员工序号删除员工
   #员工序号 == index + 1
   		del_num = int(input('请输入要删除的员工的序号：'))
   		if 0 < del_num <= len(sys_list):
   			del_i = del_num - 1
   			emp = f'\t{del_num}\t{sys_list[del_i]}'
   			print('以下员工将被删除')
   			print('-'*62)
   			print('\t序号\t姓名\t年龄\t性别\t住址\t能力')
   			print(emp)
   			user_confirm = input('是否确认此次操作[Y/N]:')
   			if user_confirm == 'Y' or user_confirm == 'y' or user_confirm =='yes':
   				sys_list.pop(emp) 
   				print('操作成功!')
   			else:
   				print('操作已取消！')
   	elif user_choose == '4':
   		del_num = int(input('请输入要修改的员工的序号：'))
   		if 0 < del_num <= len(sys_list):
   			del_i = del_num - 1
   			emp = f'\t{del_num}\t{sys_list[del_i]}'
   			print('以下员工信息将被修改')
   			print('-'*62)
   			print('\t序号\t姓名\t年龄\t性别\t住址\t能力')
   			print(emp)
   			name = input('请输入修改后员工的姓名： ')
   			age = input('请输入修改后员工的年龄： ')
   			gender = input('请输入修改后员工的性别： ')
   			address = input('请输入修改后员工的住址： ')
   			ability_level = input('请输入修改后员工的能力水平： ')
   			emp_1 = f'{name}\t{age}\t{gender}\t{address}\t{ability_level}'
   			user_confirm = input('是否确认此次操作[Y/N]:')
   			if user_confirm == 'Y' or user_confirm == 'y' or user_confirm =='yes': 
   				sys_list.pop(emp)
   				sys_list[del_i] = emp_1
   				print('操作成功!')
   			else:
   				print('操作已取消！')
   		else:
   			print(f'没有编号为{del_num}的员工')
   	elif user_choose == '5':
   		
   		print('欢迎使用员工管理系统，再见')
   		print('按回车键退出')
   		break
   	else:
   		print('输入错误，请重新输入')
   ```

   

命令行中的执行效果：

```python
-------------------- 欢迎使用员工管理系统 --------------------
请选择要做的操作：
        1.查询员工信息
        2.添加员工信息
        3.删除员工信息
        4.更新员工信息
        5.退出系统
请选择[1-5]:1
--------------------------------------------------------------
        序号    姓名    年龄    性别    住址    能力
        1       孙悟空  19      男      花果山  业务能力强
        2       猪八戒  25      男      高老庄  业务能力弱
        3       唐僧    23      男      大唐    业务能力弱
        4       沙僧    27      男      流沙河  业务能力一般
请选择要做的操作：
        1.查询员工信息
        2.添加员工信息
        3.删除员工信息
        4.更新员工信息
        5.退出系统
请选择[1-5]:2
--------------------------------------------------------------
请输入员工的姓名： aa
请输入员工的年龄： aa
请输入员工的性别： aa
请输入员工的住址： aa
请输入员工的能力水平： aa
以下员工将被添加到列表中：aa    aa      aa      aa      aa
是否确认此次操作[Y/N]:y
操作成功!
请选择要做的操作：
        1.查询员工信息
        2.添加员工信息
        3.删除员工信息
        4.更新员工信息
        5.退出系统
请选择[1-5]:
```

