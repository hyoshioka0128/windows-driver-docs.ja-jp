---
title: コールバック インターフェイスの関連付けの例
description: コールバック インターフェイスの関連付けの例
ms.assetid: 6156730b-394c-451c-beea-1b25ba5a1fe3
keywords:
- コールバックオブジェクト WDK UMDF
- コールバックインターフェイス WDK UMDF
- コールバックインターフェイスの関連付け WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6bf28b0466225189fec2c07eac7560a6a92d486
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210046"
---
# <a name="associating-callback-interfaces-example"></a>コールバック インターフェイスの関連付けの例


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

ドライバーが[デバイスコールバックオブジェクトを作成](creating-callback-objects-example.md)するために使用する作成インスタンスメソッドを実装する方法を次のコード例に示します。 ドライバーは、コールバックコンテキストを割り当て、指定された**IUnknown**を1つ以上のコールバックインターフェイスに関連付けます。 このフレームワークは、後で**QueryInterface**を使用して、ドライバーでサポートされているコールバックインターフェイスを検出できます。

```cpp
static HRESULT CreateInstance(
                  IUnknown **ppUnknown, 
                  IWDFDeviceInitialize *pDeviceInit,
                  HANDLE CompletionPort 
                  ) {
   ...
   // Allocate the callback context
   CMyDevice *pMyDevice = new CMyDevice();
   ...
   HRESULT hr;
   // Discover the callback interface
   hr = pMyDevice->QueryInterface( 
                      __uuidof(IUnknown), 
                      (void **) ppUnknown
                      );
   ...
   return hr;
}
```

 

 





