## Django 小作业

框架 By [c7w](https://github.com/c7w)

代码填空 By [Andonade](https://github.com/Andonade)

2023 计算机系学生科协暑期培训

修改自 2023 春《软件工程》课程 Django 小作业


## API 文档

在完成本作业时，参照了 [API 文档](https://thuse-course.github.io/course-index/handout/api/).


## 环境配置

本次作业使用 `conda` 创建一个新的虚拟环境：

```zsh
conda create -n django_hw python=3.9 -y
conda activate django_hw
```

在此环境的基础之上，你可以运行下述命令安装依赖，注意请确保你的当前工作路径在克隆的小作业仓库中：

```zsh
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple -r requirements.txt
```

## 完成内容

本作业完成了以下step


### 添加路由

在 `board/urls.py` 中：

- 为 `boards/<index>` API 添加路由到 `views.boards_index` 视图函数
    - 注意这里不要写成 `<int:index>`，因为 API 文档里规定对于不是 int 的情况也要返回合法的 JSON 请求，而非展示 Django 的默认 404 网页

- 为 `user/<userName>` API 添加路由到下面“添加视图函数”节中自定义的视图函数



### 补全模型

在 `board/models.py` 中：

- 补全 `Board` 类的成员
    - `id`，使用 BigAutoField，设置主键
    - `user`，外键连接到 `User` 类，使用级联删除
    - `board_state`，使用 CharField
    - `board_name`，使用 CharField
    - `created_time`，使用 FloatField，初始值为类创建时的时间
- 补全 `Board` 表的元数据
    - 为 `board_name` 创建索引
    - 在 `user` 和 `board_name` 上建立联合唯一约束

之后，使用如下命令建库：

```zsh
 python3 manage.py makemigrations board
 python3 manage.py migrate
```



### 补全与添加视图函数

在 `board/views.py` 中：

- 按照所给注释补全 `login` 登录函数
- 阅读 API 文档中的对应项，然后补全 `check_for_board_data` 中的检查输入字段功能
- 按照所给注释补全 `board` 视图函数
- 阅读 API 文档中的对应项，完成 `boards_index` 的 DELETE 方法
- 阅读 API 文档中的对应项，完成 `user/<userName>` API 所对应的视图函数



### 进行单元测试

预先撰写好的脚本 `test.sh` 包含了进行单元测试与计算覆盖率的功能。为运行单元测试，运行：

```zsh
python3 manage.py test
```

正确完成本次作业应该可以通过所有测试点。在小作业中你可以阅读 `board/tests.py` 中的测试逻辑对你的路由、模型与视图函数进行修改，**但请不要修改 `board/tests.py` 中的内容**。在后续的项目中 `tests.py` 将由组内负责测试与质量保证的同学进行撰写。

