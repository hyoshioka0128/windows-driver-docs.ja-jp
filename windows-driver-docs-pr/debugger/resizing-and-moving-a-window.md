---
title: サイズ変更と、ウィンドウを移動します。
description: サイズ変更と、ウィンドウを移動します。
ms.assetid: 135e1ec1-9d58-45de-a0b4-5f962ed9e1f7
keywords:
- デバッグ情報のウィンドウ、サイズ変更、およびウィンドウを移動します。
- サイズ変更や windows の移動
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78ed01fb656b4c9550c91c9625955ff4278da7bb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529211"
---
# <a name="resizing-and-moving-a-window"></a>サイズ変更と、ウィンドウを移動します。


## <span id="ddk_resizing_and_moving_windows_dbg"></span><span id="DDK_RESIZING_AND_MOVING_WINDOWS_DBG"></span>


フローティング ウィンドウは、常に WinDbg ウィンドウに関連付けられます。 WinDbg を最小化する場合は、すべてのフローティング ウィンドウが最小化されます。 され WinDbg を復元する場合、すべてのフローティング ウィンドウが復元されます。 WinDbg のウィンドウの背後にフローティング ウィンドウを配置することができますしないでください。

フローティング ウィンドウで各しない個別に互いと移動 WinDbg ウィンドウで、選択した場合を除き、**フレームを使用して移動**ウィンドウのショートカット メニュー。

ドッキング ウィンドウは、WinDbg フレーム内で固定の位置を占有します。 WinDbg のサイズを変更する場合は、すべてドッキング ウィンドウの新しいサイズに自動的にスケールします。 同じ状況は、別のドッキング ステーションにドッキングされているが windows に適用されます。

2 つのドッキング ウィンドウの枠線をマウス ポインターを移動する場合、マウス ポインターが矢印になります。 この矢印をドラッグして、2 つの隣接するウィンドウのサイズを変更し、ドッキング状態のままにできます。

WinDbg のウィンドウには、ドッキング ウィンドウが常に格納されます。 ありません空の領域、ウィンドウにドッキングされている windows が存在する場合です。 同じ状況は、独立したドックに適用されます。

 

 





