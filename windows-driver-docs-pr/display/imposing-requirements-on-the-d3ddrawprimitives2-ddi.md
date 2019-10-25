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
ms.openlocfilehash: 0a08057c8222dfedf72068006d4b5b920ec583f3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840459"
---
# <a name="imposing-requirements-on-the-d3ddrawprimitives2-ddi"></a>D3dDrawPrimitives2 DDI に課される要件


## <span id="ddk_imposing_requirements_on_the_d3ddrawprimitives2_ddi_gg"></span><span id="DDK_IMPOSING_REQUIREMENTS_ON_THE_D3DDRAWPRIMITIVES2_DDI_GG"></span>


非同期クエリを処理する DirectX 9.0 バージョンドライバーの機能により、ドライバーの[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)関数に2つの新しい要件があります。 [非同期クエリの処理](handling-asynchronous-queries.md)に関するトピックで説明されているこれらの要件は、次の一覧にまとめられています。

-   ドライバーの*D3dDrawPrimitives2*関数は、ドライバーがより多くの応答を書き込むことができるように、ランタイムがそれを送信する可能性があるため、空のコマンドバッファーを処理できることを確認する必要があります。 ランタイムは、以前にドライバーが応答バッファーで D3DDP2OP\_の操作コードを返した場合、受信コマンドストリームで空のコマンドバッファーを送信します。

-   *D3dDrawPrimitives2*が成功した**場合 (** [**D3DHAL\_DRAWPRIMITIVES2DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data) structure が D3D\_OK) に設定されている場合、ドライバーは D3DHAL の**dwerroroffset**メンバーのみを設定する必要があり\_応答が使用可能な場合は、DRAWPRIMITIVES2DATA を0以外にします。 ドライバーがクエリに応答せず、 **ddrval**が D3D\_OK の場合は、 **dwerroroffset**を0に設定する必要があります。

 

 





