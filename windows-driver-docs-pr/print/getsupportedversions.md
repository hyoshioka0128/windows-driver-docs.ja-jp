---
title: GetSupportedVersions
description: IPrintTicketProvider GetSupportedVersions メソッドでは、印刷ドライバーがサポートする印刷スキーマのメジャー バージョン番号を返します。 ここでは、バージョン 1 は唯一のバージョンが存在するため、このメソッドは、1 つだけサポートされているバージョンを返す必要があります。
ms.assetid: 0b648cc3-4d61-401c-b626-34db2b026b2a
keywords:
- GetSupportedVersions
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 664d55ef7fb14295c7a2edca40a5aaa2af9fbee6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368992"
---
# <a name="getsupportedversions"></a>GetSupportedVersions


[ **IPrintTicketProvider::GetSupportedVersions** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554371(v=vs.85))メソッドは印刷ドライバーがサポートする印刷スキーマのメジャー バージョン番号を返します。 ここでは、バージョン 1 は唯一のバージョンが存在するため、このメソッドは、1 つだけサポートされているバージョンを返す必要があります。

次のサンプル コードに示すように実装は、最初のバージョンの Windows Vista、および新しいバージョンが追加されるまでに機能します。 新しいバージョンがサポートされている場合は、この値が変更されます。

```cpp
STDMETHODIMP 
CPrintTicketProvider::
GetSupportedVersions(THIS_ HANDLE hPrinter,
                           INT *ppVersions[],
                           INT *pcVersions)
{
    if ( (*ppVersions = (INT*)CoTaskMemAlloc(sizeof(INT))) != NULL)
    {
         (*ppVersions)[0] = 1;  // Version 1
        *pcVersions = 1; // 1 supported version
        return S_OK;
    }
    else
        return E_OUTOFMEMORY;
}
```

 

 




