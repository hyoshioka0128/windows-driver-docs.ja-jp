---
title: FsRtlEnterFileSystem 関数
description: FsRtlEnterFileSystem マクロは、カーネル モードの通常非同期プロシージャ コール (APC) の配信を一時的に無効にします。 特殊なカーネル モードの Apc が引き続き配信されます。
date: 06/25/2019
ms.assetid: 6aa6315d-e430-4189-8eb5-9427a2e5ba46
keywords:
- インストール可能なファイル システム ドライバーの FsRtlEnterFileSystem 関数
topic_type:
- apiref
api_name:
- FsRtlEnterFileSystem
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: df21f165ebb51f6a55de87d375b4226696e026ff
ms.sourcegitcommit: 61d5dccad989614313be2e59df6e08cd46364e76
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2019
ms.locfileid: "67412217"
---
# <a name="fsrtlenterfilesystem-function"></a>FsRtlEnterFileSystem 関数

**FsRtlEnterFileSystem**マクロは、カーネル モードの通常非同期プロシージャ コール (APC) の配信を一時的に無効にします。 特殊なカーネル モードの Apc が引き続き配信されます。

## <a name="syntax"></a>構文

```ManagedCPlusPlus
VOID FsRtlEnterFileSystem(
   VOID
);
```

## <a name="parameters"></a>パラメーター

なし

## <a name="return-value"></a>戻り値

この関数では、値は返されません。

## <a name="remarks"></a>注釈

各ファイル システム ドライバーのエントリ ポイント ルーチンを呼び出す必要があります**FsRtlEnterFileSystem**すぐにファイル I/O を実行するときに必要なリソースを取得する前に要求し、呼び出す[ **FsRtlExitFileSystem**](fsrtlexitfilesystem.md)直後。 これにより、ファイル I/O 要求の実行およびその他のブロック中に、ルーチンを中断することはできません。

すべての成功した呼び出し**FsRtlEnterFileSystem**後続の呼び出しによって照合される必要があります[ **FsRtlExitFileSystem**](fsrtlexitfilesystem.md)します。

ファイル システム フィルター ドライバーは、通常カーネル Apc の配信を無効に呼び出して**FsRtlEnterFileSystem**または[ **KeEnterCriticalRegion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keentercriticalregion)より前のバージョン[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)場合にのみ[ **FsRtlExitFileSystem** ](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsrtlexitfilesystem)または[ **KeLeaveCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keleavecriticalregion)同じディスパッチ ルーチンでは、します。 いない呼び出す必要がある**FsRtlEnterFileSystem**または**KeEnterCriticalRegion**より前のバージョン**保留**を呼び出して**FsRtlExitFileSystem**または**KeLeaveCriticalRegion**で、*完了ルーチン*IRP の。 Driver Verifier は、この条件を捕捉しやすくルール。

ファイル システム フィルター ドライバーは、任意のリソースを取得する前に、通常カーネル Apc を無効にする必要があります。 ファイル システム フィルター ドライバーは、次のルーチンでリソースを取得します。

* [**ExAcquireResourceExclusive**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)
* [**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)
* [**ExAcquireResourceShared**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)
* [**ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)
* [**ExAcquireSharedStarveExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544367)
* [**ExAcquireSharedWaitForExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544370)

代替手段として**FsRtlEnterFileSystem**、ミニフィルター ドライバーを使用できる、 [ **FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)、 [ **FltAcquireResourceShared**](fltacquireresourceshared.md)、および[ **FltReleaseResource** ](fltreleaseresource.md)獲得およびリソースを解放するときに Apc を適切に処理するルーチン。

## <a name="requirements"></a>必要条件

|   |   |
| - | - |
| 対象プラットフォーム | Desktop |
| Header | Ntifs.h (Ntifs.h を含む) |
| IRQL | <= APC_LEVEL |

## <a name="see-also"></a>関連項目

[**ExAcquireResourceExclusive**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)

[**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)

[**ExAcquireResourceShared**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)

[**ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)

[**ExAcquireSharedWaitForExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544370)

[**ExAcquireSharedStarveExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544367)

[**ExReleaseResource**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)

[**ExReleaseResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exreleaseresourcelite)

[**ExTryToAcquireFastMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545647(v=vs.85))

[**FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)

[**FltAcquireResourceShared**](fltacquireresourceshared.md)

[**FltReleaseResource**](fltreleaseresource.md)

[**FsRtlExitFileSystem**](fsrtlexitfilesystem.md)

[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)

[**KeEnterCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keentercriticalregion)

[**KeRaiseIrqlToDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keraiseirqltodpclevel)
