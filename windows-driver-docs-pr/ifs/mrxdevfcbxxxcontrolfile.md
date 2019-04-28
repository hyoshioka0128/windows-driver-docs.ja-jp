---
title: MRxDevFcbXXXControlFile ルーチン
description: MRxDevFcbXXXControlFile ルーチンは、ネットワークのミニ リダイレクターにデバイス FCB コントロール要求 (IOCTL または FSCTL 要求) を渡す RDBSS によって呼び出されます。
ms.assetid: d60449d0-17d0-4303-8d0d-cba091de2b07
keywords:
- MRxDevFcbXXXControlFile ルーチン インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: dfce585a92100ceb8f541839671e1e1edbc8b434
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379693"
---
# <a name="mrxdevfcbxxxcontrolfile-routine"></a>MRxDevFcbXXXControlFile ルーチン


*MRxDevFcbXXXControlFile*ルーチンを呼び出して[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)ネットワーク ミニリダイレクターにデバイス FCB コントロール要求 (IOCTL または FSCTL 要求) を渡す。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxDevFcbXXXControlFile;

NTSTATUS MRxDevFcbXXXControlFile(
  _Inout_ PRX_CONTEXT RxContext
)
{ ... }
```

<a name="parameters"></a>パラメーター
----------

*RxContext* \[入力、出力\]  
RX へのポインター\_CONTEXT 構造体。 このパラメーターには、操作を要求している IRP が含まれています。

<a name="return-value"></a>戻り値
------------

*MRxDevFcbXXXControlFile*ステータスを返します\_次のいずれかなど、成功した場合に成功した場合、または、適切な NTSTATUS の値します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">リターン コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>STATUS_ACCESS_DENIED</strong></td>
<td align="left"><p>ネットワーク ミニリダイレクターを起動または停止するように要求されましたが、呼び出し元には、この操作に適切なセキュリティが不足していました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_DEVICE_REQUEST</strong></td>
<td align="left"><p>ネットワークのミニ リダイレクターに、無効なデバイスの要求が送信されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_REDIRECTOR_HAS_OPEN_HANDLES</strong></td>
<td align="left"><p>これは、ネットワークのミニ リダイレクターの停止要求しますが、リダイレクターがこの時点で停止することを防ぐことが開いているハンドル。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_REDIRECTOR_NOT_STARTED</strong></td>
<td align="left"><p>これは、ネットワークのミニ リダイレクターの停止要求しますが、リダイレクターは開始されませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_REDIRECTOR_STARTED</strong></td>
<td align="left"><p>これは、ネットワークのミニ リダイレクターの開始要求しますが、リダイレクターがまだ開始されています。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

*MRxDevFcbXXXControlFile* IOCTL と FSCTL を要求を処理 FCB のデバイスに関連するネットワークのミニ リダイレクターに送信されます。

呼び出しの前に*MRxDevFcbXXXControlFile*、RDBSS、RX では、次のメンバーを変更します\_によって示される CONTEXT 構造体、 *RxContext*パラメーター。

**MajorFunction** IRP の主要な関数に設定されています。

IRP が場合\_MJ\_ファイル\_システム\_RDBSS、RX では、次のメンバーを変更し、コントロールを要求\_によって示される CONTEXT 構造体、 *RxContext*パラメーター。

**LowIoContext.ParamsFor.FsCtl.MinorFunction** FSCTL コードの軽微な関数のコードに設定されています。

**LowIoContext.ParamsFor.FsCtl.FsControlCode** IRP の FSCTL コードに設定されています。

これが IRP 場合\_MJ\_デバイス\_コントロールまたは IRP\_MJ\_内部\_デバイス\_RDBSSRXでは、次のメンバーを変更し、コントロールを要求\_によって示される CONTEXT 構造体、 *RxContext*パラメーター。

**LowIoContext.ParamsFor.FsCtl.FsControlCode** IRP の制御コードに設定されます。

場合*MRxDevFcbXXXControlFile*ステータスを返します\_成功すると、そのルーチンが成功しました。 その他の戻り値は、エラーが発生したことを示します。

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
<td align="left">Mrx.h (Mrx.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**MRxStart**](https://msdn.microsoft.com/library/windows/hardware/ff550829)

[**MRxStop**](mrxstop.md)

 

 






