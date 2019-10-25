---
title: MRxSetFileInfoAtCleanup ルーチン
description: MRxSetFileInfoAtCleanup ルーチンは、クリーンアップ時にネットワークミニリダイレクターがファイルシステムオブジェクトにファイル情報を設定するよう要求するために、RDBSS によって呼び出されます。
ms.assetid: 099244ee-cc66-4500-9fee-a10238aaa66c
keywords:
- MRxSetFileInfoAtCleanup ルーチンのインストール可能なファイルシステムドライバー
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxSetFileInfoAtCleanup
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13c2fe54d41d7e46d010c3f3ef6be336284f39ba
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841076"
---
# <a name="mrxsetfileinfoatcleanup-routine"></a>MRxSetFileInfoAtCleanup ルーチン


*MRxSetFileInfoAtCleanup*ルーチンは、クリーンアップ時にネットワークミニリダイレクターがファイルシステムオブジェクトにファイル情報を設定するよう要求するために、 [RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)によって呼び出されます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxSetFileInfoAtCleanup;

NTSTATUS MRxSetFileInfoAtCleanup(
  _Inout_ PRX_CONTEXT RxContext
)
{ ... }
```

<a name="parameters"></a>parameters
----------

*RxContext* \[in、out\]  
RX\_コンテキスト構造体へのポインター。 このパラメーターには、操作を要求している IRP が含まれています。

<a name="return-value"></a>戻り値
------------

*MRxSetFileInfoAtCleanup*は正常に完了した場合、または適切な NTSTATUS 値を\_状態を返します。

<a name="remarks"></a>解説
-------

RDBSS は、ファイルオブジェクトへの最後のハンドルが閉じられたときに、クリーンアップ中に*MRxSetFileInfoAtCleanup*への呼び出しを発行します。 これは、ファイルオブジェクトへの最後の参照が削除されたときに呼び出される close 操作とは異なります。

*MRxSetFileInfoAtCleanup*は、ファイルのタイムスタンプまたはファイルのサイズが変更された場合に、RDBSS によって呼び出されます。 *MRxSetFileInfoAtCleanup* by RDBSS の呼び出しは、これらの変更ごとに個別に行われます。 ファイルサイズとタイムスタンプの両方が変更された場合、RDBSS は*MRxSetFileInfoAtCleanup*を2回呼び出します。

*MRxSetFileInfoAtCleanup*を呼び出す前に、RDBSS は、ファイルのタイムスタンプが変更された場合に*RxContext*パラメーターが指す RX\_コンテキスト構造内の次のメンバーを変更します。

**Info. FileInformationClass**メンバーは、FILEINFORMATIONCLASS のファイル\_情報\_クラス値に設定されます。

**情報バッファー**のメンバーは、スタックに割り当てられた基本\_情報構造\_ファイルに設定されます。

**情報の長さ**のメンバーは、基本\_情報の構造\_、ファイルの sizeof に設定されます。

*MRxSetFileInfoAtCleanup*を呼び出す前に、RDBSS は、ファイルのサイズが変更された場合に*RxContext*パラメーターが指す RX\_コンテキスト構造内の次のメンバーを変更します。

FileEndOfFileInformation の\_クラス値のファイル\_情報に設定され**ます。**

情報**バッファー**のメンバーは、スタックに割り当てられている\_ファイル\_情報構造の末尾\_\_ファイルに設定されます。

**Info**メンバーは<strong>sizeof (</strong>file\_END\_\_ファイル\_情報<strong>)</strong>に設定されます。

RDBSS は、 *MRxSetFileInfoAtCleanup*からの戻り値を無視します。

ネットワークミニリダイレクターは、このルーチンで何も実行しないことを選択し、状態\_SUCCESS を返します。 ファイルサイズまたはタイムスタンプに対する変更は、クリーンアップ操作中に処理されます。

<a name="requirements"></a>前提条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>ターゲットプラットフォーム</p></td>
<td align="left">デスクトップ</td>
</tr>
<tr class="even">
<td align="left"><p>ヘッダー</p></td>
<td align="left">Mrx .h (Mrx を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**MRxIsValidDirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_chkdir_calldown)

[**MRxQueryDirectory**](mrxquerydirectory.md)

[**MRxQueryEaInfo**](mrxqueryeainfo.md)

[**MRxQueryFileInfo**](mrxqueryfileinfo.md)

[**MRxQueryQuotaInfo**](mrxqueryquotainfo.md)

[**MRxQuerySdInfo**](mrxquerysdinfo.md)

[**MRxQueryVolumeInfo**](mrxqueryvolumeinfo.md)

[**MRxSetEaInfo**](mrxseteainfo.md)

[**MRxSetFileInfo**](mrxsetfileinfo.md)

[**MRxSetQuotaInfo**](mrxsetquotainfo.md)

[**MRxSetSdInfo**](mrxsetsdinfo.md)

[**MRxSetVolumeInfo**](mrxsetvolumeinfo.md)

 

 






