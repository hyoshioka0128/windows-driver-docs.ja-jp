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
ms.openlocfilehash: c9bf6bc2c61adbd7ce141c31cfeb6f39436ee8f5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380762"
---
# <a name="enumerating-dxt-formats"></a>DXT 形式の列挙


## <span id="ddk_enumerating_dxt_formats_gg"></span><span id="DDK_ENUMERATING_DXT_FORMATS_GG"></span>


Microsoft directx では、ピクセル形式を列挙するために、ドライバーの 2 つの方法があります。 最初のメソッドは、テクスチャのために使用する形式を列挙します。 このメソッドは実装を使用して、 **lpTextureFormats**のメンバー、 [ **D3DHAL\_GLOBALDRIVERDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff545963)構造体。 2 番目のメソッドのいずれかの DDSCAPS 使用できる形式を列挙します\_オーバーレイ サーフェスまたは DDSCAPS\_OFFSCREENPLAIN サーフェス。 2 番目のメソッドを使用して、 **dwNumFourCCCodes**のメンバー、 [ **DDCORECAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549248)構造に含まれる、 [ **DD\_HALINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551627)構造と**lpdwFourCC** 、DD にも含まれている配列\_HALINFO 構造体。

DXT 形式は、主にテクスチャとして使用するとしているため、ドライバーは、最初のメソッドをのみ DXT 形式を列挙します。 DXT 形式を追加する必要はありません、 **lpdwFourCC**配列。

 

 





