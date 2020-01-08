---
title: QueryDeviceNamespace
description: IPrintTicketProvider QueryDeviceNamespace ルーチンには、印刷チケットのプライベート名前空間から機能またはオプションを設定する必要がある場合に、PrintTicket から DEVMODE への変換と DEVMODE から PrintTicket への変換で使用される既定の名前空間が用意されています。
ms.assetid: 5f940cdc-42c3-4521-91c5-cc8e340ce34a
keywords:
- QueryDeviceNamespace
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27c2a49de895530c78ff7cb7cf42109d2944a036
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652849"
---
# <a name="querydevicenamespace"></a>QueryDeviceNamespace


[**IPrintTicketProvider:: QueryDeviceNamespace**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554378(v=vs.85))ルーチンは、出力チケットのプライベート名前空間から機能またはオプションを配置する必要がある場合に、PRINTTICKET から devmode への変換と Devmode から printticket への変換で使用される既定の名前空間を提供します。

次のサンプルコードは、このメソッドを実装する方法を示しています。

```cpp
STDMETHODIMP
CPrintTicketProvider::QueryDeviceNamespace(BSTR *pDefaultNamespace)
{
    *pDefaultNamespace = SysAllocString(TEXT("https://schemas.contoso.com/printers/seriesA/v.1.0"));
    
    if (!(*pDefaultNamespace))
    {
        return E_OUTOFMEMORY;
    }
 
    return S_OK;
}
```

 

 




