---
title: 状態更新コールバック関数の使用
description: 状態更新コールバック関数の使用
ms.assetid: fadd2edb-776b-4ef1-b663-cc004522f8ae
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4edba9ebd26408382aa9ab9deb46569e2c5044e4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388977"
---
# <a name="using-the-state-refresh-callback-functions"></a>状態更新コールバック関数の使用


ユーザー モードのディスプレイ ドライバーを使用して、 [Direct3D ランタイム バージョン 10 状態更新コールバック関数](https://msdn.microsoft.com/library/windows/hardware/ff552879)ステートレスのドライバーを実現するために、またはコマンド バッファー プリアンブル データが蓄積されます。

Direct3D のランタイムでは、その状態更新コールバック関数へのポインターを提供する、 [ **D3D10DDI\_CORELAYER\_DEVICECALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff541820)構造体、 **pUMCallbacks**のメンバー、 [ **D3D10DDIARG\_CREATEDEVICE** ](https://msdn.microsoft.com/library/windows/hardware/ff541664)への呼び出しで指す構造体、 [ **CreateDevice(D3D10)** ](https://msdn.microsoft.com/library/windows/hardware/ff540635)関数。

ユーザー モードのディスプレイ ドライバーが呼び出すには、たとえば、 [ **pfnStateIaIndexBufCb** ](https://msdn.microsoft.com/library/windows/hardware/ff568970)状態更新コールバック関数では、ドライバーがドライバーの呼び出しの内部では[ **IaSetIndexBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff567387)関数。 ユーザー モードのディスプレイ ドライバーが使用する場合がありますので、特に、この呼び出しは、決して、 **pfnStateIaIndexBufCb** 、プリアンブルおよびへの呼び出しを構築するコールバック関数*IaSetIndexBuffer*可能性がありますコマンド バッファーのサイズを使い果たしてしまうし、フラッシュが発生します。 このような場合は、呼び出しの**pfnStateIaIndexBufCb**元の呼び出しとして同じ「新しい」のバインド情報を渡す*IaSetIndexBuffer*します。 このような状況より最適な preamble で発生します。

 

 





