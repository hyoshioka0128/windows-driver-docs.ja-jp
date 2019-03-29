---
title: WinDbg Preview - ファイル メニュー
description: このセクションでは、WinDbg プレビュー デバッガーで、[ファイル] メニューを使用する方法について説明します。
ms.date: 08/04/2017
ms.localizationpriority: medium
ms.openlocfilehash: cba9d8ab2c98735dd78be50bfa78b07e3a979a82
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570574"
---
# <a name="windbg-preview---file-menu"></a>WinDbg Preview - ファイル メニュー 

このトピックで説明するファイル メニューを使用する方法。

### <a name="start-debugging"></a>デバッグを開始します。

最初に、[ファイル] メニューを開くとと、表示*デバッグを開始*と、最新のデバッガーの対象とします。 使用*デバッグを開始*新しい構成を以前のデバッガー セッションを開きます。

#### <a name="recent"></a>Recent

最近使用した一覧には、最近使ったワークスペースおよびデバッガー接続の一覧が含まれています。 作業の設定の詳細については、ワークスペースを参照してください[WinDbg Preview のセットアップ: 設定とワークスペース](windbg-setup-preview.md)します。

右クリック メニューを使用すると、ピン留め、名前変更および移動するように、ワークスペースを管理します。 メモ帳でそれらを編集します。

![ワークスペース ファイル ピン留めするメモ帳で開いている名前の変更の編集を表示 メニューを右クリックし、一覧から削除だけでなく固定解除されたターゲットをクリア](images/windbgx-workspace-right-click.png)

#### <a name="start-a-new-session"></a>新しいセッションを開始します。

他のタブを使用して、*デバッグを開始*アタッチするか、プロセスの起動など、新しいデバッガー セッションを開始するセクション。 新しいセッションの開始の詳細については、次を参照してください[WinDbg Preview - ユーザー モードのセッションを開始](windbg-user-mode-preview.md)と[WinDbg Preview - カーネル モードのセッションを開始。](windbg-kernel-mode-preview.md)


### <a name="save-workspace"></a>ワークスペースを保存します。

使用*ワークスペースを保存*を現在のワークスペースを保存します。

セッションの接続情報は、ワークスペースの構成ファイルに格納されます。 ワークスペースのファイルは、.debugTarget ファイルの拡張子で保存されます。 

ワークスペースのファイルの既定の場所を示します。 

```console
C:\Users\*UserName*\AppData\Local\DBG\targets
```

### <a name="open-source-file"></a>ソース ファイルを開く

使用*ソース ファイルを開く*ソース ファイルを開きます。 コードの実行により読み込まれていない追加のソース ファイルを操作するときに実行します。 ソース ファイルの操作方法の詳細については、次を参照してください[WinDbg では、ソース コードのデバッグ。](source-window.md)


### <a name="open-script"></a>スクリプトを開く

使用*スクリプトを開きます*を既存の Javascript または NatVis スクリプトを開きます。 スクリプトの操作の詳細については、次を参照してください。 [WinDbg Preview - Scripting メニュー](windbg-scripting-preview.md)します。

### <a name="settings"></a>設定

設定メニューを使用して、ソースとシンボルのパスを設定すると、デバッガーのライトと暗いテーマを選択します。 詳細については、設定を参照してください[WinDbg Preview のセットアップ: 設定とワークスペース](windbg-setup-preview.md)します。


### <a name="about"></a>バージョン情報
使用*について*デバッガーのビルド バージョン情報を表示します。 使用できますも使用してこの画面を Microsoft のプライバシーに関する声明を表示します。

---
 
## <a name="see-also"></a>関連項目

[WinDbg のプレビューを使用したデバッグ](debugging-using-windbg-preview.md)
 





