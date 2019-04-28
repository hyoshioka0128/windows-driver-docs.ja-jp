---
title: CcIsThereDirtyLoggedPages ルーチン
description: CcIsThereDirtyLoggedPages ルーチンは、ボリュームがダーティ ログ データがシステム キャッシュにあるすべてのファイルを含むかどうかを判断します。
ms.assetid: B8FDD817-87E6-4D82-B668-7F1078041281
keywords:
- CcIsThereDirtyLoggedPages ルーチン インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- CcIsThereDirtyLoggedPages
api_location:
- NtosKrnl.exe
api_type:
- DllExport
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 745807c96a29eb281e946647eaf044054e839315
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378026"
---
# <a name="ccistheredirtyloggedpages-routine"></a>CcIsThereDirtyLoggedPages ルーチン


**CcIsThereDirtyLoggedPages**ルーチンは、ボリュームがシステム キャッシュのダーティ ログ データを格納しているすべてのファイルを含むかどうかを決定します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
BOOLEAN CcIsThereDirtyLoggedPages(
  _In_     PDEVICE_OBJECT DeviceObject,
  _In_opt_ PULONG         NumberOfDirtyPages
);
```

<a name="parameters"></a>パラメーター
----------

*DeviceObject* \[in\]  
確認するボリュームに関連付けられているデバイスのオブジェクトへのポインター。

*NumberOfDirtyPages* \[で、省略可能\]  
ポインターを省略可能な**ULONG**ダーティ ログ ページに関連付けられているボリューム上の数を受け取るバッファー*デバイス オブジェクト*します。

<a name="return-value"></a>戻り値
------------

**CcIsThereDirtyLoggedPages**ルーチンを返します。 **TRUE**ボリュームにログ データをキャッシュに変更されたが、まだディスクにフラッシュされていない 1 つまたは複数のキャッシュされたファイルが含まれます。 このルーチンを返しますそれ以外の場合、 **FALSE**します。

<a name="remarks"></a>注釈
-------

このルーチンは返します**TRUE**ログのダーティ ページが存在しない場合。 返します**TRUE**ログ ページが現在、ボリュームにキューがある場合。

異なり[ **CcIsThereDirtyDataEx**](https://msdn.microsoft.com/library/windows/hardware/ff539152)、 **CcIsThereDirtyLoggedPages**ルーチンでは、ファイル システムのデバイス オブジェクトを使用して、ダーティを確認するボリューム キャッシュ情報を検索するにはページにログインします。

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
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 8 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h (Ntifs.h または FltKernel.h を含む)</td>
</tr>
<tr class="even">
<td align="left"><p>Library</p></td>
<td align="left">NtosKrnl.lib</td>
</tr>
<tr class="odd">
<td align="left"><p>DLL</p></td>
<td align="left">NtosKrnl.exe</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**CcFlushCache**](https://msdn.microsoft.com/library/windows/hardware/ff539082)

[**CcPurgeCacheSection**](https://msdn.microsoft.com/library/windows/hardware/ff539188)

[**CcIsThereDirtyDataEx**](https://msdn.microsoft.com/library/windows/hardware/ff539152)

 

 






