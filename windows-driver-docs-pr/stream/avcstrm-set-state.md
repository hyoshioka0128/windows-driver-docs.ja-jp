---
title: AVCSTRM\_\_の状態の設定
description: AVCSTRM\_\_の状態の設定
ms.assetid: 890ae8d1-d7e2-40a4-af7f-b6df32d845e4
keywords:
- AVCSTRM_SET_STATE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- AVCSTRM_SET_STATE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 007ebe7a07b43f40f9a03e2d1749298df8228d7a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845021"
---
# <a name="avcstrm_set_state"></a>AVCSTRM\_\_の状態の設定


## <span id="ddk_avcstrm_set_state_ks"></span><span id="DDK_AVCSTRM_SET_STATE_KS"></span>


**Avcstrm\_SET\_STATE**関数のコードは、指定されたストリームを新しいストリームの状態に配置します。

### <a name="io-status-block"></a>I/O ステータス ブロック

成功した場合、 *avcstrm sys*は、 **Irp&gt;iostatus. status**を status\_SUCCESS に設定します。

考えられるエラーの戻り値は次のとおりです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>エラーの状態</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>STATUS_DEVICE_REMOVED</p></td>
<td><p><strong>AVCSTRM_READ</strong>操作に対応するデバイスは存在しなくなりました。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_CANCELLED</p></td>
<td><p>要求を完了できませんでした。</p></td>
</tr>
<tr class="odd">
<td><p>STATUS_INVALID_PARAMETER</p></td>
<td><p>IRP に指定されたパラメーターが正しくありません。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_INSUFFICIENT_RESOURCES</p></td>
<td><p>要求を完了するための十分なシステムリソースがありませんでした。</p></td>
</tr>
<tr class="odd">
<td><p>あります</p></td>
<td><p>要求は受信されましたが、さらに処理する必要があります。 I/o 完了ルーチンは、最終的な応答を処理します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="comments"></a>コメント

この関数は、次に示すように、AVC\_ストリームの**Commanddata**共用体の**streamstate**メンバーを使用して、\_ブロック構造\_要求します。

```cpp
typedef struct _AVC_STREAM_REQUEST_BLOCK {
  ULONG  SizeOfThisBlock;
  ULONG  Version;
  AVCSTRM_FUNCTION  Function;
  .
  .
  PVOID AVCStreamContext;
  .
  .
  union _tagCommandData {
    .
    .
    KSSTATE  StreamState;
    .
    .
  } CommandData;
} AVC_STREAM_REQUEST_BLOCK, *PAVC_STREAM_REQUEST_BLOCK;
```

### <a name="requirements"></a>要件

**ヘッダー:** *Avcstrm .h*で宣言されています。 *Avcstrm .h*をインクルードします。

### <a name="span-idavc_stream_request_block_inputspanspan-idavc_stream_request_block_inputspanavc_stream_request_block-input"></a><span id="avc_stream_request_block_input"></span><span id="AVC_STREAM_REQUEST_BLOCK_INPUT"></span>\_ストリーム\_要求\_入力をブロックします。

<span id="SizeOfThisBlock__Version_and_Function"></span><span id="sizeofthisblock__version_and_function"></span><span id="SIZEOFTHISBLOCK__VERSION_AND_FUNCTION"></span>**SizeOfThisBlock、バージョン、および関数**  
[**INIT\_AVCSTRM\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/nf-avcstrm-init_avcstrm_header)マクロを使用して、これらのメンバーを初期化します。 マクロの Request 引数に**Avcstrm\_SET\_STATE**を渡します。

<span id="AVCStreamContext"></span><span id="avcstreamcontext"></span><span id="AVCSTREAMCONTEXT"></span>**AVCStreamContext**  
新しいストリームの状態に配置するために、以前の**Avcstrm\_開い**ている呼び出しによって返されるストリームコンテキスト (ハンドル) を指定します。

<span id="StreamState"></span><span id="streamstate"></span><span id="STREAMSTATE"></span>**StreamState**  
ストリームを配置する新しいストリームの状態を指定します。

サブユニットドライバーは、まず IRP と[**AVC\_ストリーム\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_avc_stream_request_block)構造に割り当てる必要があります。 次に、 [**INIT\_avcstrm\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/nf-avcstrm-init_avcstrm_header)マクロを使用して、AVC\_ストリーム\_要求\_ブロック構造を初期化し、 **AVCSTRM\_GET\_STATE**をマクロに要求引数として渡します。 次に、サブユニットドライバーは、 **Avcstreamcontext**メンバーをストリームのストリームコンテキスト (ハンドル) に設定し、ストリームの状態を取得します。

この要求を送信するために、サブユニットは irp [ **\_MJ\_内部\_\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)に送信します。 Irp の**iocontrolcode**メンバーを[**IOCTL\_AVCSTRM\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ni-avcstrm-ioctl_avcstrm_class)および引数1に設定します。新しいストリームの状態に配置するストリームを記述する\_要求\_ブロック構造体に設定された IRP\_ストリームに設定された IRP のメンバー。

サブユニットドライバーは、このコマンドが同期的に完了することを期待できます。 結果は、 *avcstrm .sys*の保留中の操作なしで直ちに返されます。

この関数コードは、IRQL = パッシブ\_レベルで呼び出す必要があります。

### <a name="see-also"></a>参照

[**AVC\_STREAM\_REQUEST\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_avc_stream_request_block)、 [**INIT\_AVCSTRM\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/nf-avcstrm-init_avcstrm_header)、 [**IRP\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)、 [**IOCTL\_avcstrm\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ni-avcstrm-ioctl_avcstrm_class)、 [**Ksstate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ne-ks-ksstate)、 [**avcstrm\_関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ne-avcstrm-_avcstrm_function)

 

 





