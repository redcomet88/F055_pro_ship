# F055_pro vue+neo4j船舶知识问答系统|知识图谱|问答系统|CNN算法机器学习船舶分类

> 完整项目收费，可联系QQ: 81040295 微信: mmdsj186011 注明从github来的，谢谢！
也可以关注我的B站： 麦麦大数据 https://space.bilibili.com/1583208775
>
> 关注B站，私信获取！   [麦麦大数据](https://space.bilibili.com/1583208775)
> 编号:  F055 PRO
## 视频

[video(video-NZ5gctTO-1766462271312)(type-csdn)(url-https://live.csdn.net/v/embed/506911)(image-https://i-blog.csdnimg.cn/direct/d4cedbf3892e4728ba8c847e6379a8c0.png)(title-F055船舶问答识别知识库)]

## 1 系统简介
系统简介：本系统是一个基于Vue+Flask+Neo4j构建的船舶知识问答系统。其核心功能围绕船舶知识图谱的构建与智能问答展开。主要功能模块包括：用户登录注册、知识图谱可视化、船舶分类预测、自然语言问答、船舶信息查询、知识图谱管理、用户个人设置等。
## 2 功能设计
该系统采用前后端分离的B/S架构模式，基于Vue.js + Flask + Neo4j技术栈实现。前端通过Vue.js框架搭建响应式界面，结合Element Plus组件库提供友好的用户交互体验，使用Vue-Router进行页面路由管理，Axios实现与后端的异步数据交互。Flask后端负责构建RESTful API服务，通过Neo4j驱动（py2neo）连接图数据库，利用Cypher语言进行图谱查询与操作，存储船舶实体（如船型、建造年份、用途、船旗国等）及语义关系。前端结合Neo4j-GraphQL插件或Cytoscape.js实现知识图谱的交互式可视化。在船舶分类功能方面，系统采用CNN算法进行船舶图像识别，将CNN模型嵌入Flask服务中，实现自动分类与推荐。
### 2.1 系统架构图
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/1cff6faa0a0f4bcb8e36832008c229bb.jpeg)
### 2.2 功能模块图
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/bc6c15be952d41e1830060f78dc4d236.jpeg)

主要功能模块有：
1. 用户认证模块（登录/注册/权限管理）
2. 船舶知识图谱建模与存储
3. 知识图谱可视化与导航
4. 自然语言问答接口（支持语义理解）
5. 个人中心（用户信息维护）
### 3.1 登录 & 注册
登录注册做的是一个可以切换的登录注册界面，点击“去注册”或“去登录”可以切换表单。登录需要验证用户名和密码是否正确，支持账号密码登录，可选择记住登录状态。注册功能需填写用户名、邮箱、密码，系统会进行格式校验与唯一性判断，注册成功后自动跳转至登录页。
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/2a6467faa5a74c5d81b8ea5ac03910da.png)
### 3.2 船舶知识图谱建模
系统通过爬取船舶行业数据（如船舶登记信息、船型参数、港口数据等）构建领域知识图谱。实体包括：船舶类型、母港、船东、建造年份、载重吨、推进系统、船体结构等，其关系包括：“属于”、“建造于”、“服务于”、“配备有”等，全部录入Neo4j图数据库。
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/d506a59d82a140ac97659f0dd377163e.png)
### 3.3 数据导入与清洗
开发了数据清洗与导入脚本，使用Pandas预处理CSV/Excel数据，过滤空值与异常值，标准化实体名称（如“散货船”→“Bulk Carrier”），使用py2neo批量导入Neo4j图数据库，保证知识图谱结构完整。
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/e4a34d8f95134104bc7b24723db96e6c.png)
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/d33e68bdadb548148c4e07fb4335e671.png)
### 3.4 知识图谱可视化
前端通过Cytoscape.js或Neo4j Browser组件，展示任意节点（如“集装箱船”）及其关联关系，用户可通过点击节点查看详细信息，支持缩放、拖拽、高亮、聚类等交互操作。
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/9762a3727a9844b2aa8d56533bc71b8b.png)
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/ce8e1dfec1ec494399df891279f471c4.png)
支持查看图谱的详情：
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/5ec6299ab0364226a13d80c768dd95a2.png)
### 3.5 本地问答系统
系统提供自然语言输入接口（如“哪些船是油轮？”），前端将用户提问通过NLP技术（如关键词提取或BERT语义理解）转义成Cypher查询语句，调用后端接口执行图谱查询，返回结构化信息或图表。
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/de7295fb657a40238194eaf363c09067.png)
### 3.6 在线问答系统
系统集成 大语言模型（LLM）API（如通义千问、Qwen、ChatGLM、文心一格等），支持用户输入自然语言问题（如：“告诉我这艘船的尺寸”、“2010年后有哪些新型客轮？”），系统通过语义理解、知识图谱匹配、模型推理等方式生成结构化或自然语言回答。问答流程支持多轮对话，提升交互效率与用户满意度。

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/c195de7d53fa43b7a6ff685f77325448.jpeg)
### 3.7 船舶信息知识库
系统内置 20万条船舶相关信息数据，涵盖船舶名称、类型、吨位、建造年份、所属国家、技术参数、历史事件等字段。知识库支持多条件组合查询、模糊搜索、分页展示和导出功能。用户可通过关键词、分类、建造时间等条件快速定位所需船舶信息，实现知识的高效利用。

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/27674e9b5cbe449683cd079c4e9c153e.jpeg)
### 3.8 CNN船舶分类识别
用户上传船舶图像，系统通过预训练的 CNN 模型（如 ResNet、EfficientNet 等）对图像进行特征提取与分类，识别出船舶类型（如：油轮、集装箱船、货轮、帆船、军舰、客轮等），并在前端展示分类结果及置信度。系统支持批量上传与实时识别，为海事管理、船舶监管、智能识别系统提供技术支撑。
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/8f9d2c43132949e99496872711d81ed6.jpeg)
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/5fe35dce4da046a2bb4635d4bb4d87f5.jpeg)
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/b7cfe831736e4a149221deb6d4176d50.jpeg)

