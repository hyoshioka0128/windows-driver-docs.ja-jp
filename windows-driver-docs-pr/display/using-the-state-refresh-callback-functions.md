---
title: 状態更新コールバック関数の使用
description: 状態更新コールバック関数の使用
ms.assetid: fadd2edb-776b-4ef1-b663-cc004522f8ae
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e88c4be26f1108e8e841a1c92b2a63ff6db5e3b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825366"
---
# <a name="using-the-state-refresh-callback-functions"></a>状態更新コールバック関数の使用


ユーザーモードの表示ドライバーでは、 [Direct3D ランタイムバージョン10の状態更新コールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を使用して、ステートレスドライバーを実現したり、コマンドバッファーのプリアンブルデータを作成したりできます。

Direct3D ランタイムは、 [**D3D10DDI\_CORELAYER\_DEVICECALLBACKS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddi_corelayer_devicecallbacks)構造内の状態更新コールバック関数へのポインターを提供します。この構造体は、D3D10DDIARG の**pUMCallbacks**メンバーによって[ **\_CREATEDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)構造体は、 [**CreateDevice (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)関数の呼び出しでを指します。

ユーザーモードの表示ドライバーは、たとえば、 [**PfnstateiIaSetIndexBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_state_ia_indexbuf_cb)の状態更新コールバック関数を呼び出しますが、ドライバーはドライバーの[](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_ia_setindexbuffer)関数の呼び出し内にあります。 この呼び出しは、特にユーザーモードの表示ドライバーが**Pfnstateiaindexbufcb**コールバック関数を使用してプリアンブルを作成し、 *IaSetIndexBuffer*を呼び出すとコマンドバッファーのサイズが枯渇し、揃える. このような状況では、 **Pfnstateiaindexbufcb**を呼び出すと、 *IaSetIndexBuffer*への元の呼び出しと同じ "新しい" バインド情報が渡されます。 このような状況では、より最適化されたプリアンブルが生成されます。

 

 





