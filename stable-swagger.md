## Compute Server 公开 API

Compute Server 组件负责 CAIP 计算相关业务逻辑。这个章节列出了所有 Compute Server 组件公开 API。

### 列出所有项目的算力规格

根据指定条件分页查询所有项目的`算力规格`。

URI: GET /v2/flavor

Query 参数：

| 参数        | 是否必选 | 参数类型        | 描述                                                              |
| ----------- | -------- | --------------- | ----------------------------------------------------------------- |
| enabled     | false    | boolean         | 是否开启算力规格，未开启的算力规格无法在用户项目中被查看和使用    |
| flavor_type | false    | string          | 算力规格类型。                                                    |
| limit       | false    | integer         | 指定每一页返回的最大条目数                                        |
| offset      | false    | integer         | 分页列表的起始页                                                  |
| sort        | false    | string          | 指定查询的排序顺序。`+` 为正序，`-` 为倒序。比如：`+name`,`-date` |
| namespace   | false    | array of string | 项目 ID，公共算力规格可以使用 `public` 关键字检索                 |
| name        | false    | string          | 名称                                                              |
| withNode    | false    | boolean         | 查询时返回集群节点信息                                            |

响应状态码：200

Body 参数：

| 参数     | 参数类型                                       | 描述         |
| -------- | ---------------------------------------------- | ------------ |
| metadata | [cambricon.ListMeta](#cambricon.listmeta)      | 列表附加信息 |
| items    | array of [cambricon.Flavor](#cambricon.flavor) | 算力规格列表 |

### 创建算力规格

创建`算力规格`

URI: POST /v2/flavor

请求 Body 参数：

| 参数 | 是否必选 | 参数类型                              | 描述 |
| ---- | -------- | ------------------------------------- | ---- |
| body | true     | [cambricon.Flavor](#cambricon.flavor) |      |

响应状态码：201

Body 参数：

| 参数 | 参数类型 | 描述                                                                                                                                                                                                                                                                                                                                                          |
| ---- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| id   | string   | 唯一标识符                                                                                                                                                                                                                                                                                                                                                    |
| name | string   | 名称                                                                                                                                                                                                                                                                                                                                                          |
| type | string   | 资源类型 (可选项: algorithm, cairfavoritealgorithm, cairfavoritedataset, dataset, evaluationjob, flavor, inference, job, modelconversion, modelpackage, modelpackageversion, notebook, persistentvolumeclaim, predictor, predictorjob, pretrainedmodel, sampleset, savedmodel, server, sharedalgorithm, shareddataset, sharedmodel, tensorboard, trainingjob) |

### 删除算力规格

删除`算力规格`

URI: DELETE /v2/flavor/{uid}

路径参数：

| 参数 | 是否必选 | 参数类型 | 描述       |
| ---- | -------- | -------- | ---------- |
| uid  | true     | string   | 唯一标识符 |

响应状态码：202

### 修改算力规格

修改算力规格

URI: PUT /v2/flavor/{uid}

路径参数：

| 参数 | 是否必选 | 参数类型 | 描述       |
| ---- | -------- | -------- | ---------- |
| uid  | true     | string   | 唯一标识符 |

请求 Body 参数：

| 参数 | 是否必选 | 参数类型                              | 描述 |
| ---- | -------- | ------------------------------------- | ---- |
| body | true     | [cambricon.Flavor](#cambricon.flavor) |      |

响应状态码：202

### 列出项目中的`我的算法卷`

根据指定条件分页查询项目中的`我的算法卷`。

URI: GET /v2/namespace/{namespace}/algorithm

路径参数：

| 参数      | 是否必选 | 参数类型 | 描述    |
| --------- | -------- | -------- | ------- |
| namespace | true     | string   | 项目 ID |

Query 参数：

| 参数    | 是否必选 | 参数类型        | 描述                                                              |
| ------- | -------- | --------------- | ----------------------------------------------------------------- |
| labels  | false    | array of string | 指定需要过滤的标签，多个标签用`,`分隔                             |
| limit   | false    | integer         | 指定每一页返回的最大条目数                                        |
| offset  | false    | integer         | 分页列表的起始页                                                  |
| sort    | false    | string          | 指定查询的排序顺序。`+` 为正序，`-` 为倒序。比如：`+name`,`-date` |
| name    | false    | string          | 名称                                                              |
| status  | false    | array of string | 资源状态                                                          |
| user_id | false    | string          | 创建者 ID                                                         |

响应状态码：200

Body 参数：

| 参数     | 参数类型                                                       | 描述         |
| -------- | -------------------------------------------------------------- | ------------ |
| metadata | [cambricon.ListMeta](#cambricon.listmeta)                      | 列表附加信息 |
| items    | array of [cambricon.TrainingVolume](#cambricon.trainingvolume) | 训练用卷列表 |

### 创建我的算法卷

创建`我的算法卷``

URI: POST /v2/namespace/{namespace}/algorithm

路径参数：

| 参数      | 是否必选 | 参数类型 | 描述    |
| --------- | -------- | -------- | ------- |
| namespace | true     | string   | 项目 ID |

请求 Body 参数：

| 参数 | 是否必选 | 参数类型                                              | 描述 |
| ---- | -------- | ----------------------------------------------------- | ---- |
| body | true     | [cambricon.TrainingVolume](#cambricon.trainingvolume) |      |

响应状态码：201

Body 参数：

| 参数 | 参数类型 | 描述                                                                                                                                                                                                                                                                                                                                                          |
| ---- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| id   | string   | 唯一标识符                                                                                                                                                                                                                                                                                                                                                    |
| name | string   | 名称                                                                                                                                                                                                                                                                                                                                                          |
| type | string   | 资源类型 (可选项: algorithm, cairfavoritealgorithm, cairfavoritedataset, dataset, evaluationjob, flavor, inference, job, modelconversion, modelpackage, modelpackageversion, notebook, persistentvolumeclaim, predictor, predictorjob, pretrainedmodel, sampleset, savedmodel, server, sharedalgorithm, shareddataset, sharedmodel, tensorboard, trainingjob) |

### 删除`我的算法卷`

删除`我的算法卷`

URI: DELETE /v2/namespace/{namespace}/algorithm/{uid}

路径参数：

| 参数      | 是否必选 | 参数类型 | 描述       |
| --------- | -------- | -------- | ---------- |
| namespace | true     | string   | 项目 ID    |
| uid       | true     | string   | 唯一标识符 |

响应状态码：202

### 查询项目中的特定`我的算法卷`详情

根据指定条件分页查询项目中的`我的算法卷`。

URI: GET /v2/namespace/{namespace}/algorithm/{uid}

路径参数：

| 参数      | 是否必选 | 参数类型 | 描述       |
| --------- | -------- | -------- | ---------- |
| namespace | true     | string   | 项目 ID    |
| uid       | true     | string   | 唯一标识符 |

响应状态码：200

Body 参数：

| 参数     | 参数类型                                                          | 描述     |
| -------- | ----------------------------------------------------------------- | -------- |
| metadata | [cambricon.ObjectMeta](#cambricon.objectmeta)                     | 附加信息 |
| spec     | [cambricon.TrainingVolumeSpec](#cambricon.trainingvolumespec)     | 规格     |
| status   | [cambricon.TrainingVolumeStatus](#cambricon.trainingvolumestatus) | 状态     |

### 修改我的算法卷

修改`我的算法卷`

URI: PUT /v2/namespace/{namespace}/algorithm/{uid}

路径参数：

| 参数      | 是否必选 | 参数类型 | 描述       |
| --------- | -------- | -------- | ---------- |
| namespace | true     | string   | 项目 ID    |
| uid       | true     | string   | 唯一标识符 |

请求 Body 参数：

| 参数 | 是否必选 | 参数类型                                              | 描述 |
| ---- | -------- | ----------------------------------------------------- | ---- |
| body | true     | [cambricon.TrainingVolume](#cambricon.trainingvolume) |      |

响应状态码：202

### 列出项目中的`我的数据集`

根据指定条件分页查询项目中的`我的数据集`。

URI: GET /v2/namespace/{namespace}/dataset

路径参数：

| 参数      | 是否必选 | 参数类型 | 描述    |
| --------- | -------- | -------- | ------- |
| namespace | true     | string   | 项目 ID |

Query 参数：

| 参数    | 是否必选 | 参数类型        | 描述                                                              |
| ------- | -------- | --------------- | ----------------------------------------------------------------- |
| labels  | false    | array of string | 指定需要过滤的标签，多个标签用`,`分隔                             |
| limit   | false    | integer         | 指定每一页返回的最大条目数                                        |
| offset  | false    | integer         | 分页列表的起始页                                                  |
| sort    | false    | string          | 指定查询的排序顺序。`+` 为正序，`-` 为倒序。比如：`+name`,`-date` |
| name    | false    | string          | 名称                                                              |
| status  | false    | array of string | 资源状态                                                          |
| user_id | false    | string          | 创建者 ID                                                         |

响应状态码：200

Body 参数：

| 参数     | 参数类型                                                       | 描述         |
| -------- | -------------------------------------------------------------- | ------------ |
| metadata | [cambricon.ListMeta](#cambricon.listmeta)                      | 列表附加信息 |
| items    | array of [cambricon.TrainingVolume](#cambricon.trainingvolume) | 训练用卷列表 |

### 创建我的数据集

创建`我的数据集`

URI: POST /v2/namespace/{namespace}/dataset

路径参数：

| 参数      | 是否必选 | 参数类型 | 描述    |
| --------- | -------- | -------- | ------- |
| namespace | true     | string   | 项目 ID |

请求 Body 参数：

| 参数 | 是否必选 | 参数类型                                              | 描述 |
| ---- | -------- | ----------------------------------------------------- | ---- |
| body | true     | [cambricon.TrainingVolume](#cambricon.trainingvolume) |      |

响应状态码：201

Body 参数：

| 参数 | 参数类型 | 描述                                                                                                                                                                                                                                                                                                                                                          |
| ---- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| id   | string   | 唯一标识符                                                                                                                                                                                                                                                                                                                                                    |
| name | string   | 名称                                                                                                                                                                                                                                                                                                                                                          |
| type | string   | 资源类型 (可选项: algorithm, cairfavoritealgorithm, cairfavoritedataset, dataset, evaluationjob, flavor, inference, job, modelconversion, modelpackage, modelpackageversion, notebook, persistentvolumeclaim, predictor, predictorjob, pretrainedmodel, sampleset, savedmodel, server, sharedalgorithm, shareddataset, sharedmodel, tensorboard, trainingjob) |

### 删除我的数据集

删除`我的数据集`

URI: DELETE /v2/namespace/{namespace}/dataset/{uid}

路径参数：

| 参数      | 是否必选 | 参数类型 | 描述       |
| --------- | -------- | -------- | ---------- |
| namespace | true     | string   | 项目 ID    |
| uid       | true     | string   | 唯一标识符 |

响应状态码：202

### 查询项目中的特定`我的数据集`详情

根据指定条件分页查询项目中的`我的数据集`。

URI: GET /v2/namespace/{namespace}/dataset/{uid}

路径参数：

| 参数      | 是否必选 | 参数类型 | 描述       |
| --------- | -------- | -------- | ---------- |
| namespace | true     | string   | 项目 ID    |
| uid       | true     | string   | 唯一标识符 |

响应状态码：200

Body 参数：

| 参数     | 参数类型                                                          | 描述     |
| -------- | ----------------------------------------------------------------- | -------- |
| metadata | [cambricon.ObjectMeta](#cambricon.objectmeta)                     | 附加信息 |
| spec     | [cambricon.TrainingVolumeSpec](#cambricon.trainingvolumespec)     | 规格     |
| status   | [cambricon.TrainingVolumeStatus](#cambricon.trainingvolumestatus) | 状态     |

### 修改我的数据集

修改`我的数据集`

URI: PUT /v2/namespace/{namespace}/dataset/{uid}

路径参数：

| 参数      | 是否必选 | 参数类型 | 描述       |
| --------- | -------- | -------- | ---------- |
| namespace | true     | string   | 项目 ID    |
| uid       | true     | string   | 唯一标识符 |

请求 Body 参数：

| 参数 | 是否必选 | 参数类型                                              | 描述 |
| ---- | -------- | ----------------------------------------------------- | ---- |
| body | true     | [cambricon.TrainingVolume](#cambricon.trainingvolume) |      |

响应状态码：202

### 列出项目中的`我的模型卷`

根据指定条件分页查询项目中的`我的模型卷`。

URI: GET /v2/namespace/{namespace}/savedmodel

路径参数：

| 参数      | 是否必选 | 参数类型 | 描述    |
| --------- | -------- | -------- | ------- |
| namespace | true     | string   | 项目 ID |

Query 参数：

| 参数    | 是否必选 | 参数类型        | 描述                                                              |
| ------- | -------- | --------------- | ----------------------------------------------------------------- |
| labels  | false    | array of string | 指定需要过滤的标签，多个标签用`,`分隔                             |
| limit   | false    | integer         | 指定每一页返回的最大条目数                                        |
| offset  | false    | integer         | 分页列表的起始页                                                  |
| sort    | false    | string          | 指定查询的排序顺序。`+` 为正序，`-` 为倒序。比如：`+name`,`-date` |
| name    | false    | string          | 名称                                                              |
| status  | false    | array of string | 资源状态                                                          |
| user_id | false    | string          | 创建者 ID                                                         |

响应状态码：200

Body 参数：

| 参数     | 参数类型                                                       | 描述         |
| -------- | -------------------------------------------------------------- | ------------ |
| metadata | [cambricon.ListMeta](#cambricon.listmeta)                      | 列表附加信息 |
| items    | array of [cambricon.TrainingVolume](#cambricon.trainingvolume) | 训练用卷列表 |

### 创建我的模型

创建`我的模型`

URI: POST /v2/namespace/{namespace}/savedmodel

路径参数：

| 参数      | 是否必选 | 参数类型 | 描述    |
| --------- | -------- | -------- | ------- |
| namespace | true     | string   | 项目 ID |

请求 Body 参数：

| 参数 | 是否必选 | 参数类型                                              | 描述 |
| ---- | -------- | ----------------------------------------------------- | ---- |
| body | true     | [cambricon.TrainingVolume](#cambricon.trainingvolume) |      |

响应状态码：201

Body 参数：

| 参数 | 参数类型 | 描述                                                                                                                                                                                                                                                                                                                                                          |
| ---- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| id   | string   | 唯一标识符                                                                                                                                                                                                                                                                                                                                                    |
| name | string   | 名称                                                                                                                                                                                                                                                                                                                                                          |
| type | string   | 资源类型 (可选项: algorithm, cairfavoritealgorithm, cairfavoritedataset, dataset, evaluationjob, flavor, inference, job, modelconversion, modelpackage, modelpackageversion, notebook, persistentvolumeclaim, predictor, predictorjob, pretrainedmodel, sampleset, savedmodel, server, sharedalgorithm, shareddataset, sharedmodel, tensorboard, trainingjob) |

### 删除我的模型

删除`我的模型`

URI: DELETE /v2/namespace/{namespace}/savedmodel/{uid}

路径参数：

| 参数      | 是否必选 | 参数类型 | 描述       |
| --------- | -------- | -------- | ---------- |
| namespace | true     | string   | 项目 ID    |
| uid       | true     | string   | 唯一标识符 |

响应状态码：202

### 查询项目中的特定`我的模型卷`详情

根据指定条件分页查询项目中的`我的模型卷`。

URI: GET /v2/namespace/{namespace}/savedmodel/{uid}

路径参数：

| 参数      | 是否必选 | 参数类型 | 描述       |
| --------- | -------- | -------- | ---------- |
| namespace | true     | string   | 项目 ID    |
| uid       | true     | string   | 唯一标识符 |

响应状态码：200

Body 参数：

| 参数     | 参数类型                                                          | 描述     |
| -------- | ----------------------------------------------------------------- | -------- |
| metadata | [cambricon.ObjectMeta](#cambricon.objectmeta)                     | 附加信息 |
| spec     | [cambricon.TrainingVolumeSpec](#cambricon.trainingvolumespec)     | 规格     |
| status   | [cambricon.TrainingVolumeStatus](#cambricon.trainingvolumestatus) | 状态     |

### 修改我的模型

修改`我的模型`

URI: PUT /v2/namespace/{namespace}/savedmodel/{uid}

路径参数：

| 参数      | 是否必选 | 参数类型 | 描述       |
| --------- | -------- | -------- | ---------- |
| namespace | true     | string   | 项目 ID    |
| uid       | true     | string   | 唯一标识符 |

请求 Body 参数：

| 参数 | 是否必选 | 参数类型                                              | 描述 |
| ---- | -------- | ----------------------------------------------------- | ---- |
| body | true     | [cambricon.TrainingVolume](#cambricon.trainingvolume) |      |

响应状态码：202

### 列出项目中的`训练任务`

根据指定条件分页查询项目中的`训练任务`。

URI: GET /v2/namespace/{namespace}/batch-trainingjob

路径参数：

| 参数      | 是否必选 | 参数类型 | 描述    |
| --------- | -------- | -------- | ------- |
| namespace | true     | string   | 项目 ID |

Query 参数：

| 参数          | 是否必选 | 参数类型        | 描述                                                                                           |
| ------------- | -------- | --------------- | ---------------------------------------------------------------------------------------------- |
| commun_type   | false    | string          | 分布式模式                                                                                     |
| limit         | false    | integer         | 指定每一页返回的最大条目数                                                                     |
| offset        | false    | integer         | 分页列表的起始页                                                                               |
| sort          | false    | string          | 指定查询的排序顺序。`+` 为正序，`-` 为倒序。比如：`+name`,`-date`                              |
| name          | false    | string          | 名称                                                                                           |
| sourceID      | false    | string          | 依赖的卷 ID                                                                                    |
| sourceType    | false    | string          | 卷类型，（可选项：algorithm（我的算法卷），dataset（我的数据集），savedmodel（保存模型地址）） |
| status        | false    | array of string | 资源状态                                                                                       |
| training_type | false    | string          | 训练任务类型                                                                                   |
| user_id       | false    | string          | 创建者 ID                                                                                      |

响应状态码：200

Body 参数：

| 参数     | 参数类型                                                           | 描述         |
| -------- | ------------------------------------------------------------------ | ------------ |
| metadata | [cambricon.ListMeta](#cambricon.listmeta)                          | 附加信息     |
| items    | array of [cambricon.BatchTrainingJob](#cambricon.batchtrainingjob) | 训练任务列表 |

### 创建训练任务

创建`训练任务`

URI: POST /v2/namespace/{namespace}/batch-trainingjob

路径参数：

| 参数      | 是否必选 | 参数类型 | 描述    |
| --------- | -------- | -------- | ------- |
| namespace | true     | string   | 项目 ID |

请求 Body 参数：

| 参数 | 是否必选 | 参数类型                                                  | 描述 |
| ---- | -------- | --------------------------------------------------------- | ---- |
| body | true     | [cambricon.BatchTrainingJob](#cambricon.batchtrainingjob) |      |

响应状态码：201

Body 参数：

| 参数 | 参数类型 | 描述                                                                                                                                                                                                                                                                                                                                                          |
| ---- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| id   | string   | 唯一标识符                                                                                                                                                                                                                                                                                                                                                    |
| name | string   | 名称                                                                                                                                                                                                                                                                                                                                                          |
| type | string   | 资源类型 (可选项: algorithm, cairfavoritealgorithm, cairfavoritedataset, dataset, evaluationjob, flavor, inference, job, modelconversion, modelpackage, modelpackageversion, notebook, persistentvolumeclaim, predictor, predictorjob, pretrainedmodel, sampleset, savedmodel, server, sharedalgorithm, shareddataset, sharedmodel, tensorboard, trainingjob) |

### 删除训练任务

删除`训练任务`

URI: DELETE /v2/namespace/{namespace}/batch-trainingjob/{uid}

路径参数：

| 参数      | 是否必选 | 参数类型 | 描述       |
| --------- | -------- | -------- | ---------- |
| namespace | true     | string   | 项目 ID    |
| uid       | true     | string   | 唯一标识符 |

响应状态码：202

### 查询项目中的特定`训练任务`详情

根据指定条件分页查询项目中的`训练任务`。

URI: GET /v2/namespace/{namespace}/batch-trainingjob/{uid}

路径参数：

| 参数      | 是否必选 | 参数类型 | 描述       |
| --------- | -------- | -------- | ---------- |
| namespace | true     | string   | 项目 ID    |
| uid       | true     | string   | 唯一标识符 |

响应状态码：200

Body 参数：

| 参数              | 参数类型                                                          | 描述                                                                                                                              |
| ----------------- | ----------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| batched           | boolean                                                           | 是否为批量训练任务。已废弃，请使用 `trainingType` 字段                                                                            |
| communType        | string                                                            | 分布式模式 (可选项: horovod, tensorflow, pytorch, standalone)                                                                     |
| info              | [cambricon.BatchTrainingJobInfo](#cambricon.batchtrainingjobinfo) | 训练任务状态                                                                                                                      |
| metadata          | [cambricon.ObjectMeta](#cambricon.objectmeta)                     | 附加信息                                                                                                                          |
| priorityClassName | string                                                            | 任务优先级类别名。（可选项：`train-job-priority-1`（默认），`train-job-priority-3`（紧急），`train-job-priority-11`（非常紧急）） |
| spec              | [cambricon.BatchTrainingJobSpec](#cambricon.batchtrainingjobspec) | 规格                                                                                                                              |
| status            | string                                                            | 状态                                                                                                                              |
| subJobs           | [cambricon.TrainingJobList](#cambricon.trainingjoblist)           | 子任务列表                                                                                                                        |
| trainingType      | string                                                            | 任务类型 (可选项: batch, normal, experiment)                                                                                      |

### 修改训练任务

修改`训练任务`

URI: PUT /v2/namespace/{namespace}/batch-trainingjob/{uid}

路径参数：

| 参数      | 是否必选 | 参数类型 | 描述       |
| --------- | -------- | -------- | ---------- |
| namespace | true     | string   | 项目 ID    |
| uid       | true     | string   | 唯一标识符 |

请求 Body 参数：

| 参数 | 是否必选 | 参数类型                                                  | 描述 |
| ---- | -------- | --------------------------------------------------------- | ---- |
| body | true     | [cambricon.BatchTrainingJob](#cambricon.batchtrainingjob) |      |

响应状态码：202

### 删除训练任务

删除`训练任务`

URI: DELETE /v2/namespace/{namespace}/trainingjob/{uid}

路径参数：

| 参数      | 是否必选 | 参数类型 | 描述       |
| --------- | -------- | -------- | ---------- |
| namespace | true     | string   | 项目 ID    |
| uid       | true     | string   | 唯一标识符 |

响应状态码：202

### 列出项目中的`子训练任务`

根据指定条件分页查询项目中的`子训练任务`。

URI: GET /v2/namespace/{namespace}/trainingjob/{uid}

路径参数：

| 参数      | 是否必选 | 参数类型 | 描述       |
| --------- | -------- | -------- | ---------- |
| namespace | true     | string   | 项目 ID    |
| uid       | true     | string   | 唯一标识符 |

响应状态码：200

Body 参数：

| 参数              | 参数类型                                                    | 描述                                                                                                                              |
| ----------------- | ----------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| communType        | string                                                      | 分布式模式 (可选项: horovod, tensorflow, pytorch, standalone)                                                                     |
| metadata          | [cambricon.ObjectMeta](#cambricon.objectmeta)               | 附加信息                                                                                                                          |
| priorityClassName | string                                                      | 任务优先级类别名。（可选项：`train-job-priority-1`（默认），`train-job-priority-3`（紧急），`train-job-priority-11`（非常紧急）） |
| spec              | [cambricon.TrainingJobSpec](#cambricon.trainingjobspec)     | 任务规格                                                                                                                          |
| status            | [cambricon.TrainingJobStatus](#cambricon.trainingjobstatus) | 任务状态                                                                                                                          |

### 停止子任务

停止批量训练任务中的子任务

URI: POST /v2/namespace/{namespace}/trainingjob/{uid}/stop

路径参数：

| 参数      | 是否必选 | 参数类型 | 描述       |
| --------- | -------- | -------- | ---------- |
| namespace | true     | string   | 项目 ID    |
| uid       | true     | string   | 唯一标识符 |

响应状态码：202

## Model 定义

### cambricon.ACL

| 参数     | 是否必选 | 参数类型        | 描述                                                                           |
| -------- | -------- | --------------- | ------------------------------------------------------------------------------ |
| effected | false    | array of string | 汇总后的权限，客户端不需要设置，由系统自动生成 (可选项: Read, Write, WriteACL) |
| project  | false    | string          | 资源设置的权限 (可选项: None, ReadWrite, ReadOnly)                             |

### cambricon.AnnotationDatasetSource

| 参数     | 是否必选 | 参数类型 | 描述           |
| -------- | -------- | -------- | -------------- |
| id       | true     | string   | 标注数据集 ID  |
| name     | true     | string   | 标注数据集名称 |
| readOnly | false    | boolean  | 是否只读       |
| version  | true     | string   | 版本           |

### cambricon.BatchTrainingJob

| 参数              | 是否必选 | 参数类型                                                          | 描述                                                                                                                              |
| ----------------- | -------- | ----------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| batched           | false    | boolean                                                           | 是否为批量训练任务。已废弃，请使用 `trainingType` 字段                                                                            |
| communType        | false    | string                                                            | 分布式模式 (可选项: horovod, tensorflow, pytorch, standalone)                                                                     |
| info              | false    | [cambricon.BatchTrainingJobInfo](#cambricon.batchtrainingjobinfo) | 训练任务状态                                                                                                                      |
| metadata          | true     | [cambricon.ObjectMeta](#cambricon.objectmeta)                     | 附加信息                                                                                                                          |
| priorityClassName | false    | string                                                            | 任务优先级类别名。（可选项：`train-job-priority-1`（默认），`train-job-priority-3`（紧急），`train-job-priority-11`（非常紧急）） |
| spec              | false    | [cambricon.BatchTrainingJobSpec](#cambricon.batchtrainingjobspec) | 规格                                                                                                                              |
| status            | false    | string                                                            | 状态                                                                                                                              |
| subJobs           | false    | [cambricon.TrainingJobList](#cambricon.trainingjoblist)           | 子任务列表                                                                                                                        |
| trainingType      | false    | string                                                            | 任务类型 (可选项: batch, normal, experiment)                                                                                      |

### cambricon.BatchTrainingJobInfo

| 参数             | 是否必选 | 参数类型                                                  | 描述             |
| ---------------- | -------- | --------------------------------------------------------- | ---------------- |
| experimentStatus | false    | [cambricon.ExperimentStatus](#cambricon.experimentstatus) | 超参数优化状态   |
| overview         | false    | string                                                    | 训练任务总体状态 |

### cambricon.BatchTrainingJobList

| 参数     | 是否必选 | 参数类型                                                           | 描述         |
| -------- | -------- | ------------------------------------------------------------------ | ------------ |
| metadata | false    | [cambricon.ListMeta](#cambricon.listmeta)                          | 附加信息     |
| items    | true     | array of [cambricon.BatchTrainingJob](#cambricon.batchtrainingjob) | 训练任务列表 |

### cambricon.CairSource

| 参数         | 是否必选 | 参数类型 | 描述                                         |
| ------------ | -------- | -------- | -------------------------------------------- |
| deleted      | false    | boolean  | 是否已删除，客户端不需要设置，由系统自动生成 |
| resourceID   | true     | string   | 资源 ID                                      |
| resourceName | false    | string   | 资源名，只读                                 |
| versionID    | true     | string   | 资源版本 ID                                  |
| versionName  | false    | string   | 资源版本名，只读                             |

### cambricon.CardUsage

| 参数     | 是否必选 | 参数类型                                      | 描述                                          |
| -------- | -------- | --------------------------------------------- | --------------------------------------------- |
| app      | false    | [cambricon.IDResponse](#cambricon.idresponse) | 应用 ID                                       |
| physical | false    | integer                                       | 物理板卡号                                    |
| vf       | false    | integer                                       | virtual function 序号（仅在开启虚拟化后可用） |

### cambricon.Error

| 参数    | 是否必选 | 参数类型 | 描述     |
| ------- | -------- | -------- | -------- |
| code    | false    | integer  | 错误码   |
| message | false    | string   | 错误信息 |

### cambricon.ExperimentSpec

| 参数                | 是否必选 | 参数类型                                                                           | 描述         |
| ------------------- | -------- | ---------------------------------------------------------------------------------- | ------------ |
| algorithm           | true     | [org.kubeflow.v1beta1.AlgorithmSpec](#org.kubeflow.v1beta1.algorithmspec)          | 算法规格     |
| earlyStopping       | false    | [org.kubeflow.v1beta1.EarlyStoppingSpec](#org.kubeflow.v1beta1.earlystoppingspec)  | 提早停止规格 |
| maxFailedTrialCount | false    | integer                                                                            | 最大失败任务 |
| maxTrialCount       | false    | integer                                                                            | 最大任务数量 |
| objective           | true     | [org.kubeflow.v1beta1.ObjectiveSpec](#org.kubeflow.v1beta1.objectivespec)          | 优化目标     |
| parallelTrialCount  | false    | integer                                                                            | 最大并行任务 |
| parameters          | true     | array of [org.kubeflow.v1beta1.ParameterSpec](#org.kubeflow.v1beta1.parameterspec) | 超参数       |

### cambricon.ExperimentStatus

| 参数                 | 是否必选 | 参数类型                                                                               | 描述             |
| -------------------- | -------- | -------------------------------------------------------------------------------------- | ---------------- |
| currentOptimalTrial  | false    | [org.kubeflow.v1beta1.OptimalTrial](#org.kubeflow.v1beta1.optimaltrial)                | 当前优化尝试状态 |
| trialObservationList | false    | array of [cambricon.ExperimentTrialObservation](#cambricon.experimenttrialobservation) | 优化尝试列表     |

### cambricon.ExperimentTrialObservation

| 参数                 | 是否必选 | 参数类型                                                                                       | 描述       |
| -------------------- | -------- | ---------------------------------------------------------------------------------------------- | ---------- |
| observation          | false    | [org.kubeflow.v1beta1.Observation](#org.kubeflow.v1beta1.observation)                          | 观测值     |
| parameterAssignments | false    | array of [org.kubeflow.v1beta1.ParameterAssignment](#org.kubeflow.v1beta1.parameterassignment) | 设置的参数 |
| status               | false    | string                                                                                         | 状态       |
| trialName            | false    | string                                                                                         | 尝试名     |

### cambricon.Flavor

| 参数                 | 是否必选 | 参数类型                                           | 描述                                                                                          |
| -------------------- | -------- | -------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| cpuMilliCoresLimit   | true     | integer                                            | CPU 最大限制，单位：千分之一核                                                                |
| cpuMilliCoresRequest | true     | integer                                            | CPU 最小需求，单位：千分之一核                                                                |
| credit               | true     | integer                                            | 每小时价格，单位： 1/10^6                                                                     |
| deleted              | false    | boolean                                            | 是否已删除，只在 flavorInfo 字段中使用                                                        |
| enabled              | false    | boolean                                            | 是否启用                                                                                      |
| ephemeralStorageGb   | true     | integer                                            | 根目录存储限制，单位：GB                                                                      |
| flavorType           | false    | string                                             | 算力规格类型 (可选项: CPU, GPU, MLU, Unknown)                                                 |
| freeReplicas         | false    | integer                                            | 空闲副本数，只在 flavorInfo 字段中使用                                                        |
| gpuMilliCores        | true     | integer                                            | GPU 卡数，单位：千分之一卡                                                                    |
| gpuType              | true     | string                                             | GPU 类型                                                                                      |
| id                   | false    | string                                             | 算力规格 ID，客户端不需要设置，创建时由系统自动生成                                           |
| mellanoxIb           | true     | integer                                            | Mellanox IB 数量                                                                              |
| mellanoxRoce         | true     | integer                                            | Mellanox RoCE 数量                                                                            |
| memMbLimit           | true     | integer                                            | 内存最大限制，单位：MB                                                                        |
| memMbRequest         | true     | integer                                            | 内存最小需求，单位：MB                                                                        |
| mluMilliCores        | true     | integer                                            | MLU 卡数，单位：千分之一卡                                                                    |
| mluType              | true     | string                                             | MLU 类型                                                                                      |
| name                 | true     | string                                             | 算力规格名称                                                                                  |
| namespace            | false    | string                                             | 算力规格所在项目，公共算力规格此字段为 public                                                 |
| nodeSelector         | false    | [cambricon.NodeSelector](#cambricon.nodeselector)  | 节点选择器                                                                                    |
| nodes                | false    | array of [cambricon.NodeInfo](#cambricon.nodeinfo) | 算力规格可用节点信息（仅在查询时 `withNode` 参数为 true 且开启了 `ShowNodes` 功能开关时列出） |
| totalReplicas        | false    | integer                                            | 集群最多能够创建满足此算力规格的容器数量，仅在查询时使用                                      |

### cambricon.FlavorList

| 参数     | 是否必选 | 参数类型                                       | 描述         |
| -------- | -------- | ---------------------------------------------- | ------------ |
| metadata | false    | [cambricon.ListMeta](#cambricon.listmeta)      | 列表附加信息 |
| items    | true     | array of [cambricon.Flavor](#cambricon.flavor) | 算力规格列表 |

### cambricon.GitRepoSource

| 参数     | 是否必选 | 参数类型 | 描述                               |
| -------- | -------- | -------- | ---------------------------------- |
| deleted  | false    | boolean  | 是否已删除                         |
| httpURL  | false    | string   | HTTP URL                           |
| id       | false    | string   | 唯一标识符                         |
| ref      | false    | string   | git branch 或者 tag                |
| repoName | false    | string   | 仓库名，只读字段，客户端不需要设置 |

### cambricon.IDResponse

| 参数 | 是否必选 | 参数类型 | 描述                                                                                                                                                                                                                                                                                                                                                          |
| ---- | -------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| id   | false    | string   | 唯一标识符                                                                                                                                                                                                                                                                                                                                                    |
| name | false    | string   | 名称                                                                                                                                                                                                                                                                                                                                                          |
| type | false    | string   | 资源类型 (可选项: algorithm, cairfavoritealgorithm, cairfavoritedataset, dataset, evaluationjob, flavor, inference, job, modelconversion, modelpackage, modelpackageversion, notebook, persistentvolumeclaim, predictor, predictorjob, pretrainedmodel, sampleset, savedmodel, server, sharedalgorithm, shareddataset, sharedmodel, tensorboard, trainingjob) |

### cambricon.Label

| 参数        | 是否必选 | 参数类型 | 描述                                                 |
| ----------- | -------- | -------- | ---------------------------------------------------- |
| color       | false    | string   | 颜色                                                 |
| createdAt   | false    | string   | 创建时间，客户端不需要设置，创建时由系统自动生成     |
| description | false    | string   | 描述                                                 |
| id          | false    | string   | 标签 ID，客户端不需要设置，创建时由系统自动生成      |
| name        | true     | string   | 标签名称                                             |
| namespace   | false    | string   | 标签所在项目 ID                                      |
| updatedAt   | false    | string   | 标签更新时间，客户端不需要设置，更新时由系统自动生成 |

### cambricon.ListMeta

| 参数   | 是否必选 | 参数类型 | 描述                                               |
| ------ | -------- | -------- | -------------------------------------------------- |
| status | true     | object   | 状态映射，key 为状态，value 为处于该状态资源的数量 |
| total  | true     | integer  | 资源数量                                           |

### cambricon.NodeInfo

| 参数          | 是否必选 | 参数类型                                             | 描述             |
| ------------- | -------- | ---------------------------------------------------- | ---------------- |
| cardUsage     | false    | array of [cambricon.CardUsage](#cambricon.cardusage) | 板卡使用情况     |
| cpuType       | false    | string                                               | CPU 类型         |
| driverVersion | false    | string                                               | 驱动版本         |
| gpuType       | false    | string                                               | GPU 型号         |
| kernelVersion | false    | string                                               | 操作系统内核版本 |
| mluType       | false    | string                                               | MLU 型号         |
| name          | false    | string                                               | 节点名称         |
| os            | false    | string                                               | 操作系统         |
| total         | false    | map<string, string>                                  | 节点所有资源     |
| used          | false    | map<string, string>                                  | 节点已用资源     |

### cambricon.ObjectMeta

| 参数              | 是否必选 | 参数类型                                     | 描述                                                 |
| ----------------- | -------- | -------------------------------------------- | ---------------------------------------------------- |
| creationTimestamp | false    | string                                       | 创建时间戳，客户端不需要设置，创建时由系统自动生成   |
| deletionTimestamp | false    | string                                       | 删除时间戳，客户端不需要设置，删除时由系统自动生成   |
| labels            | false    | array of [cambricon.Label](#cambricon.label) | 标签，仅对部分资源有效                               |
| name              | true     | string                                       | 资源名称                                             |
| namespace         | false    | string                                       | 资源所在项目 ID                                      |
| uid               | false    | string                                       | 资源 ID，客户端不需要设置，创建时由系统自动生成      |
| userID            | false    | string                                       | 创建人 ID，客户端不需要设置，创建时由系统自动生成    |
| username          | false    | string                                       | 创建人用户名，客户端不需要设置，创建时由系统自动生成 |

### cambricon.TrainingAlgorithmSpec

| 参数                   | 是否必选 | 参数类型                                                     | 描述                                         |
| ---------------------- | -------- | ------------------------------------------------------------ | -------------------------------------------- |
| algorithmGits          | false    | array of [cambricon.GitRepoSource](#cambricon.gitreposource) | 算法用 Git 仓库                              |
| algorithmVolumes       | false    | array of [cambricon.VolumeSource](#cambricon.volumesource)   | 我的算法卷                                   |
| beginner               | false    | boolean                                                      | 初学者模式（仅 UI 使用，不影响训练任务行为） |
| cairFavoriteAlgorithms | false    | array of [cambricon.CairSource](#cambricon.cairsource)       | 算法收藏                                     |
| command                | true     | array of string                                              | 命令（仅 UI 使用，不影响训练任务行为）       |
| executionCommand       | false    | string                                                       | 执行命令（仅 UI 使用，不影响训练任务行为）   |
| postCommand            | false    | string                                                       | 训练后命令（仅 UI 使用，不影响训练任务行为） |
| preCommand             | false    | string                                                       | 初始化命令（仅 UI 使用，不影响训练任务行为） |

### cambricon.TrainingJob

| 参数              | 是否必选 | 参数类型                                                    | 描述                                                                                                                              |
| ----------------- | -------- | ----------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| communType        | false    | string                                                      | 分布式模式 (可选项: horovod, tensorflow, pytorch, standalone)                                                                     |
| metadata          | true     | [cambricon.ObjectMeta](#cambricon.objectmeta)               | 附加信息                                                                                                                          |
| priorityClassName | false    | string                                                      | 任务优先级类别名。（可选项：`train-job-priority-1`（默认），`train-job-priority-3`（紧急），`train-job-priority-11`（非常紧急）） |
| spec              | false    | [cambricon.TrainingJobSpec](#cambricon.trainingjobspec)     | 任务规格                                                                                                                          |
| status            | false    | [cambricon.TrainingJobStatus](#cambricon.trainingjobstatus) | 任务状态                                                                                                                          |

### cambricon.TrainingJobBasicSpec

| 参数                 | 是否必选 | 参数类型                                                                         | 描述                                                                                    |
| -------------------- | -------- | -------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| acl                  | false    | [cambricon.ACL](#cambricon.acl)                                                  | 访问权限信息                                                                            |
| annotationDatasets   | false    | array of [cambricon.AnnotationDatasetSource](#cambricon.annotationdatasetsource) | 标注数据集                                                                              |
| cairFavoriteDatasets | false    | array of [cambricon.CairSource](#cambricon.cairsource)                           | 数据集收藏                                                                              |
| cairFavoriteModels   | false    | array of [cambricon.CairSource](#cambricon.cairsource)                           | 模型收藏                                                                                |
| driverVersion        | false    | string                                                                           | 驱动版本                                                                                |
| flavorID             | false    | string                                                                           | 算力规格 ID。已废弃，请使用 `flavorIDs` 字段                                            |
| flavorIDs            | false    | array of string                                                                  | 算力规格 ID 列表                                                                        |
| flavorInfo           | false    | [cambricon.Flavor](#cambricon.flavor)                                            | 算力规格信息，客户端不需要设置，获取时由系统自动生成。已废弃，请使用 `flavorInfos` 字段 |
| flavorInfos          | false    | array of [cambricon.Flavor](#cambricon.flavor)                                   | 算力规格信息，客户端不需要设置，获取时由系统自动生成                                    |
| image                | true     | string                                                                           | 镜像                                                                                    |
| inputModelVolumes    | false    | array of [cambricon.VolumeSource](#cambricon.volumesource)                       | 输入模型卷                                                                              |
| masterCount          | false    | integer                                                                          | Master 数量                                                                             |
| masterFlavorID       | false    | string                                                                           | Master 算力规格 ID                                                                      |
| modelVolumes         | false    | array of [cambricon.VolumeSource](#cambricon.volumesource)                       | 输出模型卷                                                                              |
| persistentVolumes    | false    | array of [cambricon.VolumeSource](#cambricon.volumesource)                       | 存储卷                                                                                  |
| pretrainVolumes      | false    | array of [cambricon.VolumeSource](#cambricon.volumesource)                       | 预训练模型卷                                                                            |
| sampleSets           | false    | array of [cambricon.VolumeSource](#cambricon.volumesource)                       | 样本集                                                                                  |
| sampleVolumes        | false    | array of [cambricon.VolumeSource](#cambricon.volumesource)                       | 我的数据集                                                                              |
| volumes              | false    | array of string                                                                  | 存储卷                                                                                  |
| workerCount          | true     | integer                                                                          | Worker 数量                                                                             |

### cambricon.TrainingJobList

| 参数     | 是否必选 | 参数类型                                                 | 描述     |
| -------- | -------- | -------------------------------------------------------- | -------- |
| metadata | false    | [cambricon.ListMeta](#cambricon.listmeta)                | 附加信息 |
| items    | true     | array of [cambricon.TrainingJob](#cambricon.trainingjob) | 列表     |

### cambricon.TrainingJobStatus

| 参数         | 是否必选 | 参数类型 | 描述               |
| ------------ | -------- | -------- | ------------------ |
| failed       | false    | integer  | 错误任务数量       |
| flavorIndex  | false    | integer  | 选择的算力规格序号 |
| minAvailable | false    | integer  | 最小可用数量       |
| overview     | false    | string   | 状态概览           |
| pending      | false    | integer  | 等待任务数量       |
| retryCount   | false    | integer  | 重试次数           |
| running      | false    | integer  | 运行任务数量       |
| succeeded    | false    | integer  | 成功任务数量       |
| terminating  | false    | integer  | 正在中止任务数量   |
| unknown      | false    | integer  | 未知状态任务数量   |
| version      | false    | integer  | 版本               |

### cambricon.TrainingVolume

| 参数     | 是否必选 | 参数类型                                                          | 描述     |
| -------- | -------- | ----------------------------------------------------------------- | -------- |
| metadata | true     | [cambricon.ObjectMeta](#cambricon.objectmeta)                     | 附加信息 |
| spec     | true     | [cambricon.TrainingVolumeSpec](#cambricon.trainingvolumespec)     | 规格     |
| status   | false    | [cambricon.TrainingVolumeStatus](#cambricon.trainingvolumestatus) | 状态     |

### cambricon.TrainingVolumeList

| 参数     | 是否必选 | 参数类型                                                       | 描述         |
| -------- | -------- | -------------------------------------------------------------- | ------------ |
| metadata | false    | [cambricon.ListMeta](#cambricon.listmeta)                      | 列表附加信息 |
| items    | true     | array of [cambricon.TrainingVolume](#cambricon.trainingvolume) | 训练用卷列表 |

### cambricon.TrainingVolumeSpec

| 参数             | 是否必选 | 参数类型                        | 描述                                                      |
| ---------------- | -------- | ------------------------------- | --------------------------------------------------------- |
| acl              | false    | [cambricon.ACL](#cambricon.acl) | 访问权限信息                                              |
| pvcName          | false    | string                          | K8s 中的 PVC 名称，客户端不需要设置，创建时由系统自动生成 |
| storageClassName | true     | string                          | 存储集群名称                                              |
| storageSize      | true     | integer                         | 存储容量，单位：GB                                        |

### cambricon.TrainingVolumeStatus

| 参数         | 是否必选 | 参数类型 | 描述                                                       |
| ------------ | -------- | -------- | ---------------------------------------------------------- |
| importStatus | false    | string   | 训练用卷状态 (可选项: Creating, Running, Error, Succeeded) |
| phase        | false    | string   | 训练用卷所处阶段 (可选项: Pending, Bound, Lost)            |

### cambricon.VolumeSource

| 参数     | 是否必选 | 参数类型 | 描述                                           |
| -------- | -------- | -------- | ---------------------------------------------- |
| deleted  | false    | boolean  | 是否已删除，客户端不需要设置，由系统自动生成   |
| id       | true     | string   | 卷 ID                                          |
| name     | false    | string   | 卷名，客户端不需要设置，由系统自动生成         |
| readOnly | false    | boolean  | 是否只读                                       |
| source   | false    | string   | 选择`我的`还是`公共` (可选项: private, shared) |

### org.kubeflow.v1beta1.AlgorithmSetting

| 参数  | 是否必选 | 参数类型 | 描述     |
| ----- | -------- | -------- | -------- |
| name  | false    | string   | 设置名称 |
| value | false    | string   | 设置值   |

### org.kubeflow.v1beta1.AlgorithmSpec

| 参数              | 是否必选 | 参数类型                                                                                 | 描述                                                  |
| ----------------- | -------- | ---------------------------------------------------------------------------------------- | ----------------------------------------------------- |
| algorithmName     | false    | string                                                                                   | 搜索算法 (可选项: random, grid, bayesianoptimization) |
| algorithmSettings | false    | array of [org.kubeflow.v1beta1.AlgorithmSetting](#org.kubeflow.v1beta1.algorithmsetting) | 算法参数                                              |

### org.kubeflow.v1beta1.EarlyStoppingSpec

| 参数              | 是否必选 | 参数类型                                                                                 | 描述                        |
| ----------------- | -------- | ---------------------------------------------------------------------------------------- | --------------------------- |
| algorithmName     | false    | string                                                                                   | 算法名 (可选项: medianstop) |
| algorithmSettings | false    | array of [org.kubeflow.v1beta1.AlgorithmSetting](#org.kubeflow.v1beta1.algorithmsetting) | 算法参数                    |

### org.kubeflow.v1beta1.FeasibleSpace

| 参数 | 是否必选 | 参数类型        | 描述   |
| ---- | -------- | --------------- | ------ |
| list | false    | array of string | 数列   |
| max  | false    | string          | 最大值 |
| min  | false    | string          | 最小值 |
| step | false    | string          | 间隔   |

### org.kubeflow.v1beta1.Metric

| 参数   | 是否必选 | 参数类型 | 描述   |
| ------ | -------- | -------- | ------ |
| latest | false    | string   | 最新值 |
| max    | false    | string   | 最大值 |
| min    | false    | string   | 最小值 |
| name   | false    | string   | 名称   |

### org.kubeflow.v1beta1.MetricStrategy

| 参数  | 是否必选 | 参数类型 | 描述                            |
| ----- | -------- | -------- | ------------------------------- |
| name  | false    | string   | 指标名称                        |
| value | false    | string   | 策略 (可选项: min, max, latest) |

### org.kubeflow.v1beta1.ObjectiveSpec

| 参数                  | 是否必选 | 参数类型                                                                             | 描述                                  |
| --------------------- | -------- | ------------------------------------------------------------------------------------ | ------------------------------------- |
| additionalMetricNames | false    | array of string                                                                      | 附加指标名                            |
| goal                  | false    | number                                                                               | 优化目标                              |
| metricStrategies      | false    | array of [org.kubeflow.v1beta1.MetricStrategy](#org.kubeflow.v1beta1.metricstrategy) | 指标策略                              |
| objectiveMetricName   | false    | string                                                                               | 搜索指标                              |
| type                  | false    | string                                                                               | 优化方向 (可选项: minimize, maximize) |

### org.kubeflow.v1beta1.Observation

| 参数    | 是否必选 | 参数类型                                                             | 描述     |
| ------- | -------- | -------------------------------------------------------------------- | -------- |
| metrics | false    | array of [org.kubeflow.v1beta1.Metric](#org.kubeflow.v1beta1.metric) | 观测指标 |

### org.kubeflow.v1beta1.OptimalTrial

| 参数                 | 是否必选 | 参数类型                                                                                       | 描述       |
| -------------------- | -------- | ---------------------------------------------------------------------------------------------- | ---------- |
| bestTrialName        | false    | string                                                                                         | 最佳尝试名 |
| observation          | false    | [org.kubeflow.v1beta1.Observation](#org.kubeflow.v1beta1.observation)                          | 观测状态   |
| parameterAssignments | false    | array of [org.kubeflow.v1beta1.ParameterAssignment](#org.kubeflow.v1beta1.parameterassignment) | 参数设置   |

### org.kubeflow.v1beta1.ParameterAssignment

| 参数  | 是否必选 | 参数类型 | 描述   |
| ----- | -------- | -------- | ------ |
| name  | false    | string   | 参数名 |
| value | false    | string   | 参数值 |

### org.kubeflow.v1beta1.ParameterSpec

| 参数          | 是否必选 | 参数类型                                                                  | 描述                                                    |
| ------------- | -------- | ------------------------------------------------------------------------- | ------------------------------------------------------- |
| feasibleSpace | false    | [org.kubeflow.v1beta1.FeasibleSpace](#org.kubeflow.v1beta1.feasiblespace) | 搜索间隔                                                |
| name          | false    | string                                                                    | 超参数名称                                              |
| parameterType | false    | string                                                                    | 超参数类型 (可选项: double, int, discrete, categorical) |
