---
title: WinDbg プレビュー-[ファイル] メニュー
description: ここでは、WinDbg preview デバッガーの [ファイル] メニューを使用する方法について説明します。
ms.date: 01/10/2020
ms.localizationpriority: medium
ms.openlocfilehash: e5e4e33e13ea8de20f8b6fb04a0dbf3f7cb9c496
ms.sourcegitcommit: 6d930ed810124ade8e29a617c7abcd399113696f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/17/2020
ms.locfileid: "76256754"
---
# <a name="windbg-preview---file-menu"></a>WinDbg プレビュー-[ファイル] メニュー

![ビットパターンを使用した windbg プレビューの小さいロゴ](images/windbgx-preview-logo.png)

このトピックでは、[ファイル] メニューの使用方法について説明します。

### <a name="start-debugging"></a>デバッグを開始する

[ファイル] メニューを初めて開くと、[*デバッグの開始*] と [最近使ったデバッガーのターゲット] が表示されます。 [*デバッグ開始*] を使用して、以前のデバッガーセッションを新規に構成します。

#### <a name="recent"></a>Recent

[最近使ったもの] の一覧には、最近使用したワークスペースとデバッガーの接続の一覧が表示されます。 作業設定の詳細については、「 [WinDbg プレビュー設定–設定とワークスペース](windbg-setup-preview.md)」を参照してください。

右クリックメニューを使用して、固定、名前の変更、移動などのワークスペースを管理できます。 メモ帳で編集することもできます。

![ワークスペースファイルの右クリックメニューを開き、[メモ帳の pin で編集]、[リストから削除]、および [ピン留めされていないターゲット] をクリアします。](images/windbgx-workspace-right-click.png)

#### <a name="start-a-new-session"></a>新しいセッションを開始します。

プロセスのアタッチや起動など、新しいデバッガーセッションを開始するには、[*デバッグの開始*] セクションの他のタブを使用します。 新しいセッションを開始する方法の詳細については、「 [WinDbg preview-ユーザーモードセッションを開始する](windbg-user-mode-preview.md)」および「 [windbg プレビュー-カーネルモードセッションを開始する](windbg-kernel-mode-preview.md)」を参照してください。

### <a name="save-workspace"></a>ワークスペースの保存

現在のワークスペースを保存するには、[*ワークスペースの保存*] を使用します。

セッション接続情報は、ワークスペース構成ファイルに格納されます。 ワークスペースファイルは、debugTarget ファイル拡張子付きで格納されます。

ワークスペースファイルの既定の場所は次のとおりです。

```console
C:\Users\*UserName*\AppData\Local\DBG\targets
```

### <a name="open-source-file"></a>ソースファイルを開く

ソースファイルを開くには、*オープンソースファイル*を使用します。 これは、コードの実行によって読み込まれていない追加のソースファイルを操作する場合に使用します。 ソースファイルの操作の詳細については、「 [WinDbg でのソースコードのデバッグ](source-window.md)」を参照してください。

### <a name="open-script"></a>スクリプトを開く

既存の Javascript または NatVis スクリプトを開くには、 *[スクリプトを開く*] を使用します。 スクリプトの操作の詳細については[、「WinDbg プレビュー-スクリプトメニュー](windbg-scripting-preview.md)」を参照してください。

### <a name="settings"></a>設定

[設定] メニューを使用して、ソースとシンボルのパスを設定すると共に、デバッガーの明るいテーマとダークテーマを選択します。 設定の詳細については[、「WinDbg Preview Setup-settings and workspaces](windbg-setup-preview.md)」を参照してください。

### <a name="about"></a>[バージョン情報]

*について*は、デバッガーのビルドバージョン情報を表示するために使用します。 また、この画面を使用して、Microsoft のプライバシーに関する声明を表示することもできます。

### <a name="exit"></a>終了

デバッガーを終了するには、 *exit*を使用します。

---

## <a name="see-also"></a>関連項目

[WinDbg プレビューを使用したデバッグ](debugging-using-windbg-preview.md)
