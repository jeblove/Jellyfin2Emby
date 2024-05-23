# Jellyfin2Emby

[English Documentation](./README.en.md)

> 将Jellyfin用户以及用户观看记录迁移到Emby

该脚本基于[Marc-Vieg/Emby2Jelly](https://github.com/Marc-Vieg/Emby2Jelly)修改为Jellyfin2Emby

已知缺陷：

1. 未能准确迁移【继续观看】中播放具体进度；
   迁移后为该影片(剧集)未播放
   例如：jellyfin A剧集播放到S01E03的10分钟，迁移后为Emby A剧集S01E03未播放
2. 未能迁移【喜爱】的影片记录
3. 密码未能迁移

---

### 测试版本

- jellyfin：10.8.13

- emby：4.8.7.0

---

### 检查

**确保你的内容已经被识别（建议在你的库中刷新缺失的元数据）**

确保让Emby和Jellyfin搜索缺失的元数据，甚至每个电视剧集都需要有其providerIds才能被正确迁移。

---
### Requirements

python3
```
json
requests
urllib.parse
configobj
time
getpass
```
---

### 配置

编辑settings.ini文件并添加你的Emby和Jellyfin的URL和API密钥
```
[Emby]
EMBY_APIKEY = aaaabbbbbbbcccccccccccccdddddddd
EMBY_URLBASE = http://127.0.0.1:8097/
EMBY_PASSWORD = passwordAZ
[Jelly]
JELLY_APIKEY = eeeeeeeeeeeeeeeffffffffffffffffggggggggg
JELLY_URLBASE = http://127.0.0.1:8096/

# 结尾需要有斜杠/

## 如果你有自定义路径或者反向代理，不要忘记 /emby/ 或者 /jelly/
```

---

### 使用

从jellyfin迁移到emby

```
python3 jellyfin2emby.py
参数：（一次只能使用一个文件，每次运行一个文件，一次从文件运行）
		--tofile [文件]     运行脚本，将查看状态保存到文件而不是发送到目标服务器
		--fromfile [文件]   运行脚本，以文件作为源服务器并将查看状态发送到目标服务器
		--new-user-pw "change-your-password-9efde123"
```

（密码顺序，优先new-user-pw参数，其次settings.ini中EMBY_PASSWORD，最后则是运行时手动输入）

---

### 结果

脚本将生成一个RESULTS.txt，包含每个用户的摘要和未找到的媒体列表：
```
                      ### Jelly2Emby ###


fish (Jellyfin) is  fish (Emby)
user0 Created on Emby


--- fish ---
Medias Migrated : 71 / 71
--- user0 ---
Medias Migrated : 1 / 1
```

---

### 感谢

再次感谢Emby2Jelly原作者Marc-Vieg(CobayeGunther)