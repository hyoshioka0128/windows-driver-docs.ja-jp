---
title: FsRtlEnterFileSystem 関数
description: FsRtlEnterFileSystem マクロは、通常のカーネルモードの非同期プロシージャ呼び出し (APC) の配信を一時的に無効にします。 特別なカーネルモードの Apc は引き続き配信されます。
date: 06/25/2019
ms.assetid: 6aa6315d-e430-4189-8eb5-9427a2e5ba46
keywords:
- FsRtlEnterFileSystem 関数のインストール可能なファイルシステムドライバー
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
ms.openlocfilehash: 7eec3b19a4b10ce4440f35c3cbda2667d3a14e3d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841233"
---
# <a name="fsrtlenterfilesystem-function"></a>FsRtlEnterFileSystem 関数

**Fsrtlenterfilesystem**マクロは、通常のカーネルモードの非同期プロシージャ呼び出し (APC) の配信を一時的に無効にします。 特別なカーネルモードの Apc は引き続き配信されます。

## <a name="syntax"></a>構文

```ManagedCPlusPlus
VOID FsRtlEnterFileSystem(
   VOID
);
```

## <a name="parameters"></a>パラメーター

なし

## <a name="return-value"></a>戻り値

この関数は値を返しません。

## <a name="remarks"></a>注釈

すべてのファイルシステムドライバーのエントリポイントルーチンは、ファイル i/o 要求を実行するために必要なリソースを取得する直前に**Fsrtlenterfilesystem**を呼び出し、その後すぐに[**Fsrtlenterfilesystem**](fsrtlexitfilesystem.md)を呼び出す必要があります。 これにより、ルーチンを実行中に中断したり、他のファイル i/o 要求をブロックしたりすることはできません。

**Fsrtlenterfilesystem**の呼び出しが成功するたびに、後続の[**Fsrtlenterfilesystem**](fsrtlexitfilesystem.md)の呼び出しで一致する必要があります。

ファイルシステムフィルタードライバーは、 [**Fsrtlenterfilesystem**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsrtlexitfilesystem)または[**KeLeaveCriticalRegion が**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)の場合にのみ、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)の前に**Fsrtlenterfilesystem**または[**KeEnterCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)を呼び出すことによって、通常のカーネル apc の配信を無効にすることができます。同じディスパッチルーチン内。 **IoCallDriver**の前に**Fsrtlenterfilesystem**または**KEENTERCRITICALREGION**を呼び出して、IRP の*完了ルーチン*で**fsrtlenterfilesystem**または**KeLeaveCriticalRegion**を呼び出すことはできません。 Driver Verifier には、この状況を検出するための規則があります。

ファイルシステムフィルタードライバーは、リソースを取得する前に通常のカーネル Apc を無効にする必要があります。 ファイルシステムフィルタードライバーは、次のルーチンを使用してリソースを取得します。

* [**ExAcquireResourceExclusive**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)
* [**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)
* [**ExAcquireResourceShared**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)
* [**ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)
* [**ExAcquireSharedStarveExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544367)
* [**ExAcquireSharedWaitForExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544370)

[**FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)、 [**FltAcquireResourceShared**](fltacquireresourceshared.md)、および[**FltReleaseResource**](fltreleaseresource.md)ルーチンは、 **fsrtlenterfilesystem**の代わりに使用できます。このルーチンでは、とを取得するときに、apc を正しく処理します。リソースを解放しています。

## <a name="requirements"></a>要件

|   |   |
| - | - |
| 対象プラットフォーム | Desktop |
| Header | Ntifs (Ntifs を含む) |
| IRQL | < = APC_LEVEL |

## <a name="see-also"></a>関連項目

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

[**FsRtlExitFileSystem**](fsrtlexitfilesystem.md)

[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)

[**KeEnterCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)

[**KeRaiseIrqlToDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirqltodpclevel)
