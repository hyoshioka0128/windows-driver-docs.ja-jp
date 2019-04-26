---
title: WinDbg Preview - keyboard shortcuts
description: このセクションでは、WinDbg プレビュー デバッガーのキーボード ショートカットを提供します。
ms.date: 08/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ea41f3c3bf56bb02a6be0346199ce9786d0d0d6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353139"
---
# <a name="windbg-preview-keyboard-shortcuts"></a>WinDbg Preview keyboard shortcuts 

このセクションでは、WinDbg プレビュー デバッガーのキーボード ショートカットをまとめたものです。

使用して利用可能なすべてのリボン メニュー オプションは、 **Alt +** オプションの最初の文字。 たとえば**alt + h**ホームのメニューに移動する**Alt + H + P**ヘルプを表示します。

![リボンのクイック キーを使用して文字を示すホームのメニューのスクリーン ショット](images/windbgx-ribbon-home-menu-alt-keys.png)


### <a name="flow-control"></a>フロー制御

| キー入力     | 説明             |
| ------------- |-------------------------|
 F5 | 続行 
F10     | ステップ オーバー 
F11     | ステップ イン
Shift + F11   |   ステップ アウト
F7      | 行に実行します。
Ctrl + Shift + I    |   命令ポインターを強調表示された行に設定します。
Ctrl + Break または Alt + Del   |   休憩
Ctrl + Shift + F5   |   再起動
Shift + F5    |   デバッグを停止します。
Alt + H、D     | デタッチ



### <a name="setup"></a>セットアップ

| キー入力     | 説明             |
| ------------- |-------------------------|
F6      |   プロセスにアタッチ
Ctrl + R      |       リモート インスタンスに接続します。
Ctrl + D      |       開いているダンプ ファイル
Ctrl + K      |       カーネル デバッガーのアタッチ先
Ctrl + E      |       プロセスを起動します。
Ctrl + P      |       アプリ パッケージを起動します。

### <a name="breakpoints"></a>ブレークポイント         

| キー入力     | 説明             |
| ------------- |-------------------------|  
F9          |  強調表示された行のブレークポイントの切り替え
Ctrl + Alt + K      |   初期の中断の切り替え
Alt + B、A         |  ブレークポイントを追加します。

### <a name="windowing"></a>ウィンドウ化

| キー入力     | 説明             |
| ------------- |-------------------------|
Ctrl + Tab        |       チェンジャーのウィンドウを開く
Ctrl+1      |       コマンド ウィンドウで開く/フォーカス
Ctrl キーを押しながら 2      |       [ウォッチ] ウィンドウで開く/フォーカス
Ctrl + 3      |       [ローカル] ウィンドウで開く/フォーカス
Ctrl + 4      |       [レジスタ] ウィンドウで開く/フォーカス
Ctrl + 5      |       [メモリ] ウィンドウで開く/フォーカス
Ctrl キーを押しながら 6      |       履歴 ウィンドウで開く/フォーカス
Ctrl + 7      |       逆アセンブル ウィンドウで開く/フォーカス
Ctrl + 8      |       [ブレークポイント] ウィンドウで開く/フォーカス
Ctrl キーを押しながら 9      |       [スレッド] ウィンドウを開く/フォーカス


### <a name="scripting"></a>スクリプトの作成

| キー入力      | 説明             |
| -------------- |-------------------------|
Ctrl + Shift + O     |      スクリプトを開く
Ctrl + Shift + Enter |      スクリプトを実行します。
Ctrl + S           |      スクリプトを保存します。
Alt + S、N          |      新しいスクリプト
Alt + S、U          |      スクリプトのリンクを解除します。


### <a name="stack-navigation"></a>スタックのナビゲーション

| キー入力     | 説明             |
| ------------- |-------------------------|
Ctrl + ↑/↓      |   スタック フレームの上下を移動します。


### <a name="help"></a>Help 

| キー入力     | 説明             |
| ------------- |-------------------------|
F1              |       ヘルプ ファイルを開く
Shift + F1        |       オンライン選択 (ソース ウィンドウ) を検索します。


### <a name="misc"></a>その他  

| キー入力     | 説明             |
| ------------- |-------------------------|
Ctrl + Alt + V      |       詳細モードの切り替え




## <a name="see-also"></a>関連項目

[WinDbg のプレビューを使用したデバッグ](debugging-using-windbg-preview.md)






