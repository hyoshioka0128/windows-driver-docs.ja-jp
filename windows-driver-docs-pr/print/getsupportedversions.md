---
title: GetSupportedVersions
description: IPrintTicketProvider GetSupportedVersions メソッドでは、印刷ドライバーがサポートする印刷スキーマのメジャー バージョン番号を返します。 ここでは、バージョン 1 は唯一のバージョンが存在するため、このメソッドは、1 つだけサポートされているバージョンを返す必要があります。
ms.assetid: 0b648cc3-4d61-401c-b626-34db2b026b2a
keywords:
- GetSupportedVersions
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 789e8584590b7abaab5001e9279c1d47a535b6a9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385246"
---
# <a name="getsupportedversions"></a>GetSupportedVersions


[ **IPrintTicketProvider::GetSupportedVersions** ](https://msdn.microsoft.com/library/windows/hardware/ff554371)メソッドは印刷ドライバーがサポートする印刷スキーマのメジャー バージョン番号を返します。 ここでは、バージョン 1 は唯一のバージョンが存在するため、このメソッドは、1 つだけサポートされているバージョンを返す必要があります。

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

 

 




