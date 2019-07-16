---
title: コールバック インターフェイスの関連付けの例
description: コールバック インターフェイスの関連付けの例
ms.assetid: 6156730b-394c-451c-beea-1b25ba5a1fe3
keywords:
- コールバック オブジェクト WDK UMDF
- コールバック インターフェイス WDK UMDF
- コールバックを関連付けるインターフェイスを WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f4be15bd42f67d4256b3917a9e1fabe33f5ed5a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68229675"
---
# <a name="associating-callback-interfaces-example"></a>コールバック インターフェイスの関連付けの例


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

次のコード例は、ドライバー、ドライバーを使用しているインスタンスの作成メソッドを実装する方法を示しています。[デバイス コールバック オブジェクトを作成](creating-callback-objects-example.md)です。 ドライバーがコールバック コンテキストを割り当て、および関連付ける、指定された**IUnknown** 1 つまたは複数のコールバック インターフェイスを使用します。 フレームワークを使用できます**QueryInterface**ドライバーによってサポートされているコールバック インターフェイスを検出します。

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

 

 





