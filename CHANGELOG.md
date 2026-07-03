# AAP Workflow CHANGELOG

## v0.2

基线文件：`AAP_v0.1.json`（即之前从 `github.com/DaibinThink/AAP` 仓库读取、id为 `92112d97-bb64-4b44-86f2-ea5691ef8f6e` 的官方Kernel workflow）

本版本**只做工程整理，不做Prompt升级，不改任何推理逻辑**。

---

### [Added] 新增内容

**新增 3 个 Group：**
- `Output`（id=7）：预留给 VAEDecode(124)、SaveImage(94) 所在区域的可视化分组框（仅新增分组框，未移动、未修改这两个节点本身）
- `Documentation`（id=8）：包含新增的 "AAP Documentation" 说明节点
- `Future Expansion`（id=9）：包含新增的 "Future Expansion" 说明节点

**新增 2 个 MarkdownNote 节点（纯文档，无input/output，不参与实际推理）：**

| 节点id | 标题 | 内容概要 |
|---|---|---|
| 900 | AAP Documentation | AAP版本号、基线Workflow说明、模型版本清单、推荐CFG(1)/Steps(4)/分辨率来源说明、实验记录占位 |
| 901 | Future Expansion | 列出规划中的扩展方向：Reference 3/4、Material/Lighting/Furniture/Landscape Conditioning，明确标注均为占位说明，未实现任何实际节点 |

---

### [Changed] 变更内容

**仅2处Group标题重命名（只改`title`字段，未改`id`/`bounding`/所含节点）：**
- `Sampler` → `Sampling`
- `Reference Conditioning` → `Reference`

**元数据：**
- `last_node_id`：692 → 901
- `revision`：0 → 1

---

### [Unchanged] 明确未改动内容（已逐字节校验）

以下内容与 v0.1 **逐字节完全一致**，未做任何修改：

- 全部23个原有节点（id、type、pos、size、widgets_values、inputs、outputs、properties、flags、order、mode 均未变）
  - UNETLoader (126)
  - CLIPLoader (133)
  - VAELoader (127)
  - CLIPTextEncode (135) —— Prompt文本内容未改
  - ConditioningZeroOut (685)
  - FluxKVCache (139)
  - CFGGuider (138) —— CFG=1 未改
  - KSamplerSelect (122)
  - Flux2Scheduler (137) —— 步数4未改
  - EmptyFlux2LatentImage (129)
  - SamplerCustomAdvanced (123)
  - RandomNoise (125)
  - VAEDecode (124)
  - SaveImage (94)
  - GetImageSize (128)
  - ImageScaleToTotalPixels (130, 131)
  - LoadImage (76, 81)
  - Reference Conditioning Subgraph实例 (134, 132)
  - 原有MarkdownNote (97, 692)
- `links` 数组（29条连接，全部link id/origin/target/slot完全一致）
- `definitions.subgraphs`（2个Subgraph定义，含内部ReferenceLatent/VAEEncode节点及内部links，完全一致）
- `config`、`extra`、`floatingLinks`
- 顶层 `id`（workflow id）
- `version`（0.4）
- 原有5个Group的 `bounding`（坐标范围）及所含节点归属

---

### 校验记录

生成后已执行以下自动化校验：

1. 原有23个节点逐字节diff：**PASS**（无任何一个节点被修改）
2. `links` 数组整体比对：**PASS**（完全一致）
3. `definitions`（Subgraph定义）整体比对：**PASS**（完全一致）
4. 节点id唯一性检查：**PASS**（25个节点，无重复）
5. Group id唯一性检查：**PASS**（8个Group，无重复）
6. JSON可正常解析（结构完整）：**PASS**

---

*本版本严格遵循"只允许新增Group和说明性MarkdownNote，禁止修改Kernel节点、Prompt、CFG、Scheduler、ReferenceLatent、Condition Flow"的约束。*

