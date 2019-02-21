---
title: WinDbg Preview - データ モデル
description: このセクションでは、WinDbg プレビュー デバッガーでのデータ モデル メニューを操作する方法について説明します。
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: d0e35ba5ffb7fa8bd170b1401e3e6b4a80987174
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560091"
---
# <a name="windbg-preview---data-model"></a>WinDbg Preview - データ モデル 

このセクションでは、データ モデル メニューのプレビューの WinDbg デバッガーで使用する方法について説明します。

![デバッガーでのデータ モデル メニューのスクリーン ショット](images/windbgx-data-model-menu.png)


## <a name="new-model-query"></a>新しいモデルのクエリ

新しいモデルのクエリを作成するのにには、新しいモデルのクエリ ダイアログを使用します。 何も配置することができますにする場合は、通常にここで`dx`コマンド。

たとえば、指定`Debugger.Sessions`デバッガー セッション オブジェクトを確認します。 

![新しいデータ モデルのクエリ ダイアログ ボックス](images/windbgx-data-model-new-model-dialog.png)

デバッガーの全般的な情報のオブジェクトを参照する[dx (表示デバッガー オブジェクト モデルの式)](dx--display-visualizer-variables-.md)します。

LINQ クエリを使用して、セッションをさらに掘り下げます。 このクエリは、ほとんどのスレッドを実行している上位 5 個のプロセスを示しています。 

```dbgcmd
Debugger.Sessions.First().Processes.Select(p => new { Name = p.Name, ThreadCount = p.Threads.Count() }).OrderByDescending(p => p.ThreadCount),5
```
![データ モデルの詳細 ウィンドウが表示されたプロセスとスレッド](images/windbgx-data-model-process-threads.png)


## <a name="data-model-explorer"></a>データ モデル エクスプ ローラー

内のすべてのデータ モデル オブジェクトを簡単に参照データのモデル エクスプ ローラーを使用して、`Debugger`名前空間。

![データ モデル エクスプ ローラー ウィンドウがデバッグ オブジェクトのセッションの表示](images/windbgx-data-model-explore-window.png)


## <a name="change-query"></a>クエリの変更

アクティブなデータ モデル ウィンドウで使用されるクエリを変更するのにには、クエリの変更を使用します。


## <a name="display-mode"></a>表示モード

グリッドと階層の表示モードを切り替える表示モードを使用します。 多くの列を表示または非表示に列ヘッダーを右クリックすることができます。

グリッド モードをオブジェクトを調べることができます。 たとえば、グリッド ビューでトップのスレッドの前のクエリをここでは。 

![データ モデルの詳細 ウィンドウが表示された最上位のスレッド](images/windbgx-data-model-process-threads-grid.png)

新しいタブが開かれた任意の下線付きの項目と、クエリをクリックすると、その情報を表示する実行されます。


このクエリでは、物理デバイス オブジェクトのドライバーの名前でグループ化されたプラグ アンド プレイ デバイス ツリーで、デバイスが表示されます。

```dbgcmd
Debugger.Sessions.First().Devices.DeviceTree.Flatten(n => n.Children).GroupBy(n => n.PhysicalDeviceObject->Driver->DriverName.ToDisplayString()) 
```
![データ モデルの詳細 ウィンドウのグリッド ビューでプラグ アンド プレイ デバイス ツリーを表示](images/windbgx-data-model-pnp-device.png)

---
 
## <a name="see-also"></a>参照

[dx (表示デバッガー オブジェクト モデルの式)](dx--display-visualizer-variables-.md)

[WinDbg のプレビューを使用したデバッグ](debugging-using-windbg-preview.md)
 

 





