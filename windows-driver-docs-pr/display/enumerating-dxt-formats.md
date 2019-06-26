---
title: DXT 形式の列挙
description: DXT 形式の列挙
ms.assetid: 77fc961f-1b94-43c1-b238-86f7d8e96835
keywords:
- 圧縮されたテクスチャ WDK DirectDraw を描画するには、フォーマット DXT を列挙します。
- DirectDraw は、DXT を列挙する、Windows 2000 の WDK の表示形式のテクスチャを圧縮します。
- 圧縮されたテクスチャ サーフェス WDK DirectDraw、DXT 形式を列挙します。
- WDK DirectDraw、圧縮されたテクスチャを表示します。
- 圧縮テクスチャ WDK DirectDraw、
- WDK DirectDraw DXT を列挙する書式設定します。
- DXT は、WDK DirectDraw を書式設定します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83468541367396667d95762aeed2e791beb30c60
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355549"
---
# <a name="enumerating-dxt-formats"></a>DXT 形式の列挙


## <span id="ddk_enumerating_dxt_formats_gg"></span><span id="DDK_ENUMERATING_DXT_FORMATS_GG"></span>


Microsoft directx では、ピクセル形式を列挙するために、ドライバーの 2 つの方法があります。 最初のメソッドは、テクスチャのために使用する形式を列挙します。 このメソッドは実装を使用して、 **lpTextureFormats**のメンバー、 [ **D3DHAL\_GLOBALDRIVERDATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_globaldriverdata)構造体。 2 番目のメソッドのいずれかの DDSCAPS 使用できる形式を列挙します\_オーバーレイ サーフェスまたは DDSCAPS\_OFFSCREENPLAIN サーフェス。 2 番目のメソッドを使用して、 **dwNumFourCCCodes**のメンバー、 [ **DDCORECAPS** ](https://docs.microsoft.com/windows/desktop/api/ddrawi/ns-ddrawi-_ddcorecaps)構造に含まれる、 [ **DD\_HALINFO** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo)構造と**lpdwFourCC** 、DD にも含まれている配列\_HALINFO 構造体。

DXT 形式は、主にテクスチャとして使用するとしているため、ドライバーは、最初のメソッドをのみ DXT 形式を列挙します。 DXT 形式を追加する必要はありません、 **lpdwFourCC**配列。

 

 





