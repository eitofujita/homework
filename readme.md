## patch1 ブランチでの作業手順

1. patch1 ブランチ作成
```bash
git checkout -b patch1
```

2. `using namespace std;` を削除  
`hello_world.cpp` を開いて `using namespace std;` を消し、`std::cout` / `std::endl` に直す。

例:
```cpp
#include <iostream>
int main() {
    std::cout << "Hello World" << std::endl;
    return 0;
}
```

3. commit / push
```bash
git add hello_world.cpp
git commit -m "remove using namespace std"
git push -u origin patch1
```

4. リモートに patch1 があるか確認
```bash
git branch -a
```
`remotes/origin/patch1` が見えれば OK。

5. patch1 -> master の PR作成  
GitHub のリポジトリ画面で **Compare & pull request** を押して作成。  
CLI なら:
```bash
gh pr create --base master --head patch1 --title "patch1" --body "remove using namespace std"
```

6. patch1 でコメント追加  
`hello_world.cpp` にコメント1行追加（例: `// print greeting`）。

7. commit / push
```bash
git add hello_world.cpp
git commit -m "add comment to hello_world.cpp"
git push
```

8. PRに反映確認  
GitHub の同じ PR ページを更新し、最新コミットが増えていれば OK。  
（同じブランチ `patch1` への push は PR に自動反映される）

9. PRをマージして、リモート patch1 削除  
GitHub で **Merge pull request** -> **Delete branch**。

10. ローカルで pull
```bash
git checkout master
git pull origin master
```

11. `git log` 確認
```bash
git log --oneline --graph --decorate -n 10
```

12. ローカル patch1 削除
```bash
git branch -d patch1
```

詰まりやすいポイントは `git status` / `git branch -a` で毎回確認すると解決しやすいです。
