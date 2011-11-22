for-jigsaw
======================
じぐぃ。
 
発端
------
[これを見て](https://github.com/e-jigsaw/tumblub)  
[こうなって](http://twitter.com/#!/asonas/status/138654705994842112)  
[こんなこというから](http://twitter.com/#!/neo6120/status/138654770641645568)  
[こうしてやった](http://twitter.com/#!/asonas/status/138683758059597825)  


補足
------
半分おふざけだけど、簡単にbranchとtagについて説明するためのリポジトリ  
あと自分の理解度についての言及  


実際には
------
ぶっちゃけると[この記事](http://nvie.com/posts/a-successful-git-branching-model/)を読むとわかることなんだけど  
英語ができないと聞くから実際にやって説明してやろうと思ったら実は[日本語訳の記事](http://keijinsonyaban.blogspot.com/2010/10/successful-git-branching-model.html)があって、んじゃこれでおｋってなった  
gitでうまくWebサービスを運用するための方法とかはまさにこれを読めばいいと思う。  


三行で
------
* 最高に楽をして開発しようぜ
* ブランチ切るのにびびるな
* CVS,SVNクソ


もうちょっと詳しく
----------------
`git init`  
`git add .`  
`git commit`  
ここまでテンプレ  

`git checkout -b develop #developブランチを切る`  
`git checkout -b develop master #masterブランチを明示的に指定してブランチを切る`  
なんやかんや開発する  
`git commit -a #developブランチ上でコミット`  
`git branch #ブランチの一覧を表示して、今自分がいるブランチ名を表示`  
`git branch -a #リモートも含むブランチの一覧を表示`  
バグもなさそうだし、安定版のmasterにマージする  
`git checkout master #masterブランチに移動`  
`git merge develop #developブランチで作業した内容をmasterにマージ`  
`git merge --no-ff develop #記事で紹介されてたけどdevelop上でやった作業内容もちゃんと履歴として残してくれる`  



ブランチはわかったけどtagってなんだよ
------
良く使うのはバージョン番号をスタンプする  
`git tag #tag全部を見る`  
`git tag v0.0.0 #v0.0.0でタグを置く`  
バージョン番号はなんでも良いと思う  
versionX.X.X  
releaseX.X  
数字以外の部分は正直どうでも良いと思う  
けど、リポジトリを外に公開したり、マイルストーンを置いて開発するときは  
メジャーバージョン番号 マイナーバージョン番号 バグフィックス  
とそれぞれ振っておくと外の人はわかりやすいと思う  


バージョン番号をスタンプするだけなの？
----------------
だけではなくて、例えばこのリポジトリをcloneして  
`git show fb8dd93`  
と  
`git show v0.1.1`  
を叩くとおそらく同じ結果が返るはず。  

つまり`fb8dd93`というハッシュに対して`v0.1.1`というエイリアスを張ってると考えても多分いい  
「なんだただのエイリアスか」  
ではなくてどこかのサーバにv0.1.1のときの状態をデプロイしたいときに、このタグが使える  

`git clone git://github.com/asonas/for-jigsaw.git`  
`git tag #v0.0.1のタグがあることを確認する`  
`git tag -l #なかったら-lオプションで引っ張ってくる`  
`git checkout v0.1.1 #これでv0.1.1の状態で展開できた`  

それ以外でもたとえばv0.2.0でデプロイしちゃったけど盛大にバグがあってサービスがとまっちゃった！ってときにも  
`git checkout v0.1.1`  
と叩けば昔の状態に戻れる  



他にも
----------------
Githubを使ってると、とにかくブランチを沢山きったり(切りすぎても微妙だけど)、タグをスタンプしまくるのが楽しい
[NetworkのGraph](https://github.com/asonas/for-jigsaw/network)を見てみるとわかるけど、自分の作業履歴をTree上に表示してくれる！  
adminからコラボレータを登録して複数人で開発するときでももちろんこのGraphは作業人分だけ反映してくれる。  

いろいろかくことはあるけど、  
* `git branch`  
* `git checkout`  
* `git tag`  
を理解できたら相当楽しいし、すでに動いてるサービスのこと気にしないで気楽に開発ができると思う  


なにかあったら
----------------
是非ともIssueなりpull requestとか送ると良いと思う！あなたがGithub-erなら！  
