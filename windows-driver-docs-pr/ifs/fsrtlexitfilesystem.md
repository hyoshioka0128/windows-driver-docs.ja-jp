---
title: FsRtlExitFileSystem 関数
description: FsRtlEnterFileSystem 前の呼び出しによって無効になった通常のカーネル モード Apc の配信を再度有効に FsRtlExitFileSystem マクロ。
ms.assetid: 763ceb1c-f614-4268-a7fe-73de0c354c71
keywords:
- インストール可能なファイル システム ドライバーの FsRtlExitFileSystem 関数
topic_type:
- apiref
api_name:
- FsRtlExitFileSystem
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6363505d37a72ddd1f3bbcc874f0cc160381a611
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365900"
---
# <a name="fsrtlexitfilesystem-function"></a>FsRtlExitFileSystem 関数


**FsRtlExitFileSystem**マクロは、前の呼び出しで無効にされたカーネル モードの通常の Apc の配信を再度有効[ **FsRtlEnterFileSystem**](fsrtlenterfilesystem.md)します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
VOID FsRtlExitFileSystem(
   VOID 
);
```

<a name="parameters"></a>パラメーター
----------

**   
なし

<a name="return-value"></a>戻り値
------------

この関数では、値は返されません。

<a name="remarks"></a>注釈
-------

各ファイル システム ドライバーのエントリ ポイント ルーチンを呼び出す必要があります[ **FsRtlEnterFileSystem** ](fsrtlenterfilesystem.md)すぐにファイル I/O を実行するときに必要なリソースを取得する前に要求し、呼び出す**FsRtlExitFileSystem**直後。 これにより、ファイル I/O 要求の実行およびその他のブロック中に、ルーチンを中断することはできません。

すべての成功した呼び出し[ **FsRtlEnterFileSystem** ](fsrtlenterfilesystem.md)後続の呼び出しによって照合される必要があります**FsRtlExitFileSystem**します。

ローカル ファイル システムおよびネットワーク リダイレクターとは異なり、ファイル システム フィルター ドライバー、通常カーネル Apc の配信を無効にする必要がありますしないで (呼び出して[ **FsRtlEnterFileSystem** ](fsrtlenterfilesystem.md)または[**KeEnterCriticalRegion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keentercriticalregion) IRQL APC を発生させることによって、または\_レベル) の呼び出しを通して[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)します。

ファイル システム フィルター ドライバーに通常のカーネルの Apc を無効にする必要がありますときのみを呼び出す前にすぐには[ **ExAcquireResourceExclusive**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)、 [ **ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)、 [ **ExAcquireResourceShared**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)、 [ **ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)、または[ **ExAcquireSharedStarveExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544367)します。 呼び出した後[ **ExReleaseResource** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)または[ **ExReleaseResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exreleaseresourcelite)、フィルター ドライバーはすぐに再有効化の配信通常カーネル Apc です。 代替手段として[ **FsRtlEnterFileSystem**](fsrtlenterfilesystem.md)、ミニフィルター ドライバーを使用できる、 [ **FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)、 [ **FltAcquireResourceShared**](fltacquireresourceshared.md)、および[ **FltReleaseResource** ](fltreleaseresource.md)取得する際に Apc を正しく処理するルーチンとリソースを解放します。

呼び出す前に、通常のカーネル Apc を無効にする必要はありません[ **ExAcquireSharedWaitForExclusive** ](https://msdn.microsoft.com/library/windows/hardware/ff544370)このルーチンを呼び出すため、 [ **KeRaiseIrqlToDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keraiseirqltodpclevel)、両方の通常の動作と特殊なカーネル Apc を無効にします。 呼び出す前に行う必要ないも[ **ExAcquireFastMutex** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544337(v=vs.85))または[ **ExAcquireResourceExclusive**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)のため、これらルーチンは、通常のカーネルの Apc を無効にします。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>対象プラットフォーム</p></td>
<td align="left">Desktop</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h (Ntifs.h を含む)</td>
</tr>
<tr class="odd">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**ExAcquireFastMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544337(v=vs.85))

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

[**FsRtlEnterFileSystem**](fsrtlenterfilesystem.md)

[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)

[**KeLeaveCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keleavecriticalregion)

[**KeRaiseIrqlToDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keraiseirqltodpclevel)

 

 






