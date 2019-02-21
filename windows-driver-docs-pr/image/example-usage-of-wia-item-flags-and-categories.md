---
title: WIA 項目のフラグとカテゴリの使用例
description: WIA 項目のフラグとカテゴリの使用例
ms.assetid: 8c9f7d85-6c84-4df9-9db3-6554d7eddf93
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9ca6a4825773e4be9998ee3cef7554b6f012207
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537397"
---
# <a name="example-usage-of-wia-item-flags-and-categories"></a>WIA 項目のフラグとカテゴリの使用例





このトピックには、Windows Vista 以降が適用されます。

このセクションでは、スキャナー、WIA 項目のフラグ、WIA カテゴリと、Windows Vista でのカメラ項目のツリーを示しています。 カメラの項目のツリーおよびスキャナー項目のツリーはどのように Windows vista およびそれ以降、図を示しています。 カメラの項目のツリーとスキャナーの項目のツリーの両方の 2 つの図があります。 どちらの場合は、最初の図は、WIA 項目フラグが必要なは、2 番目の図は、WIA カテゴリが使用されるを示しています。 中に示しています。 コード例は、フラグとカテゴリの組み合わせを使用する操作は、アプリケーションの例です。

次の図は、WIA でカメラの項目のツリーとフラグを示します\_項目\_フラグ プロパティを設定する必要があります。

![wia 項目のフラグでカメラのツリーを示す図](images/art-film-tree1.png)

上記の図では、左側のツリーは、カメラの項目のツリーを表します。 右側の吹き出しには、このようなデバイスを使用する必要があります WIA 項目のフラグが含まれます。

次の図では、WIA でカメラの項目のツリーとカテゴリは\_IPA\_項目\_CATEGORY プロパティを設定する必要があります。

![カメラをツリー、カテゴリの表示を示す図](images/art-film-tree2.png)

上記の図では、左側のツリーは、カメラの項目のツリーを表します。 右側のバルーンには、このようなデバイスを使用して、必要となるカテゴリが含まれています。

次の図では、ドキュメント フィーダーの付いたスキャナーとフィルム スキャナーとフラグの項目のツリーは、WIA で\_項目\_フラグ プロパティを設定する必要があります。

![ドキュメント フィーダーの付いたスキャナーとフィルム スキャナー、wia 項目のフラグの項目のツリーを示す図](images/art-flatbed-tree1.png)

上記の図では、左側のツリーは、スキャナーの項目のツリーを表します。 右側の吹き出しには、このようなデバイスを使用する必要があります WIA 項目のフラグが含まれます。

次の図は、スキャナーとカテゴリの項目のツリーを示しています、WIA で\_IPA\_項目\_CATEGORY プロパティを設定する必要があります。

![スキャナー、および設定する必要があるカテゴリの項目のツリーを示す図](images/art-flatbed-tree2.png)

上記の図では、左側のツリーは、スキャナーの項目のツリーを表します。 右側の吹き出しは、WIA 内のカテゴリを含む\_IPA\_項目\_CATEGORY プロパティをこのようなデバイスを設定する必要があります。

WIA とカテゴリごとの有効な WIA 項目フラグについては、定義されたすべてのカテゴリの完全な一覧を参照してください。 [ **WIA\_IPA\_項目\_カテゴリ**](https://msdn.microsoft.com/library/windows/hardware/ff551581)します。

WIA がすべての完全なリスト項目のフラグを参照してください[ **WIA\_IPA\_項目\_フラグ**](https://msdn.microsoft.com/library/windows/hardware/ff551585)します。

次のコード例は、アプリケーションが、WIA の組み合わせを使用する方法を示します\_IPA\_項目\_フラグと WIA\_IPA\_項目\_を分類するカテゴリのプロパティWIA 項目のツリー内で見つかった項目 WIA します。

```cpp
HRESULT hr = S_OK;
PROPSPEC ps[2] = {{PRSPEC_PROPID,WIA_IPA_ITEM_FLAGS},
                  {PRSPEC_PROPID, WIA_IPA_ITEM_CATEGORY}};
PROPVARIANT pv[2] = {0};

hr = pIWiaPropertyStorage->ReadMultiple(2, ps, pv);
if (hr == S_OK)
{
    if (pv[0].lVal & WiaItemTypeProgrammableDataSource)
    {
        // Item is a programmable data source.
    }
    else
    {
        // Item is NOT a programmable data source and there must be
        // some data associated with the device, or a folder.
        // Use the WIA item flags to further classify the item.

        if (pv[0].lVal & WiaItemTypeImage)
        {
            // Item represents image data.
        }
        if (pv[0].lVal & WiaItemTypeAudio)
        {
            // Item represents audio data.
        }
        if (pv[0].lVal & WiaItemTypeVideo)
        {
            // Item represents video data.
        }
        if (pv[0].lVal & WiaItemTypeDocument)
        {
            // Item represents document data.
        }
    }

    // Read the category to properly use the item.
    switch(pv[1].lVal)
    {
        case WIA_CATEGORY_FINISHED_FILE:
            // Item is a finished file item.
  break;
        case WIA_CATEGORY_FLATBED:
            // Item is a flatbed scanner item.
   break;
        case WIA_CATEGORY_FILM:
            // Item is a film scanning item.
  break;
        case WIA_CATEGORY_FEEDER:
            // Item is a document feeder scanner item.
   break;
        default:
            // Item is not a WIA-defined item (possibly vendor specific?).
   break;
    }
    ...
}
...
```

 

 




