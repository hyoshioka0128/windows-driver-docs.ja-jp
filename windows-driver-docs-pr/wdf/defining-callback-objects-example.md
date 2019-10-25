---
title: コールバック オブジェクトの定義の例
description: コールバック オブジェクトの定義の例
ms.assetid: d987bb95-cbee-46aa-beaf-167572ca4a80
keywords:
- コールバックオブジェクト WDK UMDF、定義の例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f7ae9ca5e71f09eedeebd6693e520a12bedc24e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841756"
---
# <a name="defining-callback-objects-example"></a>コールバック オブジェクトの定義の例


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

次のコード例は、デバイスのコールバックオブジェクトを定義するために、ドライバーが[IPnpCallbackHardware](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackhardware)インターフェイスから継承する方法を示しています。

```cpp
class CMyDevice :
       // Callback interface exposed to the framework
       public IPnpCallbackHardware 
{// The following data members make up the context
private:
   HANDLE                  m_CompletionPort;
   WINUSB_INTERFACE HANDLE m_UsbHandle;
   UCHAR                   m_BulkOutPipe;
   ULONG                   m_BulkOutMaxPacket;
   ...
// The following methods make up the callback interfaces
public:
    virtual HRESULT stdcall OnPrepareHardware( 
                              IWDFDevice* pDevice
                              );
    STDMETHOD( OnReleaseHardware )( IWDFDevice *pDevice );

   // Method used to create a device callback object
   static HRESULT CreateInstance( 
                     IUnknown **ppUnknown, 
                     IWDFDeviceInitialize *pDeviceInit,
                     HANDLE CompletionPort 
                     );
   ...
};
```

 

 





