---
title: 単純なセグメント化フィルターの例
description: 単純なセグメント化フィルターの例
ms.assetid: 9c77fea4-61d9-4bec-8d8d-35436d00c1ed
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ada6abf55e6f324785bf7b85aa862a64015b1e5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373080"
---
# <a name="example-simple-segmentation-filter"></a>以下に例を示します。シンプル セグメンテーション フィルター





次のコード例では、単純なセグメント化フィルターを実装する方法を示します。 例では、セグメント化フィルターを使用しません、 [ **WIA\_IP\_DESKEW\_X** ](https://msdn.microsoft.com/library/windows/hardware/ff552581)と[ **WIA\_IP\_DESKEW\_Y** ](https://msdn.microsoft.com/library/windows/hardware/ff552587)プロパティ。 わかりやすくするために、エラー チェック コードが省略されています。

```cpp
typedef struct _SUB_RECT
{
    LONG  xpos;
    LONG  ypos;
    LONG  width;
    LONG  height;
} SUB_RECT;

STDMETHODIMP
SegFilter::DetectRegions(IN IStream  *pInputStream,
                         IN IWiaItem2  *pWiaItem2)
{
    HRESULT   hr = S_OK;
    SUB_RECT  pSubRegions = NULL;
    ULONG     cRegionsFound = 0;
    LONG      parent_xpos, parent_ypos;
    GUID      formatGUID = {0};

    LONG  lItemFlags = WiaItemTypeGenerated |
                       WiaItemTypeTransfer |
                       WiaItemTypeImage |
                       WiaItemTypeFile |
                       WiaItemTypeProgrammableDataSource;

    LONG  lCreationFlags = COPY_PARENTS_PROPERTY_VALUES;

    ReadPropertyGUID(pWiaItem2, WIA_IPA_FORMAT, &formatGUID);

    //
    // The algorithm that performs the actual region
    // detection has been omitted for clarity.
    //
    FindSubRegions(pInputStream,
                   formatGUID,
                   &pSubRegions,
                   &cRegionsFound);

    ReadPropertyLong(pWiaItem2, WIA_IPS_XPOS, &parent_xpos);
    ReadPropertyLong(pWiaItem2, WIA_IPS_YPOS, &parent_ypos);

    //
    // For each subimage that was found, create
    // a child item under pWiaItem2 into which
    // the coordinates for the subimage are set.
    //
    for (int i = 0; i < cRegionsFound; i++)
    {
        BSTR       bstrChildName = NULL;
        BSTR       bstrFullChildName = NULL;
        IWiaItem2  *pChildIWiaItem = NULL;

        GetNamesForChild(i,
                         &bstrChildName,
                         &bstrFullChildName);

        pWiaItem2->CreateChildItem(lItemFlags,
                                   lCreationFlags,
                                   bstrChildName,
                                   &pChildIWiaItem);

        WritePropertyLong(pChildWiaItem,
                          WIA_IPS_XPOS,
                          parent_xpos + pSubRegions[i].xpos);

        WritePropertyLong(pChildWiaItem,
                          WIA_IPS_YPOS,
                          parent_ypos + pSubRegions[i].ypos);

        WritePropertyLong(pChildWiaItem,
                          WIA_IPS_XEXTENT,
                          pSubRegions[i].width);

        WritePropertyLong(pChildWiaItem,
                          WIA_IPS_YEXTENT,
                          pSubRegions[i].height);

        pChildIWiaItem->Release();
        SysFreeString(bstrChildName);
        SysFreeString(bstrFullChildName);
    }

    if (pSubRegions)
    {
        free(pSubRegions);
    }

    return hr;
}
```

 

 




