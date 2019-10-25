---
title: FsRtlExitFileSystem 関数
description: FsRtlExitFileSystem マクロは、Fsrtlexitfilesystem の前の呼び出しによって無効にされた通常のカーネルモード Apc の配信を再度有効にします。
ms.assetid: 763ceb1c-f614-4268-a7fe-73de0c354c71
keywords:
- FsRtlExitFileSystem 関数のインストール可能なファイルシステムドライバー
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
ms.openlocfilehash: d10444d06d08d273171fa341d40063b34ac35d90
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841230"
---
# <a name="fsrtlexitfilesystem-function"></a>FsRtlExitFileSystem 関数


**Fsrtlexitfilesystem**マクロは、 [**Fsrtlexitfilesystem**](fsrtlenterfilesystem.md)の前の呼び出しによって無効にされた通常のカーネルモード apc の配信を再度有効にします。

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

この関数は値を返しません。

<a name="remarks"></a>注釈
-------

すべてのファイルシステムドライバーのエントリポイントルーチンは、ファイル i/o 要求を実行するために必要なリソースを取得する直前に[**Fsrtlenterfilesystem**](fsrtlenterfilesystem.md)を呼び出し、その後すぐに**Fsrtlenterfilesystem**を呼び出す必要があります。 これにより、ルーチンを実行中に中断したり、他のファイル i/o 要求をブロックしたりすることはできません。

[**Fsrtlenterfilesystem**](fsrtlenterfilesystem.md)の呼び出しが成功するたびに、後続の**Fsrtlenterfilesystem**の呼び出しで一致する必要があります。

ローカルファイルシステムやネットワークリダイレクターとは異なり、ファイルシステムフィルタードライバーは通常のカーネル Apc の配信を無効にしないようにする必要があります。これは、 [**Fsrtlenterfilesystem**](fsrtlenterfilesystem.md)または[**KeEnterCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)を呼び出すか、または IRQL APC の\_レベルにすることによって行います。) を呼び出して[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)します。

ファイルシステムフィルタードライバーが通常のカーネル Apc を無効にする必要があるのは、 [**ExAcquireResourceExclusive**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)、 [**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)、 [**ExAcquireResourceShared**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)を[**呼び出す直前だけです。ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)または[**ExAcquireSharedStarveExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544367)。 [**ExReleaseResource**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)または[**ExReleaseResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaseresourcelite)を呼び出した後、フィルタードライバーは通常のカーネル apc の配信を直ちに有効にする必要があります。 [**FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)、 [**FltAcquireResourceShared**](fltacquireresourceshared.md)、および[**FltReleaseResource**](fltreleaseresource.md)ルーチンは、 [**fsrtlenterfilesystem**](fsrtlenterfilesystem.md)の代わりに使用できます。このルーチンでは、とを取得するときに、apc を正しく処理します。リソースを解放しています。

[**ExAcquireSharedWaitForExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544370)を呼び出す前に通常のカーネル apc を無効にする必要はありません。このルーチンは[**KeRaiseIrqlToDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirqltodpclevel)を呼び出します。これにより、通常のカーネル apc と特殊なカーネル apc の両方が無効になります。 また、 [**ExAcquireFastMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544337(v=vs.85))または[**ExAcquireResourceExclusive**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)を呼び出す前にこれを行う必要はありません。これらのルーチンは通常のカーネル apc を無効にするためです。

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
<td align="left">Ntifs (Ntifs を含む)</td>
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

[**ExReleaseResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaseresourcelite)

[**ExTryToAcquireFastMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545647(v=vs.85))

[**FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)

[**FltAcquireResourceShared**](fltacquireresourceshared.md)

[**FltReleaseResource**](fltreleaseresource.md)

[**FsRtlEnterFileSystem**](fsrtlenterfilesystem.md)

[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)

[**KeLeaveCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)

[**KeRaiseIrqlToDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirqltodpclevel)

 

 






