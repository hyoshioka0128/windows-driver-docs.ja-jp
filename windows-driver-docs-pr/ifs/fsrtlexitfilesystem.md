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
ms.openlocfilehash: 00bb1b44085a441f0c79fbaf9478a73b46612466
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370332"
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

ローカル ファイル システムおよびネットワーク リダイレクターとは異なり、ファイル システム フィルター ドライバー、通常カーネル Apc の配信を無効にする必要がありますしないで (呼び出して[ **FsRtlEnterFileSystem** ](fsrtlenterfilesystem.md)または[**KeEnterCriticalRegion** ](https://msdn.microsoft.com/library/windows/hardware/ff552021) IRQL APC を発生させることによって、または\_レベル) の呼び出しを通して[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)します。

ファイル システム フィルター ドライバーに通常のカーネルの Apc を無効にする必要がありますときのみを呼び出す前にすぐには[ **ExAcquireResourceExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544345)、 [ **ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)、 [ **ExAcquireResourceShared**](https://msdn.microsoft.com/library/windows/hardware/ff544359)、 [ **ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)、または[ **ExAcquireSharedStarveExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544367)します。 呼び出した後[ **ExReleaseResource** ](https://msdn.microsoft.com/library/windows/hardware/ff545571)または[ **ExReleaseResourceLite**](https://msdn.microsoft.com/library/windows/hardware/ff545597)、フィルター ドライバーはすぐに再有効化の配信通常カーネル Apc です。 代替手段として[ **FsRtlEnterFileSystem**](fsrtlenterfilesystem.md)、ミニフィルター ドライバーを使用できる、 [ **FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)、 [ **FltAcquireResourceShared**](fltacquireresourceshared.md)、および[ **FltReleaseResource** ](fltreleaseresource.md)取得する際に Apc を正しく処理するルーチンとリソースを解放します。

呼び出す前に、通常のカーネル Apc を無効にする必要はありません[ **ExAcquireSharedWaitForExclusive** ](https://msdn.microsoft.com/library/windows/hardware/ff544370)このルーチンを呼び出すため、 [ **KeRaiseIrqlToDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff553084)、両方の通常の動作と特殊なカーネル Apc を無効にします。 呼び出す前に行う必要ないも[ **ExAcquireFastMutex** ](https://msdn.microsoft.com/library/windows/hardware/ff544337)または[ **ExAcquireResourceExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544345)のため、これらルーチンは、通常のカーネルの Apc を無効にします。

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


[**ExAcquireFastMutex**](https://msdn.microsoft.com/library/windows/hardware/ff544337)

[**ExAcquireResourceExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544345)

[**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)

[**ExAcquireResourceShared**](https://msdn.microsoft.com/library/windows/hardware/ff544359)

[**ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)

[**ExAcquireSharedWaitForExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544370)

[**ExAcquireSharedStarveExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544367)

[**ExReleaseResource**](https://msdn.microsoft.com/library/windows/hardware/ff545571)

[**ExReleaseResourceLite**](https://msdn.microsoft.com/library/windows/hardware/ff545597)

[**ExTryToAcquireFastMutex**](https://msdn.microsoft.com/library/windows/hardware/ff545647)

[**FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)

[**FltAcquireResourceShared**](fltacquireresourceshared.md)

[**FltReleaseResource**](fltreleaseresource.md)

[**FsRtlEnterFileSystem**](fsrtlenterfilesystem.md)

[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)

[**KeLeaveCriticalRegion**](https://msdn.microsoft.com/library/windows/hardware/ff552964)

[**KeRaiseIrqlToDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff553084)

 

 






