# 复现

主测试文件位于 cases/<case_id>/scenario.xosc，相对引用同目录 map.xodr。运行器为 CARLA 0.9.16 + 本项目 ScenarioRunner + PCLA 的 if_if（InterFuser），hero 始终为外部自主控制。

请在 crash2openx 仓库中配置自己的 CARLA_REMOTE_* 后，使用 tools/carla_remote.py 的 run 子命令。每例 evidence/runtime_code 和 runtime_manifest.json 保留了实测版本，场景需支持 ADS 同时条件、真实车身净空、生成车道路由和 Act 停止条件。库存 ScenarioRunner 的条件锁存语义不能替代这些扩展。

复现编译可使用 tools/expand_ads_batch.py，批量筛选用 tools/review_ads_expansion.py。原始种子在 source/，实验种子在 scene_seed.json。地图几何与对应原生 CARLA 检查见 evidence/roadgraph_selfcheck.json。

直接重跑可能出现不同轨迹；本包只证明所附日志对应的单次试验。evidence/scenario.runtime.xosc 是运行时证据，可能含服务器绝对路径，请使用案例目录的 scenario.xosc 作为入口。

示例（在已有依赖和远端运行环境的仓库中运行，路径替换为解压后的实际位置）：

```sh
CASE_DIR=/absolute/path/to/ads_showcase_10_20260919/cases/013_Zoox_February_19_2025
uv run python tools/carla_remote.py run --xodr "$CASE_DIR/map.xodr" --xosc "$CASE_DIR/scenario.xosc" --pcla-agent if_if --sut-actor hero --rgb-actor-role hero --max-seconds 600 --scene-seed "$CASE_DIR/scene_seed.json" --road-seed "$CASE_DIR/source/road_seed.json"
```

`implementation_snapshot/` 保存本轮编译、筛选及打包实现，需配合原仓库依赖；不包含 CARLA、模型权重或登录凭据。每例的 runtime_code 则保存该次运行实际使用的文件，早期和最终运行的停止条件版本可能不同。

`manifest.json` 的 source_scene 与 derived_scene 可直接比较参数变化。262 使用仍保持低速行驶的减速变体，避开当前 CARLA 车辆低速停住时的非物理速度尖峰，不能声称复现完全停车。038 的完整运行达到墙钟超时，仅验收所附交互窗口。

时序图的圆点表示片段起点，三角表示终点；底部净空/TTC 为动作后最多六秒的窗口指标。视频可延伸到之后的接触，接触由真实碰撞传感器证据确认。
