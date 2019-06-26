---
title: AVCSTRM\_開く
description: AVCSTRM\_開く
ms.assetid: d352615b-8ab8-40ac-b165-479686abd587
keywords:
- AVCSTRM_OPEN ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- AVCSTRM_OPEN
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2877bce3c32ca5aec13d1b1bbb9cfc0aa38eb6f6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386718"
---
# <a name="avcstrmopen"></a>AVCSTRM\_開く


## <span id="ddk_avcstrm_open_ks"></span><span id="DDK_AVCSTRM_OPEN_KS"></span>


**AVCSTRM\_オープン**関数のコードは、特定のストリームの形式でストリームを開きます。

### <a name="io-status-block"></a>I/O ステータス ブロック

成功した場合、 *avcstrm.sys*設定**Irp -&gt;IoStatus.Status**ステータス\_成功します。

成功した場合、ステータス\_でストリームのコンテキストと共に成功が返される**AVCStreamContext**のメンバー、 [ **AVC\_ストリーム\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avcstrm/ns-avcstrm-_avc_stream_request_block)構造体。 このコンテキストは、後で、その他の使用*avcstrm.sys*要求。

値には、可能性のあるエラーが返されます。

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
<td><p>対応するデバイス、 <strong>AVCSTRM_READ</strong>操作が存在しません。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_CANCELLED</p></td>
<td><p>要求は完了できませんでした。</p></td>
</tr>
<tr class="odd">
<td><p>STATUS_INVALID_PARAMETER</p></td>
<td><p>IRP で指定されたパラメーターが正しくないです。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_INSUFFICIENT_RESOURCES</p></td>
<td><p>要求を完了するための十分なシステム リソースがありませんでした。</p></td>
</tr>
<tr class="odd">
<td><p>STATUS_PENDING</p></td>
<td><p>要求を受け取りましたが、さらに処理が必要です。 I/O 完了ルーチンでは、最後の応答を処理します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="comments"></a>コメント

この関数を使用して、 **OpenStruct**のメンバー、 **CommandData**共用体、AVC の\_ストリーム\_要求\_ブロック構造の下に示すようにします。

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

### <a name="requirements"></a>必要条件

**ヘッダー:** 宣言されている*avcstrm.h*します。 含める*avcstrm.h*します。

### <a name="span-idavcstreamrequestblockinputspanspan-idavcstreamrequestblockinputspanavcstreamrequestblock-input"></a><span id="avc_stream_request_block_input"></span><span id="AVC_STREAM_REQUEST_BLOCK_INPUT"></span>AVC\_ストリーム\_要求\_ブロックの入力

<span id="SizeOfThisBlock__Version_and_Function"></span><span id="sizeofthisblock__version_and_function"></span><span id="SIZEOFTHISBLOCK__VERSION_AND_FUNCTION"></span>**SizeOfThisBlock、バージョン、および関数**  
使用して、 [ **INIT\_AVCSTRM\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avcstrm/nf-avcstrm-init_avcstrm_header)マクロをこれらのメンバーを初期化します。 渡す**AVCSTRM\_オープン**マクロの要求の引数にします。

<span id="AVCStreamContext"></span><span id="avcstreamcontext"></span><span id="AVCSTREAMCONTEXT"></span>**AVCStreamContext**  
ストリームのコンテキスト (ハンドル) を指定します。 これは、アカウントは**NULL** 、入力の場合に**AVCSTRM\_オープン**このメンバーには有効なストリームのコンテキストが含まれていますが、正常に返さ後続*avcstrm.sys*操作です。

<span id="OpenStruct"></span><span id="openstruct"></span><span id="OPENSTRUCT"></span>**OpenStruct**  
作成される AV/C ストリームの説明を指定します。

[ **AVCSTRM\_形式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avcstrm/ne-avcstrm-_avcstrm_format)列挙体は (IEC 61883 仕様) からの AV/C のサポートされているストリーミング形式の一覧を*avcstrm.sys*SDDV (61883 2) と MPEG2TS (61883 ~ 4) などをサポートする。

パラメーター アイソクロナスの接続、CIP ヘッダーおよびサブユニットが依存するようにするために必要なし、で定義されて、 [ **AVCSTRM\_形式\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avcstrm/ns-avcstrm-_avcstrm_format_info)構造体。

MPEG2TS 形式については、データを受信するための例を次に示します。

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

サブユニット ドライバーは IRP を割り当てる必要があります最初、 [ **AVC\_ストリーム\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avcstrm/ns-avcstrm-_avc_stream_request_block)構造体。 次に、使用する必要があります、 [ **INIT\_AVCSTRM\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avcstrm/nf-avcstrm-init_avcstrm_header) 、AVC を初期化するためにマクロ\_ストリーム\_要求\_ブロック構造体渡す**AVCSTRM\_オープン**マクロに要求の引数として。 次に、サブユニット ドライバーの設定、 **AVCStreamContext**メンバー **NULL**します。 このメンバーの操作が成功すると、その後で使用されている有効なストリーム コンテキスト (ハンドル) を含める必要があります*avcstrm.sys*操作。 このメンバーは変更できませんその後で、ストリームが閉じられるまで[ **AVCSTRM\_閉じる**](avcstrm-close.md). 最後に、サブユニット ドライバーの設定、 **OpenStruct**のメンバー、 **CommandData**開かれるストリームを記述する共用体。

この要求を送信するには、サブユニットの送信、 [ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)で IRP、 **IoControlCode** IRP のメンバーに設定[ **IOCTL\_AVCSTRM\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avcstrm/ni-avcstrm-ioctl_avcstrm_class)と **[引数 1]** IRP のメンバーに設定AVC\_ストリーム\_要求\_行われるようにオープン操作を記述するブロック構造体。

サブユニット ドライバーは、このコマンドが同期的に完了することができます。 保留中の操作なしですぐに結果が返され*avcstrm.sys*します。

この関数のコードは、IRQL で呼び出す必要があります = パッシブ\_レベル。

### <a name="see-also"></a>関連項目

[**AVC\_ストリーム\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avcstrm/ns-avcstrm-_avc_stream_request_block)、 [ **INIT\_AVCSTRM\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avcstrm/nf-avcstrm-init_avcstrm_header)、 [ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)、 [ **IOCTL\_AVCSTRM\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avcstrm/ni-avcstrm-ioctl_avcstrm_class)、 [ **AVCSTRM\_オープン\_構造体**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avcstrm/ns-avcstrm-_avcstrm_open_struct)、 [ **AVCSTRM\_関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avcstrm/ne-avcstrm-_avcstrm_function)、 [ **AVCSTRM\_形式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avcstrm/ne-avcstrm-_avcstrm_format)、 [ **AVCSTRM\_形式\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avcstrm/ns-avcstrm-_avcstrm_format_info)

 

 





