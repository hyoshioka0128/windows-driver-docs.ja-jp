---
title: FsFilter コールバック ルーチンの登録
description: FsFilter コールバック ルーチンの登録
ms.assetid: d040e61c-514e-446b-9e72-934fd4322d3b
keywords:
- コールバック ルーチンを登録します。
- コールバック ルーチン WDK ファイル システム
- FsFilter 通知コールバック ルーチン WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc978daf2a07eea91ea8eb5aff16f1b5a810a2eb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370118"
---
# <a name="registering-fsfilter-callback-routines"></a>FsFilter コールバック ルーチンの登録


## <span id="ddk_registering_fsfilter_callback_routines_if"></span><span id="DDK_REGISTERING_FSFILTER_CALLBACK_ROUTINES_IF"></span>


FsFilter 通知コールバック ルーチンは、基になるファイル システムは、特定の操作を実行した後と前に呼び出されます。 FsFilter コールバック ルーチンの詳細については、次を参照してください。 [ **FsRtlRegisterFileSystemFilterCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff547172)します。

FsFilter 通知のコールバック ルーチンを登録するには必要がありますを割り当てるし、初期化、FS\_フィルター\_コールバックは、構造体、構造体で FsFilter コールバック ルーチンのエントリ ポイントを保存してのアドレスを渡す、構造体、*コールバック*パラメーターを**FsRtlRegisterFileSystemFilterCallbacks**します。

たとえば、仮想的な"MyLegacyFilter"ドライバーはその FsFilter コールバック ルーチンをよう登録できます。

```cpp
fsFilterCallbacks.SizeOfFsFilterCallbacks = sizeof(FS_FILTER_CALLBACKS);
fsFilterCallbacks.PreAcquireForSectionSynchronization = MyLegacyFilterPreFsFilterOperation;
fsFilterCallbacks.PostAcquireForSectionSynchronization = MyLegacyFilterPostFsFilterOperation;
fsFilterCallbacks.PreReleaseForSectionSynchronization = MyLegacyFilterPreFsFilterOperation;
fsFilterCallbacks.PostReleaseForSectionSynchronization = MyLegacyFilterPostFsFilterOperation;
fsFilterCallbacks.PreAcquireForCcFlush = MyLegacyFilterPreFsFilterOperation;
fsFilterCallbacks.PostAcquireForCcFlush = MyLegacyFilterPostFsFilterOperation;
fsFilterCallbacks.PreReleaseForCcFlush = MyLegacyFilterPreFsFilterOperation;
fsFilterCallbacks.PostReleaseForCcFlush = MyLegacyFilterPostFsFilterOperation;
fsFilterCallbacks.PreAcquireForModifiedPageWriter = MyLegacyFilterPreFsFilterOperation;
fsFilterCallbacks.PostAcquireForModifiedPageWriter = MyLegacyFilterPostFsFilterOperation;
fsFilterCallbacks.PreReleaseForModifiedPageWriter = MyLegacyFilterPreFsFilterOperation;
fsFilterCallbacks.PostReleaseForModifiedPageWriter = MyLegacyFilterPostFsFilterOperation;

status = FsRtlRegisterFileSystemFilterCallbacks(DriverObject, &fsFilterCallbacks);
```

 

 




