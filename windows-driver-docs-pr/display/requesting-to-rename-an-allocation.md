---
title: 割り当ての名前を変更する要求
description: 割り当ての名前を変更する要求
ms.assetid: f22e19ba-9ff3-4aa1-a3f0-103f67ea7c60
keywords:
- コマンド バッファー WDK の表示、割り当ての名前を変更
- DMA バッファー WDK の表示、割り当ての名前を変更
- WDK の表示名の変更の割り当て
- WDK の表示の割り当ての名前を変更します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b45871e26a8ef09fe90dd3eb2ffd3441cbb68952
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376605"
---
# <a name="requesting-to-rename-an-allocation"></a>割り当ての名前を変更する要求


ユーザー モードのディスプレイ ドライバーは、ビデオ メモリ マネージャーがアプリケーションを示します (たとえば、頂点バッファー) 画面をロックする要求の一部として、画面の内容を破棄するとき、画面に関連付けられた割り当てを変更することを要求する必要があります。 マイクロソフトの Direct3D ランタイム渡します、**破棄**画面の現在のコンテンツを必要がなくなったことを示すフラグをビット フィールド。 ドライバーは、ビデオ メモリ マネージャーがアイドル状態になった現在の割り当てまで、アプリケーション スレッドを停止するのではなく、画面のコンテンツを保持している現在の割り当てがビジー状態で場合は、ロック要求を処理するために、新しい割り当てを割り当てることを要求できます。

ユーザー モードのディスプレイ ドライバーは、ビデオ メモリ マネージャーでは、ドライバーを設定すると、割り当てが名前を変更ことを要求、**破棄**のメンバー、 [ **D3DDDICB\_LOCKFLAGS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddicb_lockflags)構造体への呼び出しで、 [ **pfnLockCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_lockcb)関数。 ビデオ メモリ マネージャーは、割り当ての名前を変更する必要がありますがかどうか、または割り当ては現在ビジー状態かどうかと、現在のメモリ条件に基づいてアプリケーションを割り当てがアイドル状態になるまでの遅延が発生することを決定します。 名前が変更される各の割り当てには、ビデオ メモリ マネージャーは、連続して割り当てのロックに使用される割り当ての一覧を保持します。 ビデオ メモリ マネージャーでは、アプリケーションは、割り当ての内容を破棄するたびに、リストを循環します。 リストの長さは、アプリケーションの要件とメモリの負荷によって決まります。 ビデオ メモリ マネージャーが、リストを保持しようとしています。 ロック要求をアプリケーション スレッドの停止を回避するのに十分な長さ。 ただし、メモリの負荷の下で、ビデオ メモリ マネージャーは、余分なメモリ不足を回避するためにリストをトリミングできます。

ドライバーの設定の割り当ての名前の変更のリストの長さに制限を強制する、 **MaximumRenamingListLength**のメンバー、 [ **DXGK\_ALLOCATIONINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo)割り当ての作成時に構造体します。 ドライバーが設定されている場合**MaximumRenamingListLength** 0 以外の値にし、ビデオ メモリ マネージャー長さを決定します適切な名前の変更の一覧のドライバーによって課される制限を超えることがなく。 ドライバーが設定されている場合**MaximumRenamingListLength**を 0 にし、メモリ マネージャーは、サイズを増やし、パフォーマンスを向上させるために必要なサイズに名前変更一覧の。

ユーザー モードのディスプレイ ドライバーの設定と、**破棄**のメンバー [ **D3DDDICB\_LOCKFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddicb_lockflags)、ビデオ メモリ マネージャーには、表示は呼び出しません。元の割り当ての追加の割り当ての割り当てにミニポート ドライバー。 ビデオ メモリ マネージャーは、元の割り当ての作成パラメーターを使用してすべての余分な割り当てを作成します。 ディスプレイのミニポート ドライバーの観点からは、同じ割り当ては可能性のある複数の同時セグメント位置でページングが。

 

 





