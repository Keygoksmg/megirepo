## GitHub API v3 

### Access token を取得する
```
AUTH_HDR="Authorization: bearer $TOKEN"
```
### リポジトリを作成する
```
curl -H "$AUTH_HDR" -X POST \
    -d '{"name":"megirepo","auto_init":true}' \
    https://api.github.com/user/repos

REPO="api.github.com/repos/Keygoksmg/megirepo"
```
git push --set-upstream origin 287-megi
### BLOB を作成する
- ファイルをアップロード
```
CONTENT=`cat megimegi.txt`

curl -H "$AUTH_HDR" -X POST \
    -d "{\"content\":\"$CONTENT\",\"encoding\":\"utf-8\"}" \
    https://$REPO/git/blobs

>>> {
	  "url": "https://api.github.com/repos/ngs/testrepos0001/git/blobs/03c6fa49370fb5ff5c5b57f134c4f0b3f9b8fc44",
	  "sha": "03c6fa49370fb5ff5c5b57f134c4f0b3f9b8fc44"
	}

BLOB1_SHA=03c6fa49370fb5ff5c5b57f134c4f0b3f9b8fc44

```

- バイナリの場合
```
CONTENT=`curl https://help.github.com/assets/set-up-git.gif | base64`

curl -H "$AUTH_HDR" -X POST \
    -d "{\"content\":\"$CONTENT\",\"encoding\":\"base64\"}" \
    https://$REPO/git/blobs

>>> {
	  "url": "https://api.github.com/repos/ngs/testrepos0001/git/blobs/def187dee0bb8478f502f2c6942a19dbaca24118",
	  "sha": "def187dee0bb8478f502f2c6942a19dbaca24118"
	}

BLOB2_SHA=def187dee0bb8478f502f2c6942a19dbaca24118
```

### Tree を作成する
```
curl -H "$AUTH_HDR" -X POST \
    -d "{\"tree\":[
      {\"path\":\"megimegi.txt\",\"mode\":\"100644\",\"type\":\"blob\",\"sha\":\"$BLOB1_SHA\"}
    ]}" \
    https://$REPO/git/trees

>>> ...

TREE_SHA=0583674d7b9fbe9a77d6d06b4b6ef14143a56dd5
```

### 現在の Commit の SHA を取得する
```

```

### Commit を作成する
```

```

### Refを更新する
```

```