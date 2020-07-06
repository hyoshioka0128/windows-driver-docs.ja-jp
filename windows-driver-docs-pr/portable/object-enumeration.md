---
Description: オブジェクトの列挙
title: オブジェクトの列挙
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90b76e6bcb84752836934c6f5863c3d59c26e4e2
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968187"
---
# <a name="object-enumeration"></a>オブジェクトの列挙


*WpdObjectEnum*ファイルと*WpdObjectEnum*ファイルには、デバイスでサポートされているオブジェクトを列挙するメンバー関数が含まれています。

Windows ベースのアプリケーションが**Iportabledevicecontent:: EnumObject**呼び出すか、またはいずれかの 2 **IEnumPortableDeviceObjectIDs**つのメソッドが呼び出されると、この呼び出しによって**WpdObjectEnumerator**クラスの3つのコマンドハンドラーのいずれかがトリガーされます。 次の表は、 **WpdObjectEnumerator** driver メソッドへのアプリケーションメソッドのマッピングを示しています。

IPortableDeviceContent メソッド * * * *:**コマンドハンドラー**

IPortableDeviceContent:: * * * *: **Onstartfind**

IEnumPortableDeviceObjectIDs:: Next * * * *: **Onfindnext**

IEnumPortableDeviceObjectIDs:: Release * * * *: **OnEndFind**


 

**WpdObjectEnumerator**コマンドハンドラーは、 **WpdObjectEnumerator::D ispatchwpdmessage**メソッドによって呼び出されます。 サンプルドライバーの次の抜粋には、 **WpdObjectEnumerator::D ispatchwpdmessage**のコードが含まれています。

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

 

 




