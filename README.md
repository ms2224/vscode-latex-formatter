# VSCode + LaTeXフォーマッター(latexindent) 導入手順メモ

Windows環境のVSCodeでLaTeX Workshopを使い，`latexindent`でソースコードを自動整形するための設定手順．

## 1. 前提

- Visual Studio Code
- TeX Live
- LaTeX Workshop (VSCode拡張機能)

上記がインストール済みであること．
ここではWindows環境でのセットアップについて．

---

## 2. Perlのインストール

`latexindent` はPerlスクリプトのため，Perlの実行環境が必要．今回は **Strawberry Perl** でインストール．

（3. の ```latexindent -V``` が通ればPerlのインストールは不要？ texliveインストール時に ```"C:\texlive\2024\bin\windows\latexindent.exe"``` があった．）

1. [Strawberry Perlの公式サイト](http://strawberryperl.com/)へアクセス．
2. 推奨バージョンをダウンロードし，インストーラーの指示に従いインストールする．
3. PCを再起動する．

インストール後，コマンドプロンプト等で `perl -v` を実行し，バージョン情報が表示されればOK．

```text
C:\Users\(user)> perl -V
Locale 'Japanese_Japan.932' is unsupported, and may crash the interpreter.
Summary of my perl5 (revision 5 version 38 subversion 2) configuration:
  Platform:
    osname=MSWin32
    osvers=10.0
    archname=MSWin32-x64-multi-thread
  [...]
  Compiler:
    cc='gcc'
    ccflags ='-s -O2 -DWIN32 -DWIN64 -D__USE_MINGW_ANSI_STDIO -DPERL_GCC_FUNC_VPRINTF -fno-strict-aliasing -fstack-protector-strong'
    optimize='-s -O2'
  [...]
```
---

## 3. latexindentの動作確認

以下のコマンドでバージョン情報を確認．

```sh
latexindent -V
```

```text
C:\Users\(user)>　latexindent -V
3.24.4, 2024-07-18
```

---

## 4. VSCodeの設定

VSCode側でフォーマッターを有効化し，自動整形などのエディタ連携を設定する．

1. `Ctrl + Shift + P` でコマンドパレットを開く．
2. 「`settings.json`」と入力し，「**Preferences: Open User Settings (JSON)**」を選択．
3. `settings.json`に下記設定を追記する．
4. 任意のフォーマットが崩れたTexファイルを開いて `Alt + Shift + F` で自動整形する．
5. 自動整形できてたら完成！

```json
{
    //他のsetting.jsonの設定

    "latex-workshop.formatting.latex": "latexindent",
    "latex-workshop.formatting.latexindent.path": "latexindent",
}
```

ファイル保存時に自動で整形したい場合は，以下を追加する．
```json
{
    "[latex]": {
        "editor.defaultFormatter": "James-Yu.latex-workshop",
        "editor.formatOnSave": true,
    },
    "[tex]": {
        "editor.defaultFormatter": "James-Yu.latex-workshop",
        "editor.formatOnSave": true,
    },

    "latex-workshop.formatting.latex": "latexindent",
    "latex-workshop.formatting.latexindent.path": "latexindent",
}
```

---

## 参考 (References)

この手順書，特に`settings.json`の作成にあたり，以下の素晴らしい記事を参考にさせていただきました．心より感謝申し上げます．

- [【自研究室向け】LaTeX+VSCode環境構築 2023年版) - Qiita](https://qiita.com/fuku_uma/items/e5ad46125a9612320273)
- [【大学生向け】LaTeX完全導入ガイド Windows編 (2022年) - Qiita](https://qiita.com/passive-radio/items/623c9a35e86b6666b89e)
- [VSCode で最高の LaTeX 環境を作る - Qiita](https://qiita.com/rainbartown/items/d7718f12d71e688f3573)
- [Windows環境での LaTeX in Vscode - HackMD](https://hackmd.io/@w0htNoPRRV2reDrTZHL5_w/BkM-zbj-B)

## 謝辞 (Acknowledgements)

本手順書の作成にあたり，内容のレビューにご協力いただいた [@38by](https://github.com/38by) さんに，心より感謝申し上げます．
