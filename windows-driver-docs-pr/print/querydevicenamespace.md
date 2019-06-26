---
title: QueryDeviceNamespace
description: IPrintTicketProvider QueryDeviceNamespace ルーチンでは、印刷チケットで機能またはプライベートの名前空間からのオプションを配置する必要がある場合、PrintTicket の DEVMODE へと DEVMODE-PrintTicket に変換が使用する既定の名前空間を提供します。
ms.assetid: 5f940cdc-42c3-4521-91c5-cc8e340ce34a
keywords:
- QueryDeviceNamespace
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45f407a88c495370fb3d892030d4d89fd86b876a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384689"
---
# <a name="querydevicenamespace"></a>QueryDeviceNamespace


[ **IPrintTicketProvider::QueryDeviceNamespace** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554378(v=vs.85))ルーチンを配置する必要がある場合、PrintTicket の DEVMODE へと DEVMODE-PrintTicket への変換が使用する既定の名前空間を提供します、機能または印刷チケットでプライベート名前空間からのオプション。

次のサンプル コードは、このメソッドを実装する方法を示しています。

```cpp
STDMETHODIMP
CPrintTicketProvider::QueryDeviceNamespace(BSTR *pDefaultNamespace)
{
    *pDefaultNamespace = SysAllocString(TEXT("http://schemas.contoso.com/printers/seriesA/v.1.0"));
    
    if (!(*pDefaultNamespace))
    {
        return E_OUTOFMEMORY;
    }
 
    return S_OK;
}
```

 

 