### 3.9 用户个人设置
个人设置方面包含了用户信息修改、密码修改功能。
用户信息修改中可以上传头像，完成用户的头像个性化设置，也可以修改用户其他信息。
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/705c9ce844964c51ac733dbf02ec42da.png)
修改密码需要输入用户旧密码和新密码，验证旧密码成功后，就可以完成密码修改。
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/c1133c6417444f10bab1e19ff9f2ed57.png)
## 4 程序核心算法代码
### 4.1 代码说明

本系统核心逻辑包括：

- 前端通过Vue+VUE-Router实现界面跳转，Axios调用Flask接口；
- 后端采用Flask+py2neo构建REST API，提供知识图谱查询、用户认证、图像分类服务；
- CNN分类模型使用PyTorch训练并导出为ONNX或TorchScript格式，通过Flask封装成推理服务；
- 知识图谱查询使用Cypher语言，结合动态参数拼接避免注入问题；
- 问答逻辑采用简单意图识别（关键词+句法匹配）结合图查询返回结果。

### 4.2 流程图

![外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传](https://img-home.csdnimg.cn/images/20230724024159.png?origin_url=https%3A%2F%2Fvia.placeholder.com%2F800x400%3Ftext%3DWorkflow%2BDiagram&pos_id=img-ozT7UdOr-1766462245850)

> 注：此处应放置系统核心流程图（如：用户提问 → 语义解析 → Cypher生成 → 查询图数据库 → 返回结果）

### 4.3 代码实例

```python
# 4.3.1 Flask后端：获取船舶知识图谱数据（Cypher查询示例）
from flask import Flask, request, jsonify
from py2neo import Graph

app = Flask(__name__)
graph = Graph("bolt://localhost:7687", auth=("neo4j", "password"))

@app.route('/api/ship/relations', methods=['GET'])
def get_ship_relations():
    query = """
    MATCH (s:Ship)-[r]->(t)
    WHERE s.name = $name
    RETURN s, r, t
    """
    result = graph.run(query, name=request.args.get('name'))
    data = []
    for record in result:
        data.append({
            'source': record['s']['name'],
            'relation': record['r'].type,
            'target': record['t']['name']
        })
    return jsonify(data)
```

```sql
-- 4.3.2 Neo4j构建船舶知识图谱（示例Cypher）
CREATE (car:Ship {name: "ContainerShip", type: "CargoShip", capacity: 10000})
CREATE (port:Port {name: "Shanghai", country: "China"})
CREATE (car)-[:SERVED_BY]->(port)
CREATE (crew:Person {name: "Captain Zhang", role: "Master"})
CREATE (car)-[:HAS_CREW]->(crew)
```

```python
# 4.3.3 CNN分类模型（PyTorch + Flask集成）
import torch
import torch.nn as nn
import torch.optim as optim
from torchvision import models, transforms
from flask import Flask, request, jsonify
import io
from PIL import Image
import numpy as np

app = Flask(__name__)
model = models.resnet50(pretrained=True)
model.fc = nn.Linear(2048, 10)  # 10类船舶
model.load_state_dict(torch.load('ship_classifier.pth'))
model.eval()

@app.route('/predict', methods=['POST'])
def predict():
    if 'file' not in request.files:
        return jsonify({'error': 'No file uploaded'}), 400
    file = request.files['file']
    img = Image.open(file.stream).convert('RGB')
    transform = transforms.Compose([
        transforms.Resize(256),
        transforms.CenterCrop(224),
        transforms.ToTensor(),
        transforms.Normalize(mean=[0.485, 0.456, 0.406], std=[0.229, 0.224, 0.225])
    ])
    img_tensor = transform(img).unsqueeze(0)
    with torch.no_grad():
        output = model(img_tensor)
        pred = torch.argmax(output, dim=1).item()
    return jsonify({'class': pred})
```

> 文章结尾部分有CSDN官方提供的学长 联系方式名片
>
> 文章结尾部分有CSDN官方提供的学长 联系方式名片
>
> 关注B站，私信获取！   [麦麦大数据](https://space.bilibili.com/1583208775)
> 编号:  F055
