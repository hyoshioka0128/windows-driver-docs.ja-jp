---
title: WinDbg プレビュー-データモデルメニュー
description: このセクションでは、WinDbg preview デバッガーで [データモデル] メニューを使用する方法について説明します。
ms.date: 01/10/2020
ms.localizationpriority: medium
ms.openlocfilehash: 4b62daedbcfe0ad45a61211f2b2037009bfbaad7
ms.sourcegitcommit: 6d930ed810124ade8e29a617c7abcd399113696f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/17/2020
ms.locfileid: "76256756"
---
# <a name="windbg-preview---data-model-menu"></a>WinDbg プレビュー-データモデルメニュー

このセクションでは、WinDbg Preview デバッガーで [データモデル] メニューを使用する方法について説明します。

## <a name="new-model-query"></a>新しいモデルクエリ

[新しいモデルクエリ] ダイアログボックスを使用すると、新しいモデルクエリを作成できます。 通常の `dx` コマンドに入れることができます。

たとえば、`Debugger.Sessions` を指定して、デバッガーセッションオブジェクトを確認します。 

![[新しいデータモデルクエリ] ダイアログボックス](images/windbgx-data-model-new-model-dialog.png)

デバッガーオブジェクトに関する一般的な情報については、 [「dx (デバッガーオブジェクトモデル式の表示)](dx--display-visualizer-variables-.md)」を参照してください。

LINQ クエリを使用して、セッションをさらに掘り下げます。 このクエリは、最も多くのスレッドを実行している上位5つのプロセスを示します。 

```dbgcmd
Debugger.Sessions.First().Processes.Select(p => new { Name = p.Name, ThreadCount = p.Threads.Count() }).OrderByDescending(p => p.ThreadCount),5
```

![プロセスとスレッドを示すデータモデルの探索ウィンドウ](images/windbgx-data-model-process-threads.png)

## <a name="data-model-explorer"></a>データモデルエクスプローラー

データモデルエクスプローラーを使用すると、`Debugger` 名前空間内のすべてのデータモデルオブジェクトをすばやく参照できます。

![デバッグオブジェクトセッションを示すデータモデルエクスプローラーウィンドウ](images/windbgx-data-model-explore-window.png)

### <a name="display-mode"></a>表示モード

表示モードを使用すると、グリッドと階層表示モードを切り替えることができます。 列ヘッダーを右クリックすると、列の表示と非表示を切り替えることができます。

グリッドモードは、オブジェクトを掘り下げるのに役立ちます。 たとえば、次に示すのは、グリッドビューでの前の上位スレッドクエリです。 

![上位スレッドを示すデータモデルの探索ウィンドウ](images/windbgx-data-model-process-threads-grid.png)

下線付きの項目をクリックすると、新しいタブが開かれ、その情報を表示するためのクエリが実行されます。

このクエリは、プラグアンドプレイデバイスツリー内のデバイスを、カーネルセッションの物理デバイスオブジェクトのドライバーの名前でグループ化して表示します。

```dbgcmd
Debugger.Sessions.First().Devices.DeviceTree.Flatten(n => n.Children).GroupBy(n => n.PhysicalDeviceObject->Driver->DriverName.ToDisplayString()) 
```

![データモデルの [エクスプローラー] ウィンドウが表示された [プラグアンドプレイ] デバイスツリーが表示されます。](images/windbgx-data-model-pnp-device.png)

### <a name="change-query"></a>クエリの変更

[クエリの変更] を使用して、[アクティブなデータモデル] ウィンドウで使用されるクエリを変更します。

---

## <a name="see-also"></a>関連項目

[dx (表示デバッガーオブジェクトモデル式)](dx--display-visualizer-variables-.md)

[WinDbg プレビューを使用したデバッグ](debugging-using-windbg-preview.md)
