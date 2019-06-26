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
ms.openlocfilehash: 69a4c78f1f1cfd755c4204346e660fc3bc890c2e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385133"
---
# <a name="registering-fsfilter-callback-routines"></a>FsFilter コールバック ルーチンの登録


## <span id="ddk_registering_fsfilter_callback_routines_if"></span><span id="DDK_REGISTERING_FSFILTER_CALLBACK_ROUTINES_IF"></span>


FsFilter 通知コールバック ルーチンは、基になるファイル システムは、特定の操作を実行した後と前に呼び出されます。 FsFilter コールバック ルーチンの詳細については、次を参照してください。 [ **FsRtlRegisterFileSystemFilterCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)します。

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

 

 




