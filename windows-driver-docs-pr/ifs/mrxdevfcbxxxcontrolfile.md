---
title: MRxDevFcbXXXControlFile ルーチン
description: MRxDevFcbXXXControlFile ルーチンは、デバイス FCB コントロール要求 (IOCTL または FSCTL 要求) をネットワークミニリダイレクターに渡すために、RDBSS によって呼び出されます。
ms.assetid: d60449d0-17d0-4303-8d0d-cba091de2b07
keywords:
- MRxDevFcbXXXControlFile ルーチンのインストール可能なファイルシステムドライバー
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxDevFcbXXXControlFile
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2085a7720f06477f14a9dc73edc8c65064fb1a8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841112"
---
# <a name="mrxdevfcbxxxcontrolfile-routine"></a>MRxDevFcbXXXControlFile ルーチン


*MRxDevFcbXXXControlFile*ルーチンは、デバイス FCB コントロール要求 (IOCTL または FSCTL 要求) をネットワークミニリダイレクターに渡すために、 [RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)によって呼び出されます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxDevFcbXXXControlFile;

NTSTATUS MRxDevFcbXXXControlFile(
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

*MRxDevFcbXXXControlFile*は正常に完了した状態\_成功したか、または次のいずれかのような NTSTATUS 値を返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">リターンコード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>STATUS_ACCESS_DENIED</strong></td>
<td align="left"><p>ネットワークミニリダイレクターを停止または開始するための要求が行われましたが、呼び出し元にはこの操作に対する適切なセキュリティがありませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_DEVICE_REQUEST</strong></td>
<td align="left"><p>無効なデバイス要求がネットワークミニリダイレクターに送信されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_REDIRECTOR_HAS_OPEN_HANDLES</strong></td>
<td align="left"><p>これはネットワークミニリダイレクターを停止する要求でしたが、リダイレクターには、この時点で停止できないハンドルが開かれています。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_REDIRECTOR_NOT_STARTED</strong></td>
<td align="left"><p>これはネットワークミニリダイレクターを停止する要求でしたが、リダイレクターが開始されていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_REDIRECTOR_STARTED</strong></td>
<td align="left"><p>これはネットワークミニリダイレクターを開始する要求でしたが、リダイレクターは既に開始されています。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

*MRxDevFcbXXXControlFile*は、ネットワークミニリダイレクターに送信されるデバイス FCB に関連する IOCTL および FSCTL 要求を処理します。

*MRxDevFcbXXXControlFile*を呼び出す前に、RDBSS は、 *RxContext*パラメーターによって示される RX\_コンテキスト構造内の次のメンバーを変更します。

**MajorFunction**は、IRP の主要な関数に設定されています。

これが IRP\_MJ\_FILE\_SYSTEM\_CONTROL 要求であった場合、 *RxContext*パラメーターによって示される RX\_CONTEXT 構造体の次のメンバーが RDBSS によって変更されます。

**FsCtl**は、FsCtl コードのマイナー関数コードに設定されていることを示します。

**FsCtl**が、IRP の FsCtl コードに設定されていることを示します。

これが IRP\_MJ\_デバイス\_CONTROL または IRP\_MJ\_内部\_デバイス\_コントロール要求であった場合、RDBSS は RxContext が指す RX\_CONTEXT 構造体の次のメンバーを変更します。パラメーター:

**FsCtl**は、IRP の制御コードに設定されていることを示します。

*MRxDevFcbXXXControlFile*が STATUS\_SUCCESS を返した場合、ルーチンは成功しました。 その他の戻り値は、エラーが発生したことを示します。

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


[**MRxStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown_ctx)

[**MRxStop**](mrxstop.md)

 

 






