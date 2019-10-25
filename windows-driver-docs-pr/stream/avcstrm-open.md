---
title: AVCSTRM\_開いています
description: AVCSTRM\_開いています
ms.assetid: d352615b-8ab8-40ac-b165-479686abd587
keywords:
- AVCSTRM_OPEN ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- AVCSTRM_OPEN
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b2650840e7c6caa9c39b26507f40ac6b9f5c214
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845026"
---
# <a name="avcstrm_open"></a>AVCSTRM\_開いています


## <span id="ddk_avcstrm_open_ks"></span><span id="DDK_AVCSTRM_OPEN_KS"></span>


**Avcstrm\_OPEN**関数のコードは、特定のストリーム形式のストリームを開きます。

### <a name="io-status-block"></a>I/O ステータス ブロック

成功した場合、 *avcstrm sys*は、 **Irp&gt;iostatus. status**を status\_SUCCESS に設定します。

成功した場合は、状態\_SUCCESS が返されます。また、AVC\_ストリームの**Avcstreamcontext**メンバーのストリームコンテキストと共に、[**要求\_ブロック構造\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_avc_stream_request_block)ます。 このコンテキストは、その後、他の*avcstrm .sys*要求に使用されます。

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

この関数では、次に示すように、AVC\_ストリームの**Commanddata**共用体の**openstruct**メンバー\_要求\_ブロック構造体を使用します。

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
    AVCSTRM_OPEN_STRUCT  OpenStruct;
    .
    .
  } CommandData;
} AVC_STREAM_REQUEST_BLOCK, *PAVC_STREAM_REQUEST_BLOCK;
```

### <a name="requirements"></a>要件

**ヘッダー:** *Avcstrm .h*で宣言されています。 *Avcstrm .h*をインクルードします。

### <a name="span-idavc_stream_request_block_inputspanspan-idavc_stream_request_block_inputspanavc_stream_request_block-input"></a><span id="avc_stream_request_block_input"></span><span id="AVC_STREAM_REQUEST_BLOCK_INPUT"></span>\_ストリーム\_要求\_入力をブロックします。

<span id="SizeOfThisBlock__Version_and_Function"></span><span id="sizeofthisblock__version_and_function"></span><span id="SIZEOFTHISBLOCK__VERSION_AND_FUNCTION"></span>**SizeOfThisBlock、バージョン、および関数**  
[**INIT\_AVCSTRM\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/nf-avcstrm-init_avcstrm_header)マクロを使用して、これらのメンバーを初期化します。 マクロの Request 引数で**Avcstrm\_OPEN**を渡します。

<span id="AVCStreamContext"></span><span id="avcstreamcontext"></span><span id="AVCSTREAMCONTEXT"></span>**AVCStreamContext**  
ストリームコンテキスト (ハンドル) を指定します。 この値は、入力時には**NULL**にする必要があります。 **avcstrm\_OPEN**が正常に返された場合、このメンバーには、後続の*avcstrm .sys*操作の有効なストリームコンテキストが含まれます。

<span id="OpenStruct"></span><span id="openstruct"></span><span id="OPENSTRUCT"></span>**OpenStruct**  
作成する AV/C ストリームの説明を指定します。

[**Avcstrm\_FORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ne-avcstrm-_avcstrm_format)列挙体は、サポートされている AV/C ストリーミング形式の一覧を提供し*ます*(IEC 61883 仕様では、sddv (61883-2) や MPEG2TS (61883-4) など)。

アイソクロナス接続を作成するには、CIP headers およびサブユニットに依存するパラメーターが必要であり、 [**Avcstrm\_形式\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_avcstrm_format_info)構造体で定義されています。

データを受信するための MPEG2TS 形式情報の例を次に示します。

```cpp
//
// MPEG2TS
//
    { 
        sizeof(AVCSTRM_FORMAT_INFO),
        AVCSTRM_FORMAT_MPEG2TS,
        {
            0,0,
            CIP_SPH_MPEG, 
            CIP_QPC_MPEG,
            CIP_FN_MPEG,
            IP_DBS_MPEG,
            0,0
        }, // CIP header[0]
        {
            0,0,0,
            CIP_TSF_OFF,
            CIP_FMT_MPEG,
            2,
        },  // CIP header[1]
        SRC_PACKETS_PER_MPEG2TS_FRAME,   // varies depending on number of source packets
        BUFFER_SIZE_MPEG2TS_NO_SPH,   // Remove source packet header
        NUM_OF_XMT_BUFFERS_MPEG2TS,   // Subunit defined
        0,
        FALSE, // not striping SPH is the default
        0,  
        BLOCK_PERIOD_MPEG2TS, // 192, / number of 1394 cycle offset to send one block
        0,0,0,0,
    },
```

サブユニットドライバーは、まず IRP と[**AVC\_ストリーム\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_avc_stream_request_block)構造に割り当てる必要があります。 次に、 [**INIT\_avcstrm\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/nf-avcstrm-init_avcstrm_header)マクロを使用して、AVC\_ストリーム\_要求\_ブロック構造を初期化し、 **avcstrm\_OPEN**をマクロの要求引数として渡します。 次に、サブユニットドライバーは**Avcstreamcontext**メンバーを**NULL**に設定します。 操作が正常に行われた場合、このメンバーには、後続の*avcstrm .sys*操作で使用される有効なストリームコンテキスト (ハンドル) を含める必要があります。 このメンバーは、その後、 [**Avcstrm\_CLOSE**](avcstrm-close.md). でストリームが閉じられるまで、変更しないでください。 最後に、サブユニットドライバーは、開かれるストリームを記述する**Commanddata**共用体の**openstruct**メンバーを設定します。

この要求を送信するために、サブユニットは irp [ **\_MJ\_内部\_\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)に送信します。 Irp の**iocontrolcode**メンバーを[**IOCTL\_AVCSTRM\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ni-avcstrm-ioctl_avcstrm_class)および引数1に設定します。実行するオープン操作が記述されている\_要求\_ブロック構造体に設定される IRP\_ストリームに設定される IRP のメンバー。

サブユニットドライバーは、このコマンドが同期的に完了することを期待できます。 結果は、 *avcstrm .sys*の保留中の操作なしで直ちに返されます。

この関数コードは、IRQL = パッシブ\_レベルで呼び出す必要があります。

### <a name="see-also"></a>参照

[**AVC\_STREAM\_REQUEST\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_avc_stream_request_block)、 [**INIT\_AVCSTRM\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/nf-avcstrm-init_avcstrm_header)、 [**IRP\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)、 [**IOCTL\_avcstrm\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ni-avcstrm-ioctl_avcstrm_class)、 [**Avcstrm\_OPEN\_STRUCT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_avcstrm_open_struct)、 [**avcstrm\_FUNCTION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ne-avcstrm-_avcstrm_function)、 [**avcstrm\_format**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ne-avcstrm-_avcstrm_format)、 [**avcstrm\_format\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_avcstrm_format_info)

 

 





