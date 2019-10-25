---
title: FltReleaseResource ルーチン
description: FltReleaseResource ルーチンは、現在のスレッドが所有する指定されたリソースを解放します。
ms.assetid: 2884c596-77ec-4cba-b6cb-000d96cc6342
keywords:
- FltReleaseResource ルーチンのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FltReleaseResource
api_location:
- fltmgr.sys
api_type:
- DllExport
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b0891934ca079c1bbfa929ff5a7cfbfeff803a2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841327"
---
# <a name="fltreleaseresource-routine"></a>FltReleaseResource ルーチン


**FltReleaseResource**ルーチンは、現在のスレッドが所有する指定されたリソースを解放します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
VOID FltReleaseResource(
  _Inout_ PERESOURCE Resource
);
```

<a name="parameters"></a>パラメーター
----------

*リソース*\[in、out\]  
解放されるリソースの不透明なリソース構造体へのポインター。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

**FltReleaseResource**は、 [**FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)または[**FltAcquireResourceShared**](fltacquireresourceshared.md)を呼び出すことによって既に取得されたリソースを解放します。

**FltReleaseResource**は、通常のカーネル APC 配信を再び実現する[**ExReleaseResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaseresourcelite)のラッパーです。

**FltReleaseResource**は通常のカーネル APC 配信を再び行うため、 **FltReleaseResource**を呼び出した後に[**KeLeaveCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)または[**fsrtlexitfilesystem**](fsrtlexitfilesystem.md)を呼び出す必要はありません。

排他アクセスのためにリソースを取得するには、 [**FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)を呼び出します。

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
<td align="left"><p>このルーチンは、Microsoft Windows XP SP2、Microsoft Windows Server 2003 SP1 以降で使用できます。</p></td>
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
<td align="left"><p>DLL</p></td>
<td align="left">Fltmgr .sys</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= DISPATCH_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**ExDeleteResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeleteresourcelite)

[**Ex/Eresourcelite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializeresourcelite)

[**Exreinitializer Eresourcelite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreinitializeresourcelite)

[**ExReleaseResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaseresourcelite)

[**FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)

[**FltAcquireResourceShared**](fltacquireresourceshared.md)

[**FsRtlExitFileSystem**](fsrtlexitfilesystem.md)

[**KeLeaveCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)

 

 






