---
title: 例 DetectSubregions
description: 例 DetectSubregions
ms.assetid: 8fd5271a-587a-4b29-82a4-b84f70f5478f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05f11c9839bcf220de89b863794e555e34d6cfde
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373110"
---
# <a name="example-detectsubregions"></a>以下に例を示します。DetectSubregions





セグメント化、フィルター、ストリームで領域検出を実行します (*pImageStream*) に渡される、 **DetectSubregions**メソッド。 については、 **CreateSegmentationFilter**のこの例で使用されている関数を参照してください、 **IWiaItem2::GetExtension** Microsoft Windows SDK のドキュメント内のメソッド。

```cpp
HRESULT
DetectSubregions(
   IN IStream   *pImageStream,
   IN IWiaItem2 *pWiaItem2)
{
   HRESULT                 hr                  = S_OK;
   IWiaSegmentationFilter* pSegmentationFilter = NULL;

   if (!pWiaItem2 || !pImageStream)
   {
      hr = E_INVALIDARG;
   }

   if (SUCCEEDED(hr))
   {
      hr = CreateSegmentationFilter(pWiaItem2, &pSegmentationFilter);
   }

   if (SUCCEEDED(hr))
   {
      hr = pSegmentationFilter->DetectRegions(pImageStream, pWiaItem2); 
   }

   if (pSegmentationFilter)
   {
      pSegmentationFilter->Release();
      pSegmentationFilter = NULL;
   }

   return hr;
}
```

 

 




