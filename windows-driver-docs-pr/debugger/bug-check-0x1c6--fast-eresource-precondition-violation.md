---
title: バグチェック 0x1C6 FAST_ERESOURCE_PRECONDITION_VIOLATION
description: FAST_ERESOURCE_PRECONDITION_VIOLATION バグチェックの値は0x000001C6 です。 これは、現在のスレッドが高速リソースルーチンへの無効な呼び出しを実行していることを示します。
keywords:
- バグチェック 0x1C6 FAST_ERESOURCE_PRECONDITION_VIOLATION
- FAST_ERESOURCE_PRECONDITION_VIOLATION
ms.date: 01/11/2019
topic_type:
- apiref
api_name:
- FAST_ERESOURCE_PRECONDITION_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9660018e02da67455a09f51a8528e5da52b5c4ff
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534647"
---
# <a name="bug-check-0x1c6-fast_eresource_precondition_violation"></a>バグチェック 0x1C6: FAST \_ ÷の \_ 前提条件 \_ 違反

FAST \_ ÷ \_ の前提条件違反のバグチェックには、 \_ 0x000001c6 の値が指定されています。 これは、現在のスレッドが高速リソースルーチンへの無効な呼び出しを実行していることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。

 

## <a name="fast_eresource_precondition_violation-parameters"></a>FAST \_ ÷の \_ 前提条件 \_ 違反パラメーター

|パラメーター|説明|
|-------- |---------- |
|1|違反の種類。 以下の値を参照してください。 |
|2| 以下の値を参照してください。 |
|3| 以下の値を参照してください。 |
|4| 以下の値を参照してください。 |

**違反の種類**

```text
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

現在のスレッドは、高速リソースルーチンへの無効な呼び出しを実行しています。

## <a name="resolution"></a>解像度
! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。

## <a name="see-also"></a>参照
----------

[バグ チェック コード リファレンス](bug-check-code-reference2.md)

