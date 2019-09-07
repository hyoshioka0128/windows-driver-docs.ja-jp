---
Description: プロパティの削除
title: プロパティの削除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9c98d137279b62ebdd8a212fe437495f5d08437
ms.sourcegitcommit: dff3834724bd5204c4a47204540fe8125dd37b20
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2019
ms.locfileid: "70750011"
---
# <a name="property-deletion"></a>プロパティの削除


Windows ポータブルデバイス (WPD) アプリケーションが**Iportabledeviceproperties::D e)** メソッドを呼び出すと、このメソッドはサンプルドライバーの**WpdObjectProperties:: OnDelete**メソッドの呼び出しをトリガーします。 サンプルドライバー内のどのオブジェクトプロパティも削除できないため、このメソッドは単純に E\_accessdenied を返します。

```ManagedCPlusPlus
HRESULT WpdObjectProperties::OnDeleteProperties(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{
    HRESULT hr = E_ACCESSDENIED;

    UNREFERENCED_PARAMETER(pParams);
    UNREFERENCED_PARAMETER(pResults);

    // This driver has no properties which can be deleted.

    return hr;
}
```

 

 




