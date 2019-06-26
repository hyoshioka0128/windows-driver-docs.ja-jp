---
title: D3dDrawPrimitives2 DDI に課される要件
description: D3dDrawPrimitives2 DDI に課される要件
ms.assetid: a016c127-14ad-42ba-aae5-97c6c97b01f6
keywords:
- 非同期クエリ操作 WDK DirectX 9.0、D3dDrawPrimitives2
- クエリ操作 WDK DirectX 9.0、D3dDrawPrimitives2
- D3dDrawPrimitives2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2360ec25c89bb3324d5fe0bfc47d3821d9dacd80
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383931"
---
# <a name="imposing-requirements-on-the-d3ddrawprimitives2-ddi"></a>D3dDrawPrimitives2 DDI に課される要件


## <span id="ddk_imposing_requirements_on_the_d3ddrawprimitives2_ddi_gg"></span><span id="DDK_IMPOSING_REQUIREMENTS_ON_THE_D3DDRAWPRIMITIVES2_DDI_GG"></span>


非同期クエリを処理する DirectX 9.0 バージョンのドライバーの機能は、ドライバーに 2 つの新しい要件を課す[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)関数。 これらの要件に記載されて、[非同期クエリの処理](handling-asynchronous-queries.md)トピックでは、次の一覧にまとめます。

-   ドライバーの*D3dDrawPrimitives2*関数は、ランタイム可能性がありますに送信できるように、ドライバーは複数の応答を書き込むことができますので、空のコマンド バッファーを処理できるようにする必要があります。 ドライバーは、D3DDP2OP 以前返された場合、ランタイムがコマンドの受信ストリームのバッファーを空のコマンドを送信する\_応答バッファーに RESPONSECONTINUE 操作コード。

-   成功した場合の*D3dDrawPrimitives2* (**ddrval**の[ **D3DHAL\_DRAWPRIMITIVES2DATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data) D3D に設定\_OK)、ドライバー保証するためだけを設定する必要があります、 **dwErrorOffset** D3DHAL のメンバー\_DRAWPRIMITIVES2DATA 応答が使用可能な場合に 0 以外の値。 ドライバーがすべてのクエリに応答しない場合と**ddrval**は D3D\_OK、 **dwErrorOffset**を 0 に設定する必要があります。

 

 





