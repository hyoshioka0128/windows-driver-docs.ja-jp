---
title: QueryDeviceNamespace
description: IPrintTicketProvider QueryDeviceNamespace ルーチンでは、印刷チケットで機能またはプライベートの名前空間からのオプションを配置する必要がある場合、PrintTicket の DEVMODE へと DEVMODE-PrintTicket に変換が使用する既定の名前空間を提供します。
ms.assetid: 5f940cdc-42c3-4521-91c5-cc8e340ce34a
keywords:
- QueryDeviceNamespace
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bb3fb6db8507c4896c7ef1ce78a6df090cc73bf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372424"
---
# <a name="querydevicenamespace"></a>QueryDeviceNamespace


[ **IPrintTicketProvider::QueryDeviceNamespace** ](https://msdn.microsoft.com/library/windows/hardware/ff554378)ルーチンを配置する必要がある場合、PrintTicket の DEVMODE へと DEVMODE-PrintTicket への変換が使用する既定の名前空間を提供します、機能または印刷チケットでプライベート名前空間からのオプション。

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

 

 




