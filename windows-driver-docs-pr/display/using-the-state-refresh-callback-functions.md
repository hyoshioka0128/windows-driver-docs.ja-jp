---
title: 状態更新コールバック関数の使用
description: 状態更新コールバック関数の使用
ms.assetid: fadd2edb-776b-4ef1-b663-cc004522f8ae
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 328ec8fafc9fe67614c644e1e045f2bea263e3f1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377372"
---
# <a name="using-the-state-refresh-callback-functions"></a>状態更新コールバック関数の使用


ユーザー モードのディスプレイ ドライバーを使用して、 [Direct3D ランタイム バージョン 10 状態更新コールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)ステートレスのドライバーを実現するために、またはコマンド バッファー プリアンブル データが蓄積されます。

Direct3D のランタイムでは、その状態更新コールバック関数へのポインターを提供する、 [ **D3D10DDI\_CORELAYER\_DEVICECALLBACKS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddi_corelayer_devicecallbacks)構造体、 **pUMCallbacks**のメンバー、 [ **D3D10DDIARG\_CREATEDEVICE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)への呼び出しで指す構造体、 [ **CreateDevice(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)関数。

ユーザー モードのディスプレイ ドライバーが呼び出すには、たとえば、 [ **pfnStateIaIndexBufCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_state_ia_indexbuf_cb)状態更新コールバック関数では、ドライバーがドライバーの呼び出しの内部では[ **IaSetIndexBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_ia_setindexbuffer)関数。 ユーザー モードのディスプレイ ドライバーが使用する場合がありますので、特に、この呼び出しは、決して、 **pfnStateIaIndexBufCb** 、プリアンブルおよびへの呼び出しを構築するコールバック関数*IaSetIndexBuffer*可能性がありますコマンド バッファーのサイズを使い果たしてしまうし、フラッシュが発生します。 このような場合は、呼び出しの**pfnStateIaIndexBufCb**元の呼び出しとして同じ「新しい」のバインド情報を渡す*IaSetIndexBuffer*します。 このような状況より最適な preamble で発生します。

 

 





