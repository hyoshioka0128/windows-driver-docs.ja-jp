---
title: バグ チェック 0x1C6 FAST_ERESOURCE_PRECONDITION_VIOLATION
description: FAST_ERESOURCE_PRECONDITION_VIOLATION のバグ チェックでは、0x000001C6 の値を持ちます。 これは、現在のスレッドがリソースの高速ルーチンに無効な呼び出しを実行することを示します。
keywords:
- バグ チェック 0x1C6 FAST_ERESOURCE_PRECONDITION_VIOLATION
- FAST_ERESOURCE_PRECONDITION_VIOLATION
ms.date: 01/11/2019
topic_type:
- apiref
api_name:
- FAST_ERESOURCE_PRECONDITION_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2a51f1d883995da59f501da9f4221da1778f918f
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743533"
---
# <a name="bug-check-0x1c6-fasteresourcepreconditionviolation"></a>バグ チェック 0x1C6 の。高速\_÷ リソース\_PRECONDITION\_違反

高速\_÷ リソース\_PRECONDITION\_違反のバグ チェックが 0x000001C6 の値を持ちます。 これは、現在のスレッドがリソースの高速ルーチンに無効な呼び出しを実行することを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。
 

## <a name="fasteresourcepreconditionviolation-parameters"></a>高速\_÷ リソース\_PRECONDITION\_違反パラメーター

|パラメーター|説明|
|-------- |---------- |
|1|違反の種類。 次の値を参照してください。 |
|2| 次の値を参照してください。 |
|3| 次の値を参照してください。 |
|4| 次の値を参照してください。 |

**違反の種類**

```
            0x0 : The Irql of the caller was greater than the maximum allowed
                  Irql for the routine.
                2 - Irql of the caller.
                3 - Maximum allowed Irql of the routine.
            0x1 : The caller specified an invalid (i.e. uninitialized) owner
                  entry.
                2 - Pointer to the owner entry.
            0x2 : The caller specified an owner entry that was already
                  associated with a lock acquisition.
                2 - Pointer to the owner entry.
                3 - Pointer to the resource to which the owner entry is already
                    associated.
            0x3 : The caller passed a legacy resource to a fast resource
                  routine.
                2 - Pointer to the resource.
            0x4 : The caller specified a resource that has outstanding lock
                  acquisitions.
                2 - Pointer to the resource.
            0x5 : The caller was executing inside of a DPC.
            0x6 : The caller was executing inside of a Special Kernel APC.
            0x7 : The caller did not ensure Normal Kernel APCs were disabled.
            0x8 : The caller specified an owner entry that was not associated
                  with a lock acquisition of the specified resource.
                2 - Pointer to the resource specified.
                3 - Pointer to the owner entry.
                4 - Pointer to the resource with which the owner entry is
                    associated.
            0x9 : The caller specified an owner entry that was not associated
                  with the calling thread.
                2 - Pointer to the owner entry.
                3 - Pointer to the thread with which the owner entry is
                    associated.
            0xa : The caller specified an owner entry which has been disowned.
                2 - Pointer to the owner entry.
            0xb : The caller specified an owner entry with a different
                  acquisition type than the caller indicated.
                2 - Pointer to the owner entry.
                3 - High-16 bits indicate the acquisition type of the owner
                    entry. Bottom-16 bits indicate the acquisition type
                    specified. 1 = Shared, 0 = Exclusive.
            0xc : The caller specified an owner entry that was not associated
                  with a lock acquisition of the specified resource.
                2 - Pointer to the resource specified.
                3 - Pointer to the owner entry.
                4 - Pointer to the resource with which the owner entry is
                    associated.
            0xd : The caller specified an owner entry that has not been
                  disowned.
                2 - Pointer to the owner entry.
            0xe : The caller passed a fast resource to a legacy routine that
                  does not support fast resources.
                2 - Pointer to the resource.
            0xf : The caller passed a fast resource to a legacy routine that
                  supports fast resources, but the fast resource was not
                  initialized with EX_FAST_RESOURCE_ENABLE_LEGACY_APIS.
                2 - Pointer to the resource.
            0x10 : The caller passed invalid flags to ExInitializeFastResource.
                2 - Pointer to the resource specified.
                3 - The flags specified.
            0x11 : The caller passed a thread other than the current thread to
                   ExReleaseResourceForThreadLite.
                2 - Pointer to the resource specified.
                3 - The thread specified.
            0x12 : The caller attempted to disown a resource that had been
                   recursively acquired exclusive by the current thread.
                2 - Pointer to the resource specified.
            0x13 : The caller attempted to convert a resource acquisition while
                   the calling thread had outstanding recursive acquisitions of
                   the resource.
                2 - Pointer to the resource specified.
            0x14 : A thread exited with outstanding lock acquisitions.
                2 - The thread.
                3 - Pointer to one of the outstanding owner entries.
            0x15 : A thread exited with outstanding disowned lock acquisitions.
                2 - The thread.
                3 - Pointer to one of the outstanding owner entries.
            0x16 : A call to ExConvertExclusiveToSharedLite was made by a thread
                   that did not hold the specified resource exclusive.
                2 - Pointer to the resource.
                3 - Pointer to the thread.
```


## <a name="cause"></a>原因
-----

現在のスレッドでは、高速リソース ルーチンに無効な呼び出しを実行します。


## <a name="see-also"></a>関連項目
----------

[バグチェック コード リファレンス](bug-check-code-reference2.md)

