---
title: AVCSTRM\_書き込み
description: AVCSTRM\_書き込み
ms.assetid: de11778d-21ab-40ae-8e7f-5229acfeea42
keywords:
- AVCSTRM_WRITE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- AVCSTRM_WRITE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: de330cbacf319682d85b616c2ee4aa8371381c83
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845029"
---
# <a name="avcstrm_write"></a>AVCSTRM\_書き込み


## <span id="ddk_avcstrm_write_ks"></span><span id="DDK_AVCSTRM_WRITE_KS"></span>


**Avcstrm\_WRITE**関数のコードは、指定されたストリームに送信されるデータバッファーを送信するために使用されます。

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

この関数では、次に示すように、AVC\_ストリームの**Commanddata**共用体の**bufferstruct**メンバー\_要求\_ブロック構造体を使用します。

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
    AVCSTRM_BUFFER_STRUCT  BufferStruct;
    .
    .
  } CommandData;
} AVC_STREAM_REQUEST_BLOCK, *PAVC_STREAM_REQUEST_BLOCK;
```

### <a name="requirements"></a>要件

**ヘッダー:** *Avcstrm .h*で宣言されています。 *Avcstrm .h*をインクルードします。

### <a name="span-idavc_stream_request_block_inputspanspan-idavc_stream_request_block_inputspanavc_stream_request_block-input"></a><span id="avc_stream_request_block_input"></span><span id="AVC_STREAM_REQUEST_BLOCK_INPUT"></span>\_ストリーム\_要求\_入力をブロックします。

<span id="SizeOfThisBlock__Version_and_Function"></span><span id="sizeofthisblock__version_and_function"></span><span id="SIZEOFTHISBLOCK__VERSION_AND_FUNCTION"></span>**SizeOfThisBlock、バージョン、および関数**  
[**INIT\_AVCSTRM\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/nf-avcstrm-init_avcstrm_header)マクロを使用して、これらのメンバーを初期化します。 マクロの要求引数で**Avcstrm\_WRITE**を渡します。

<span id="AVCStreamContext"></span><span id="avcstreamcontext"></span><span id="AVCSTREAMCONTEXT"></span>**AVCStreamContext**  
データ書き込み操作の対象となる、以前の**Avcstrm\_オープン**呼び出しによって返されるストリームコンテキスト (ハンドル) を指定します。

<span id="BufferStruct"></span><span id="bufferstruct"></span><span id="BUFFERSTRUCT"></span>**BufferStruct**  
書き込み操作がデータを取得するバッファーを指定します。

サブユニットドライバーは、まず IRP と[**AVC\_ストリーム\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_avc_stream_request_block)構造に割り当てる必要があります。 次に、 [**INIT\_avcstrm\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/nf-avcstrm-init_avcstrm_header)マクロを使用して、AVC\_\_ストリームを初期化し\_ブロック構造を初期化し、 **avcstrm\_** を request 引数としてマクロに渡します。 次に、サブユニットドライバーは、 **Avcstreamcontext**メンバーを、データ書き込み操作の対象となるストリームのストリームコンテキスト (ハンドル) に設定します。 最後に、サブユニットドライバーは、書き込み操作がデータを取得するバッファーを記述する**Commanddata**共用体の**bufferstruct**メンバーを設定します。

この要求を送信するために、サブユニットは irp [ **\_MJ\_内部\_\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)に送信します。 Irp の**iocontrolcode**メンバーを[**IOCTL\_AVCSTRM\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ni-avcstrm-ioctl_avcstrm_class)および引数1に設定します。実行する書き込み操作を記述する\_要求\_ブロック構造体に設定される IRP\_ストリームに設定された IRP のメンバー。

このコマンドは、非同期的に完了します。 完了すると、IRP で設定された i/o 完了ルーチンが呼び出されます。

この関数コードは、IRQL = パッシブ\_レベルで呼び出す必要があります。

### <a name="see-also"></a>参照

[**AVC\_STREAM\_REQUEST\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_avc_stream_request_block)、 [**INIT\_AVCSTRM\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/nf-avcstrm-init_avcstrm_header)、 [**IRP\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)、 [**IOCTL\_avcstrm\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ni-avcstrm-ioctl_avcstrm_class)、 [**Avcstrm\_BUFFER\_STRUCT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_avcstrm_buffer_struct)、 [**avcstrm\_関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ne-avcstrm-_avcstrm_function)

 

 





