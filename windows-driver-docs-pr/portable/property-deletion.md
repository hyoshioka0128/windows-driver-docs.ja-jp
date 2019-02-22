---
Description: Property Deletion
title: プロパティの削除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9c98d137279b62ebdd8a212fe437495f5d08437
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528264"
---
# <a name="property-deletion"></a>プロパティの削除


Windows ポータブル デバイス (WPD) アプリケーションを呼び出すと、 **IPortableDeviceProperties::Delete**メソッドでは、このメソッドは、さらへの呼び出しをトリガー、 **WpdObjectProperties::OnDelete**メソッドで、ドライバーのサンプルです。 このメソッドは単に返しますサンプル ドライバーでオブジェクトのプロパティの [なし] を削除するため、E\_ACCESSDENIED します。

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

 

 




