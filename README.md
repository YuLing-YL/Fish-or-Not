# 钓否

零构建、纯前端的响应式钓鱼天气建议页。直接打开 `index.html`，或部署至 GitHub Pages / Vercel 静态站点即可。

## 数据与降级

- 优先浏览器 Geolocation，拒绝或超时后回退 IP 位置（ipapi.co）。
- 使用 Open-Meteo 取得当前、过去 24 小时与未来 3 天逐小时的气温、相对湿度、海平面气压、风速、降水和天气代码；Open-Meteo 返回的海拔会修正气压目标区间。
- 定位成功后使用 BigDataCloud 免费反向地理编码取得“省/市 + 区/县”；该服务不可用时回退 Open-Meteo 反向编码，最后显示坐标。
- 请求失败时不展示伪造数据，而给出刷新重试提示。

## 地区鱼种筛选

候选鱼种会先按省级地区白名单筛选，再参与评分和环形图归一化。无法识别省份时仅显示全国常见的鲫鱼、鲤鱼、草鱼、鲢鳙、翘嘴、黑鱼、马口、黄颡鱼、鲶鱼、鳊鱼等。罗非和鲮鱼仅在华南候选；狗鱼仅东北/新疆候选，河鲈仅新疆候选；西北不推荐鳜鱼。为安全起见，中华鲟、胭脂鱼、松江鲈、哲罗鲑等保护鱼类以及清道夫等入侵种未被写入任何推荐候选。

## 模型说明

每条鱼的基础适宜度由绝对气压 35%、24h 气压变化 10%、温度 20%、时段 10%、湿度/风速/降水/季节/水域各 5% 加权；随后仅在当前场景的目标鱼中归一化为环形图的相对概率。鱼塘使用轻微的鱼密度/投喂修正，降低天气的极端影响，但不会抹去低压闷热的风险。

这些是面向出钓的经验型启发式规则，并非真实上鱼率预测。水温、溶氧、投喂、鱼密度、水深、水色与当地禁渔规则仍应由钓者现场确认。

## 参考依据

- [Texas Parks & Wildlife：低光照的晨昏时段更利于进食](https://tpwd.texas.gov/education/resources/aquatic-science/tas/chapters/chapter-13/)
- [TPWD：鲈鱼与鲶鱼的偏好水温范围](https://tpwd.texas.gov/publications/pwdpubs/media/pwd_br_k0700_0162_01_11.pdf)
- [UF/IFAS：高温、阴天和暴雨与池塘低溶氧风险](https://edis.ifas.ufl.edu/publication/FA002/pdf)
- [USGS：溶氧受温度、气压与水体混合影响](https://pubs.usgs.gov/publication/ofr20241043/full)
- [农业农村部：罗非鱼主产区覆盖广东、福建、广西、海南和云南](https://yyj.moa.gov.cn/fzgh/201904/t20190419_6208331.htm)
- [新疆农业农村厅：额尔齐斯河/乌伦古湖有白斑狗鱼等冷水鱼](https://nynct.xinjiang.gov.cn/xjnynct/c113577/202309/1eedf14c7de14c87afd53ac71c5d2e88.shtml)
- [国家重点保护野生动物名录](https://www.beijing.gov.cn/zhengce/zhengcefagui/qtwj/202311/t20231120_3304775.html)
