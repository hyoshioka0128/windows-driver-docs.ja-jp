---
title: FsFilter コールバック ルーチンの登録
description: FsFilter コールバック ルーチンの登録
ms.assetid: d040e61c-514e-446b-9e72-934fd4322d3b
keywords:
- 登録 (コールバックルーチンを)
- コールバックルーチン WDK ファイルシステム
- FsFilter 通知コールバックルーチン WDK ファイルシステム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d2bb0491d0762e5e10983aea14e155d8d0fdc83
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841007"
---
# <a name="registering-fsfilter-callback-routines"></a>FsFilter コールバック ルーチンの登録


## <span id="ddk_registering_fsfilter_callback_routines_if"></span><span id="DDK_REGISTERING_FSFILTER_CALLBACK_ROUTINES_IF"></span>


FsFilter 通知コールバックルーチンは、基になるファイルシステムが特定の操作を実行する前と後に呼び出されます。 FsFilter のコールバックルーチンの詳細については、「 [**Fsrtlregisterfilesystemfiltercallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)」を参照してください。

FsFilter 通知コールバックルーチンを登録するには、FS\_フィルター\_コールバック構造体を割り当てて初期化し、FsFilter コールバックルーチンのエントリポイントを構造体に格納して、構造体のアドレスを**Fsrtlregisterfilesystemfiltercallbacks バック**への*コールバック*パラメーター。

たとえば、架空の "MyLegacyFilter" ドライバーは、次のように、その FsFilter コールバックルーチンを登録できます。

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

 

 




