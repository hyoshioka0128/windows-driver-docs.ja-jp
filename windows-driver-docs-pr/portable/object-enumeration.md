---
Description: オブジェクトの列挙
title: オブジェクトの列挙
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50cde952ffda2599aff596fc54510cadcd353d91
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362008"
---
# <a name="object-enumeration"></a>オブジェクトの列挙


*WpdObjectEnum.cpp*と*WpdObjectEnum.h*ファイルには、デバイスでサポートされているオブジェクトを列挙するメンバー関数が含まれます。

Windows ベースのアプリケーションを呼び出すときに**IPortableDeviceContent::EnumObject**または 2 つの方法の 1 つ、 **IEnumPortableDeviceObjectIDs**インターフェイスでは、この呼び出しをさらを 3 つのトリガーコマンド ハンドラーで、 **WpdObjectEnumerator**クラス。 次の表に、アプリケーション メソッドのマッピング**WpdObjectEnumerator**ドライバー メソッド。

|                                           |                                         |
|-------------------------------------------|-----------------------------------------|
| **IPortableDeviceContent メソッド**         | **WpdObjectEnumerator コマンド ハンドラー** |
| **IPortableDeviceContent::EnumObjects**   | **OnStartFind**                         |
| **IEnumPortableDeviceObjectIDs::Next**    | **OnFindNext**                          |
| **IEnumPortableDeviceObjectIDs::Release** | **OnEndFind**                           |

 

**WpdObjectEnumerator**によってコマンド ハンドラーが呼び出される、 **WpdObjectEnumerator::DispatchWpdMessage**メソッド。 次のサンプル ドライバーからの抜粋のコードを含む**WpdObjectEnumerator::DispatchWpdMessage します。**

```ManagedCPlusPlus
HRESULT WpdObjectEnumerator::DispatchWpdMessage(const PROPERTYKEY&     Command,
                                                IPortableDeviceValues* pParams,
                                                IPortableDeviceValues* pResults)
{
    HRESULT hr = S_OK;

    if (hr == S_OK)
    {
        if (Command.fmtid != WPD_CATEGORY_OBJECT_ENUMERATION)
        {
            hr = E_INVALIDARG;
            CHECK_HR(hr, "This object does not support this command category %ws",CComBSTR(Command.fmtid));
        }
    }

    if (hr == S_OK)
    {
        if (Command.pid == WPD_COMMAND_OBJECT_ENUMERATION_START_FIND.pid)
        {
            hr = OnStartFind(pParams, pResults);
            CHECK_HR(hr, "Failed to begin enumeration");
        }
        else if (Command.pid == WPD_COMMAND_OBJECT_ENUMERATION_FIND_NEXT.pid)
        {
            hr = OnFindNext(pParams, pResults);
            if(FAILED(hr))
            {
                CHECK_HR(hr, "Failed to find next object");
            }
        }
        else if (Command.pid == WPD_COMMAND_OBJECT_ENUMERATION_END_FIND.pid)
        {
            hr = OnEndFind(pParams, pResults);
            CHECK_HR(hr, "Failed to end enumeration");
        }
        else
        {
            hr = E_NOTIMPL;
            CHECK_HR(hr, "This object does not support this command id %d", Command.pid);
        }
    }

    return hr;
}
```

 

 




