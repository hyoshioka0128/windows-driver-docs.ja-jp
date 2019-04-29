---
title: コールバック オブジェクトの定義の例
description: コールバック オブジェクトの定義の例
ms.assetid: d987bb95-cbee-46aa-beaf-167572ca4a80
keywords:
- コールバック オブジェクト WDK UMDF、定義の例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1532967be27528fb7dd2454a7a47d16467fbacda
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330901"
---
# <a name="defining-callback-objects-example"></a>コールバック オブジェクトの定義の例


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

次のコード例は、ドライバーがから継承する方法を示しています、 [IPnpCallbackHardware](https://msdn.microsoft.com/library/windows/hardware/ff556764)デバイス コールバック オブジェクトを定義するインターフェイス。

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

 

 





