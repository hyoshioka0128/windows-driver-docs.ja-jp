---
title: FltAcquireResourceShared ルーチン
description: FltAcquireResourceShared ルーチンでは、呼び出し元のスレッドによって共有アクセス用の特定のリソースを取得します。
ms.assetid: 5232cdba-1050-46b6-8c21-177d4cd1721d
keywords:
- FltAcquireResourceShared ルーチン インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: c31804be6bd12a9b8a3d2c618c8d9ce3fe67e198
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384579"
---
# <a name="fltacquireresourceshared-routine"></a>FltAcquireResourceShared ルーチン


**FltAcquireResourceShared**ルーチンは、呼び出し元のスレッドによって共有アクセス用の特定のリソースを取得します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
VOID FltAcquireResourceShared(
  _Inout_ PERESOURCE Resource
);
```

<a name="parameters"></a>パラメーター
----------

*リソース*\[入力、出力\]  
非透過のスケジュール作成構造体へのポインター。 この構造体の非ページ プールから呼び出し元が割り当てたを呼び出すことによって初期化する必要があります[ **ExInitializeResourceLite** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializeresourcelite)または[ **ExReinitializeResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exreinitializeresourcelite).

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

このルーチンは Microsoft Windows XP SP2、Microsoft Windows Server 2003 SP1 で使用できる以降。

**FltAcquireResourceShared**ルーチンは、呼び出し元のスレッドによって共有アクセス用の特定のリソースを取得します。

かどうか、または呼び出し元が指定されている場合は、特定のリソースへの共有アクセスは、次に依存します。

-   リソースが現在所有されている場合は、共有アクセスは、現在のスレッドをすぐに許可します。

-   呼び出し元がリソースを取得して (共有または排他アクセス) する場合、同じ種類のアクセスを再帰的に、現在のスレッドが許可されます。 この呼び出しを行うも共有する特定のリソースの呼び出し元の排他的所有権は変換されませんに注意してください。

-   リソースが現在として所有している場合は、別のスレッドによって共有リソースへの排他アクセスを待機しているスレッドがないとは、共有アクセスがすぐに呼び出し元に許可します。 呼び出し元は、排他の待機がある場合、待機状態に配置されます。

-   リソースは、別のスレッドによって排他として現在所有しているか、排他アクセスを待機している別のスレッドがあり、呼び出し元は存在しない場合は、リソースへのアクセスを共有が、現在のスレッドは、リソースを取得するまで待機状態に配置されます。

**FltAcquireResourceShared**用のラッパーです[ **ExAcquireResourceSharedLite** ](https://msdn.microsoft.com/library/windows/hardware/ff544363)通常カーネル APC 配信を無効にします。

**FltAcquireResourceShared**通常カーネル APC の配信を無効にしますを呼び出す必要はありません[ **KeEnterCriticalRegion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keentercriticalregion)または[ **。FsRtlEnterFileSystem** ](fsrtlenterfilesystem.md)呼び出す前に**FltAcquireResourceShared**します。

呼び出すには、取得した後は、リソースを解放、 [ **FltReleaseResource**](fltreleaseresource.md)します。 すべての成功した呼び出し**FltAcquireResourceShared**後続の呼び出しによって照合される必要があります**FltReleaseResource**します。

リソースへの排他アクセスを取得するために呼び出す[ **FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)します。

システムのリソースの一覧からリソースを削除する[ **ExDeleteResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeleteresourcelite)します。

再利用するためのリソースを初期化するために呼び出す[ **ExReinitializeResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exreinitializeresourcelite)します。

次の構造体の詳細については、次を参照してください。 [÷ リソース ルーチンの概要](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-eresource-routines)でカーネルのアーキテクチャの設計ガイド。

<a name="requirements"></a>必要条件
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
<td align="left">Fltkernel.h (Fltkernel.h を含む)</td>
</tr>
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">FltMgr.lib</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)

[**ExDeleteResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeleteresourcelite)

[**ExInitializeResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializeresourcelite)

[**ExReinitializeResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exreinitializeresourcelite)

[**FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)

[**FltReleaseResource**](fltreleaseresource.md)

[**FsRtlEnterFileSystem**](fsrtlenterfilesystem.md)

[**KeEnterCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keentercriticalregion)

 

 






