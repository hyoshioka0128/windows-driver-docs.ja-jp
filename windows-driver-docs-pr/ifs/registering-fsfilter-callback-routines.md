---
title: FsFilter コールバック ルーチンを登録します。
description: FsFilter コールバック ルーチンを登録します。
ms.assetid: d040e61c-514e-446b-9e72-934fd4322d3b
keywords:
- コールバック ルーチンを登録します。
- コールバック ルーチン WDK ファイル システム
- FsFilter 通知コールバック ルーチン WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc978daf2a07eea91ea8eb5aff16f1b5a810a2eb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551503"
---
# <a name="registering-fsfilter-callback-routines"></a>FsFilter コールバック ルーチンを登録します。


## <span id="ddk_registering_fsfilter_callback_routines_if"></span><span id="DDK_REGISTERING_FSFILTER_CALLBACK_ROUTINES_IF"></span>


FsFilter 通知コールバック ルーチンは、基になるファイル システムは、特定の操作を実行した後と前に呼び出されます。 FsFilter コールバック ルーチンの詳細については、[ **FsRtlRegisterFileSystemFilterCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff547172)を参照してください。

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

 

 




