---
title: WinDbg プレビュー-キーボードショートカット
description: ここでは、WinDbg preview デバッガーのキーボードショートカットについて説明します。
ms.date: 01/09/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7fc4e7cec30ea3d6ed032ccdc9f12a5ee991117b
ms.sourcegitcommit: 6d930ed810124ade8e29a617c7abcd399113696f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/17/2020
ms.locfileid: "76256748"
---
# <a name="windbg-preview-keyboard-shortcuts"></a>WinDbg Preview のキーボードショートカット

![WinDbg プレビューの小さなロゴ](images/windbgx-preview-logo.png)

このセクションでは、WinDbg preview デバッガーのキーボードショートカットについて説明します。

すべてのリボンメニューオプションは、 **Alt +** オプションの最初の文字を使用して使用できます。 たとえば、 **alt + h**を使用してホームメニューにアクセスするには、 **alt + h + S キーを押し**てデバッグを停止します。

![リボンのクイックキーに使用する文字を示す [ホーム] メニューのスクリーンショット](images/windbgx-ribbon-home-menu-alt-keys.png)

### <a name="flow-control"></a>フロー制御

| キー入力     | 説明             |
| ------------- |-------------------------|
 F5 | [続行]
F10     | ステップ オーバー
F11     | ステップ イン
Shift + F11   |   ステップ アウト
F7      | 行まで実行
Ctrl + Shift + I    |   強調表示された行に命令ポインターを設定する
Ctrl + Break または Alt + Del   |   休憩
Ctrl + Shift + F5   |   [再起動]
Shift + F5    |   デバッグの停止
Alt + H、D     | デタッチ

### <a name="setup"></a>[セットアップ]

| キー入力     | 説明             |
| ------------- |-------------------------|
F6      |   プロセスにアタッチ
Ctrl + R      |       リモートへの接続
Ctrl + D      |       ダンプファイルを開く
Ctrl + K      |       カーネルデバッガーにアタッチする
Ctrl + E      |       プロセスの起動
Ctrl + P      |       アプリパッケージの起動

### <a name="breakpoints"></a>ブレークポイント

| キー入力     | 説明             |
| ------------- |-------------------------|  
F9          |  強調表示された行にブレークポイントを切り替える
Ctrl + Alt + K      |   最初の区切りの切り替え
Alt + B、A         |  ブレークポイントの追加

### <a name="windowing"></a>ウィンドウ化

| キー入力     | 説明             |
| ------------- |-------------------------|
Ctrl + Tab        |       Window チェンジャーを開く
Ctrl+1      |       コマンドウィンドウを開く/フォーカスを移動する
Ctrl+2      |       [ウォッチ] ウィンドウで開く/フォーカスを移動する
Ctrl+3      |       [ローカル] ウィンドウで開く/フォーカスを移動する
Ctrl+4      |       [レジスタ] ウィンドウで開く/フォーカスを移動する
Ctrl + 5      |       [メモリ] ウィンドウを開く、またはフォーカスを移動する
Ctrl + 6      |       スタックウィンドウで開く/フォーカスを移動する
Ctrl + 数字 7      |       [逆アセンブル] ウィンドウを開く、またはフォーカスを移動する
Ctrl + 数字 8      |       [ブレークポイント] ウィンドウを開く、またはフォーカスを移動する
Ctrl + 数字 9      |       スレッドウィンドウで開く/フォーカスを移動する

### <a name="scripting"></a>スクリプト作成

| キー入力      | 説明             |
| -------------- |-------------------------|
Ctrl + Shift + O     |      スクリプトを開く
Ctrl + Shift + Enter |      スクリプトの実行
Ctrl + S           |      スクリプトの保存
Alt + S、N          |      新しいスクリプト
Alt + S、U          |      スクリプトのリンク解除

### <a name="stack-navigation"></a>スタックナビゲーション

| キー入力     | 説明             |
| ------------- |-------------------------|
Ctrl + ↑ / ↓      |   スタックフレームの上/下へ移動

### <a name="help"></a>[ヘルプ]

| キー入力     | 説明             |
| ------------- |-------------------------|
F1              |       ヘルプファイルを開く
Shift + F1        |       選択範囲をオンラインで検索 (ソースウィンドウ)

### <a name="misc"></a>その他。  

| キー入力     | 説明             |
| ------------- |-------------------------|
Ctrl+Alt+V      |       詳細モードの切り替え

## <a name="see-also"></a>関連項目

[WinDbg プレビューを使用したデバッグ](debugging-using-windbg-preview.md)
