---
title: CcUnmapFileOffsetFromSystemCache ルーチン
description: CcUnmapFileOffsetFromSystemCache ルーチンでは、システム キャッシュからキャッシュされたファイルの一部を削除します。
ms.assetid: 37C4ACB9-343D-4F5F-A8B8-FB99A7EA274A
keywords:
- CcUnmapFileOffsetFromSystemCache ルーチン インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- CcUnmapFileOffsetFromSystemCache
api_location:
- NtosKrnl.exe
api_type:
- DllExport
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: be3b2fc09ff6a1a808001f191342d724ec9737e4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369578"
---
# <a name="ccunmapfileoffsetfromsystemcache-routine"></a>CcUnmapFileOffsetFromSystemCache ルーチン


[ **CcUnmapFileOffsetFromSystemCache** ](ccsetreadaheadgranularityex.md)ルーチン システム キャッシュからキャッシュされたファイルの一部を削除します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
VOID CcUnmapFileOffsetFromSystemCache(
  _In_ PFILE_OBJECT   FileObject,
  _In_ PLARGE_INTEGER FileOffset,
  _In_ ULONG          Length,
  _In_ ULONG          Flags
);
```

<a name="parameters"></a>パラメーター
----------

*FileObject* \[in\]  
キャッシュ メモリがマップされますが、キャッシュされたファイルのファイル オブジェクトへのポインター。

*FileOffset* \[in\]  
システム キャッシュからのマッピング解除を開始するファイルの場所へのポインター。

*長さ*\[で\]  
キャッシュからマップ解除するファイルの部分の長さ。 場合*長さ*0 の場合、ファイルから始まるメモリ セクションの残りの部分は、 *FileOffset*、マップ解除されています。

*フラグ*\[で\]  
使用されていません。 設定*フラグ*を 0 にします。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

両方を設定*FileOffset*と*長さ*を 0 にすると、 [ **CcUnmapFileOffsetFromSystemCache** ](ccsetreadaheadgranularityex.md)全体のメモリのセクションをマップ解除するにはキャッシュされたファイル。

[**CcUnmapFileOffsetFromSystemCache** ](ccsetreadaheadgranularityex.md)ファイル システム ドライバー ファイルの部分の数が多いがシステムのキャッシュに保持されているときに、キャッシュの使用率を削減することができます。

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
<td align="left"><p>Windows 8 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h (Ntifs.h を含む)</td>
</tr>
<tr class="even">
<td align="left"><p>Library</p></td>
<td align="left">NtosKrnl.lib</td>
</tr>
<tr class="odd">
<td align="left"><p>DLL</p></td>
<td align="left">NtosKrnl.exe</td>
</tr>
</tbody>
</table>

 

 





