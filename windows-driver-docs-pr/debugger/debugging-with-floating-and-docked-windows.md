---
title: フローティング ウィンドウとドッキング ウィンドウを使用したデバッグ
description: フローティング ウィンドウとドッキング ウィンドウを使用したデバッグ
ms.assetid: 2b3e67de-576e-4cbb-bdf1-58a31cea733c
keywords:
- デバッグのドッキング ウィンドウ
- デバッグのフローティング ウィンドウ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c10cec55e56e5e4bfbe3a68033813b11e86faa6d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580981"
---
# <a name="debugging-with-floating-and-docked-windows"></a>フローティング ウィンドウとドッキング ウィンドウを使用したデバッグ


## <span id="ddk_debugging_with_floating_and_docked_windows_dbg"></span><span id="DDK_DEBUGGING_WITH_FLOATING_AND_DOCKED_WINDOWS_DBG"></span>


デバッグ情報 ウィンドウで使用可能な機能をウィンドウがフローティングかどうかによって影響を受けるはいないドッキング、またはタブ付きのコレクションにドッキングはします。

### <a name="span-idoverviewofthewindowconfigurationspanspan-idoverviewofthewindowconfigurationspanoverview-of-the-window-configuration"></a><span id="overview_of_the_window_configuration"></span><span id="OVERVIEW_OF_THE_WINDOW_CONFIGURATION"></span>ウィンドウの構成の概要

フローティング ウィンドウは WinDbg ウィンドウまたはその他のどのドッキング ステーションに接続されていません。 フローティング ウィンドウは、常に、WinDbg ウィンドウの前に直接表示されます。

WinDbg ウィンドウ内または別のドッキング、ドッキング ウィンドウは固定位置を占有します。

2 つ以上のドッキング ウィンドウはタブの付いた、ときに、フレーム内の同じ位置を占有します。 同時にこれらのタブ付きウィンドウの 1 つだけ表示できます。 各タブ付きウィンドウの下部には、コレクションは、タブのセットです。 選択されているタブは、コレクション内のどのウィンドウが表示されてを示します。

### <a name="span-idmakingawindowactivespanspan-idmakingawindowactivespanmaking-a-window-active"></a><span id="making_a_window_active"></span><span id="MAKING_A_WINDOW_ACTIVE"></span>ウィンドウをアクティブにすること

位置に関係なく行うと、任意のウィンドウがアクティブで。 フローティング ウィンドウがアクティブな場合は、フォア グラウンドに表示されます。 追加のドッキング ステーション内にあるウィンドウがアクティブの場合、フォア グラウンドでそのドッキング ステーションが表示されます。 WinDbg ウィンドウ内でドッキング ウィンドウがアクティブである場合、1 つまたは複数のフローティング ウィンドウはドッキングされたウィンドウを隠すことがあります。

フローティング ウィンドウまたはドッキング ウィンドウをアクティブにするのには、そのタイトル バーをクリックします。 ドッキング ウィンドウのタブ付きのコレクションをアクティブにするのには、そのタブをクリックします。

WinDbg メニューまたはツールバーを使用して、ウィンドウをアクティブにすることができます。 下部のウィンドウの名前をクリックして任意のウィンドウをアクティブ化することができます、**ウィンドウ**メニュー。 任意のウィンドウをアクティブ化することも (以外の[[メモリ] ウィンドウ](memory-window.md)または[ソース ウィンドウ](source-window.md)) の名前をクリックして、**ビュー**メニューまたはツールバーのボタンをクリックします。

デバッグ情報のウィンドウ間を切り替えるには、CTRL + TAB キーを押します。 これらのキーを繰り返し押すと、かどうかは、フローティング、ドッキング自体、またはドッキング ウィンドウのタブ付きのコレクションの一部でに関係なく、windows のすべてをスキャンできます。 CTRL キーを離すと、現在表示しているウィンドウがアクティブになります。

ALT + TAB ショートカット キーは、標準の Microsoft Windows ショートカット キーを windows のデスクトップに切り替えます。 これらのショートカット キーを使用して、WinDbg ウィンドウと作成した追加のドッキングを切り替えることができます。 Windows タスク バー ボタンをクリックして dock をアクティブにすることができます。

 

 





