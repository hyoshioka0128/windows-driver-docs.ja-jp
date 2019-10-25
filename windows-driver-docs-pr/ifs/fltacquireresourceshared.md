---
title: FltAcquireResourceShared ルーチン
description: FltAcquireResourceShared ルーチンは、呼び出し元のスレッドによって共有アクセス用に指定されたリソースを取得します。
ms.assetid: 5232cdba-1050-46b6-8c21-177d4cd1721d
keywords:
- FltAcquireResourceShared ルーチンのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FltAcquireResourceShared
api_location:
- FltMgr.lib
- FltMgr.dll
api_type:
- LibDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3d630a061d2cba4ff08d394a6b06b98a10acc32
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841332"
---
# <a name="fltacquireresourceshared-routine"></a>FltAcquireResourceShared ルーチン


**FltAcquireResourceShared**ルーチンは、呼び出し元のスレッドによって共有アクセス用に指定されたリソースを取得します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
VOID FltAcquireResourceShared(
  _Inout_ PERESOURCE Resource
);
```

<a name="parameters"></a>パラメーター
----------

*リソース*\[in、out\]  
不透明な÷構造体へのポインター。 この構造体は、呼び出し元によって非ページプールから割り当てられ、 [**Exinitializer eresourcelite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializeresourcelite)または[**Exreinitializer eresourcelite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreinitializeresourcelite)を呼び出すことによって初期化される必要があります。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

このルーチンは、Microsoft Windows XP SP2、Microsoft Windows Server 2003 SP1 以降で使用できます。

**FltAcquireResourceShared**ルーチンは、呼び出し元のスレッドによって共有アクセス用に指定されたリソースを取得します。

指定したリソースへの共有アクセスが呼び出し元に付与されているかどうかは、次のことに依存します。

-   リソースが現在所有されていない場合は、現在のスレッドに対して共有アクセスが直ちに付与されます。

-   呼び出し元が既にリソースを取得している場合 (共有または排他アクセスの場合)、現在のスレッドは同じ種類のアクセスを再帰的に許可されます。 この呼び出しを行っても、特定のリソースの呼び出し元の排他所有権が共有に変換されることはないことに注意してください。

-   リソースが別のスレッドによって共有されているものの、リソースへの排他アクセスを待機しているスレッドがない場合、共有アクセスはすぐに呼び出し元に付与されます。 排他的な待機が発生した場合、呼び出し元は待機状態になります。

-   リソースが別のスレッドによって排他的に所有されている場合、または排他的アクセスを待機している別のスレッドが存在し、呼び出し元がリソースへの共有アクセスをまだ持っていない場合は、リソースが取得されるまで、現在のスレッドは待機状態になります。

**FltAcquireResourceShared**は、通常のカーネル APC 配信を無効にする[**ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)のラッパーです。

**FltAcquireResourceShared**は通常のカーネル APC 配信を無効にするため、 **FltAcquireResourceShared**を呼び出す前に[**KeEnterCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)または[**fsrtlenterfilesystem**](fsrtlenterfilesystem.md)を呼び出す必要はありません。

リソースを取得した後に解放するには、 [**FltReleaseResource**](fltreleaseresource.md)を呼び出します。 **FltAcquireResourceShared**の呼び出しが成功するたびに、 **FltReleaseResource**への後続の呼び出しで一致する必要があります。

排他アクセスのためにリソースを取得するには、 [**FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)を呼び出します。

システムのリソースリストからリソースを削除するには、 [**ExDeleteResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeleteresourcelite)を呼び出します。

再利用するためにリソースを初期化するには、 [**Exreinitializer Eresourcelite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreinitializeresourcelite)を呼び出します。

÷の構造体の詳細については、「カーネルアーキテクチャの設計ガイド」の「のについて」[を](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-eresource-routines)参照してください。

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
<td align="left"><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">ユニバーサル</a></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Fltkernel .h (Fltkernel. h を含む)</td>
</tr>
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">fltMgr .lib</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)

[**ExDeleteResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeleteresourcelite)

[**Ex/Eresourcelite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializeresourcelite)

[**Exreinitializer Eresourcelite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreinitializeresourcelite)

[**FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)

[**FltReleaseResource**](fltreleaseresource.md)

[**FsRtlEnterFileSystem**](fsrtlenterfilesystem.md)

[**KeEnterCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)

 

 






