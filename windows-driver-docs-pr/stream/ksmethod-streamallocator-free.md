---
title: KSMETHOD\_STREAMALLOCATOR\_FREE
description: KSMETHOD\_STREAMALLOCATOR\_無料メソッドは、特定のアロケーターにフレームを解放するため、クライアントによって使用されます。
ms.assetid: 90d42ae6-4aa2-46fd-b10c-7f07b77c86f1
keywords:
- KSMETHOD_STREAMALLOCATOR_FREE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSMETHOD_STREAMALLOCATOR_FREE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee5026b0a0193e7ed1918e7837083a562d5d567d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367594"
---
# <a name="ksmethodstreamallocatorfree"></a>KSMETHOD\_STREAMALLOCATOR\_FREE


**KSMETHOD\_STREAMALLOCATOR\_FREE**メソッドは、特定のアロケーターにフレームを解放するため、クライアントによって使用されます。 保留中の[ **KSMETHOD\_STREAMALLOCATOR\_アロケーション**](ksmethod-streamallocator-alloc.md)場合、このメソッドを使用して、完了することができます。

たとえば、カーネル モードのクライアントでは、フレームを解放するのに次のサンプル コードを使用できます。

<a name="remarks"></a>注釈
-------

```cpp
Method.Identifier.Set = KSMETHODSETID_StreamAllocator;
Method.Identifier.Id = KSMETHOD_STREAMALLOCATOR_FREE;
Method.Flags = KSMETHOD_TYPE_READ;
DeviceIoControl(
    AllocatorHandle,
    IOCTL_KS_METHOD,
    &amp;Method,
    sizeof(KSMETHOD),
    &amp;Frame,
    sizeof( PVOID ),
    &amp;BytesReturned,
    &amp;Overlapped);
```

 

 





