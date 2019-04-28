---
title: 既定のセグメント化フィルターの例
description: 既定のセグメント化フィルターの例
ms.assetid: 96c74ca6-0162-4991-b3f9-86c17c92ffc3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eef65e94113e23644d31215a52f96f4d61e1e0f0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373086"
---
# <a name="example-default-segmentation-filter"></a>以下に例を示します。既定のセグメンテーション フィルター


ドライバーは、WIA を実装している限り、Microsoft のセグメント化フィルターを利用するには独自のセグメント化フィルターが不要\_IP\_セグメンテーション プロパティ。 別の方法としては、Microsoft には、特定の状況呼び出し中に既定 WIA セグメンテーションをフィルター処理する独自のセグメント化フィルターを提供する、IHV 用です。 たとえば、IHV は、フィルムをスキャン中の複数リージョンの検出に非常にデバイスに固有のセグメント化フィルターを適用して、ベッドからスキャン中に、Microsoft によって提供されるセグメント化フィルターを使用する場合。 これを行うには、IHV WIA のセグメント化フィルターのみ作成する必要が*CLSID\_WiaDefaultSegFilter*、実装する*IWiaSegmentationFilter;* 呼び出すセグメント化フィルター*DetectRegions*します。 次のコード例では、この実行方法を示します。

```cpp
STDMETHODIMP
SegFilter::DetectRegions(
   IN LONG       lFlags,
     IN IStream    *pInputStream,
     IN IWiaItem2  *pWiaItem2)
{
    HRESULT  hr                = S_OK;
    GUID     categoryGUID      = {0};
    BOOL     bUseDefaultFilter = FALSE;

    ...


    if (SUCCEEDED(hr))

    {
        ReadPropertyLong(pWiaItem2,
                         WIA_IPA_ITEM_CATEGORY,
                         &categoryGUID);
 
        if (categoryGUID == WIA_CATEGORY_FILM)
        {
            bUseDefaultFilter = FALSE;
        }
        else if (categoryGUID == WIA_CATEGORY_FLATBED)
        {
            bUseDefaultFilter = TRUE;
        }
        else
        {
            //
            // This scanner only comes with flatbed and film items.
            //
            hr = E_INVALIDARG;
        }
    }
 
    ...
 
    if (SUCCEEDED(hr) && bUseDefaultFilter)
    {
        //
        // This must be on the flatbed item - use the Microsoft Default WIA Segmentation Filter.
        //

        IWiaSegmentationFilter *pDefaultSegFilter = NULL;
 
        hr = CoCreateInstance(CLSID_WiaDefaultSegFilter,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IWiaSegmentationFilter,
                              reinterpret_cast<void **>(&pDefaultSegFilter));
        if (SUCCEEDED(hr))
        {
            hr = pDefaultSegFilter->DetectRegions(lFlags, pInputStream, pWiaItem2);
        }
 
        if (pDefaultSegFilter)
        {
            pDefaultSegFilter->Release();
            pDefaultSegFilter = NULL;
        }
    }
    else if (SUCCEEDED(hr))
    {
        //
        // This is on the film item - use the default WIA segmentation algorithm.
        //
        ...
    }
    ...
}
```

 

 




