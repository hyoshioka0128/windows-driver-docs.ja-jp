---
title: KSMETHOD\_STREAMALLOCATOR\_アロケーション
description: KSMETHOD\_STREAMALLOCATOR\_アロケーション メソッドは、特定のアロケーターからフレームの割り当て、クライアントによって使用されます。
ms.assetid: 4104d7df-1cc6-4109-9732-220b1065ee01
keywords:
- KSMETHOD_STREAMALLOCATOR_ALLOC ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSMETHOD_STREAMALLOCATOR_ALLOC
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d934271e7cc94352413fea381ce76e8d4878af3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367472"
---
# <a name="ksmethodstreamallocatoralloc"></a>KSMETHOD\_STREAMALLOCATOR\_アロケーション


**KSMETHOD\_STREAMALLOCATOR\_アロケーション**メソッドは、特定のアロケーターからフレームを割り当て、クライアントによって使用されます。 メソッドは状態を返します\_PENDING フレームが現在使用できない場合。 それ以外の場合、メソッドは、フレーム ポインターを返します。

など、カーネル モードのクライアントは割り当てフレームに次のサンプル コードを使用できます。

<a name="remarks"></a>注釈
-------

```cpp
Method.Identifier.Set = KSMETHODSETID_StreamAllocator;
Method.Identifier.Id = KSMETHOD_STREAMALLOCATOR_ALLOC;
Method.Flags = KSMETHOD_TYPE_WRITE;
DeviceIoControl(
    AllocatorHandle,
    IOCTL_KS_METHOD,
    &amp;Method,
    sizeof(KSMETHOD),
    &amp;Frame,
    sizeof(PVOID),
    &amp;BytesReturned,
    &amp;Overlapped);
```

 

 





