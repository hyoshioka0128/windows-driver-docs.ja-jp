---
title: FltAcquireResourceExclusive ルーチン
description: FltAcquireResourceExclusive ルーチンは、呼び出し元のスレッドによって排他的にアクセスするために、指定されたリソースを取得します。
ms.assetid: 3736582e-33eb-4967-acfa-4b9d2b8cd87f
keywords:
- FltAcquireResourceExclusive ルーチンのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FltAcquireResourceExclusive
api_location:
- fltMgr.lib
- fltMgr.dll
api_type:
- LibDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 268101c49007d70f2255335f6aa73c7b1ecb62c5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841334"
---
# <a name="fltacquireresourceexclusive-routine"></a>FltAcquireResourceExclusive ルーチン


**FltAcquireResourceExclusive**ルーチンは、呼び出し元のスレッドによって排他的にアクセスするために、指定されたリソースを取得します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
VOID FltAcquireResourceExclusive(
  _Inout_ PERESOURCE Resource
);
```

<a name="parameters"></a>パラメーター
----------

*リソース*\[in、out\]  
不透明な÷構造体を指すポインターです。 この構造体は、呼び出し元によって非ページプールから割り当てられ、 [**Exinitializer eresourcelite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializeresourcelite)または[**Exreinitializer eresourcelite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreinitializeresourcelite)を呼び出すことによって初期化される必要があります。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

このルーチンは、Windows XP Service Pack 2 (SP2)、Windows Server 2003 Service Pack 1 (SP1)、およびそれ以降のバージョンの Windows で使用できます。

**FltAcquireResourceExclusive**は、呼び出し元のスレッドによって排他的にアクセスするために、指定されたリソースを取得します。

次の状況では、指定されたリソースへの排他アクセスが呼び出し元に付与されているかどうかを判断します。

-   リソースが現在所有されていない場合は、現在のスレッドに対して排他アクセスが直ちに許可されます。

-   呼び出し元が既に排他アクセス用にリソースを取得している場合、現在のスレッドは同じ種類のアクセスを再帰的に許可されます。

-   リソースへの共有アクセス権を持つ呼び出し元は、ロックを解放してから排他的に再取得する必要があります。

-   リソースが別のスレッドによって排他的に所有されている場合、または呼び出し元がリソースへの共有アクセスだけを持っている場合は、リソースを取得できるようになるまで、現在のスレッドは待機状態になります。

&gt; \[!2つのスレッドが同じリソースに対して共有ロックを保持していて、共有ロックを解放せずにロックを排他的に取得しようとすると、デッドロックが発生することに注意して\] &gt; ます。 つまり、各スレッドは、他のスレッドがロックに対して共有ホールドを解放するまで待機し、それ以外の場合は共有ホールドを解放しません。

 

**FltAcquireResourceExclusive**は、通常のカーネル APC 配信を無効にする[**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)のラッパーです。

**FltAcquireResourceExclusive**は通常のカーネル APC 配信を無効にするため、 **FltAcquireResourceExclusive**を呼び出す前に[**KeEnterCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)または[**fsrtlenterfilesystem**](fsrtlenterfilesystem.md)を呼び出す必要はありません。

リソースを取得した後に解放するには、 [**FltReleaseResource**](fltreleaseresource.md)を呼び出します。 **FltAcquireResourceExclusive**の呼び出しが成功するたびに、 **FltReleaseResource**への後続の呼び出しで一致する必要があります。

共有アクセス用のリソースを取得するには、 [**FltAcquireResourceShared**](fltacquireresourceshared.md)を呼び出します。

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
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows XP SP2、Windows Server 2003 SP1、およびそれ以降のバージョンのすべての Windows オペレーティングシステムで使用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Fltkernel .h (Fltkernel. h を含む)</td>
</tr>
<tr class="even">
<td align="left"><p>Library</p></td>
<td align="left">fltMgr .lib</td>
</tr>
<tr class="odd">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)

[**ExDeleteResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeleteresourcelite)

[**Ex/Eresourcelite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializeresourcelite)

[**Exreinitializer Eresourcelite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreinitializeresourcelite)

[**FltAcquireResourceShared**](fltacquireresourceshared.md)

[**FltReleaseResource**](fltreleaseresource.md)

[**FsRtlEnterFileSystem**](fsrtlenterfilesystem.md)

[**KeEnterCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)

 

 






