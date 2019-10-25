---
title: AVCSTRM\_ABORT\_STREAMING
description: AVCSTRM\_ABORT\_STREAMING
ms.assetid: 9a136511-c838-456f-87c5-a4639be0c299
keywords:
- AVCSTRM_ABORT_STREAMING ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- AVCSTRM_ABORT_STREAMING
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e07c2e1bdb4e16521918b4841bea9fc53846aad0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845068"
---
# <a name="avcstrm_abort_streaming"></a>AVCSTRM\_ABORT\_STREAMING


## <span id="ddk_avcstrm_abort_streaming_ks"></span><span id="DDK_AVCSTRM_ABORT_STREAMING_KS"></span>


**Avcstrm\_ABORT\_STREAMING**関数のコードは、保留中の*すべて*のデータ要求をキャンセルし、使用されたリソースを解放します。

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

この機能は、*すべて*のストリーミング irp をキャンセルします。 個々の IRP をキャンセルするには、 [**Iocancelirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp)を使用します。

サブユニットは、ターゲットデバイスが削除されたとき、またはストリーム操作を停止するために元のデータ IRP が取り消されたときに、これを呼び出す必要があります。

この関数では、AVC\_ストリームの**Commanddata**共用体のいずれのメンバーも、要求\_ブロック構造\_使用されません。

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
} AVC_STREAM_REQUEST_BLOCK, *PAVC_STREAM_REQUEST_BLOCK;
```

### <a name="requirements"></a>要件

**ヘッダー:** *Avcstrm .h*で宣言されています。 *Avcstrm .h*をインクルードします。

### <a name="span-idavc_stream_request_block_inputspanspan-idavc_stream_request_block_inputspanavc_stream_request_block-input"></a><span id="avc_stream_request_block_input"></span><span id="AVC_STREAM_REQUEST_BLOCK_INPUT"></span>\_ストリーム\_要求\_入力をブロックします。

<span id="SizeOfThisBlock__Version_and_Function"></span><span id="sizeofthisblock__version_and_function"></span><span id="SIZEOFTHISBLOCK__VERSION_AND_FUNCTION"></span>**SizeOfThisBlock、バージョン、および関数**  
[**INIT\_AVCSTRM\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/nf-avcstrm-init_avcstrm_header)マクロを使用して、これらのメンバーを初期化します。 マクロの要求引数に**Avcstrm\_ABORT\_STREAMING**を渡します。

<span id="AVCStreamContext"></span><span id="avcstreamcontext"></span><span id="AVCSTREAMCONTEXT"></span>**AVCStreamContext**  
データ書き込み操作の対象となる、以前の**Avcstrm\_オープン**呼び出しによって返されるストリームコンテキスト (ハンドル) を指定します。

サブユニットドライバーは、まず IRP と[**AVC\_ストリーム\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_avc_stream_request_block)構造に割り当てる必要があります。 次に、 [**INIT\_avcstrm\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/nf-avcstrm-init_avcstrm_header)マクロを使用して、AVC\_\_ストリームを初期化し\_ブロック構造を初期化し、 **avcstrm\_** を request 引数としてマクロに渡します。 次に、サブユニットドライバーは**Avcstreamcontext**メンバーをストリームのストリームコンテキスト (handle) に設定し、ストリーミングを中止します。

この要求を送信するために、サブユニットは irp [ **\_MJ\_内部\_\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)に送信します。 Irp の**iocontrolcode**メンバーを[**IOCTL\_AVCSTRM\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ni-avcstrm-ioctl_avcstrm_class)および引数1に設定します。実行する abort ストリーミング操作を記述する\_要求\_ブロック構造に設定されている IRP\_ストリームに設定されている IRP のメンバー。

この関数コードは、パッシブ\_レベルで呼び出す必要があります。 データ IRP が取り消されると、ディスパッチ\_レベルで実行できるようになります。 この場合、サブユニットは作業項目を開始し、その作業項目のルーチンでこの関数を呼び出す必要があります。この関数は、パッシブ\_レベルで実行されます。

### <a name="see-also"></a>参照

[**INIT\_avcstrm\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/nf-avcstrm-init_avcstrm_header)、 [**IRP\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)、 [**IOCTL\_AVCSTRM\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ni-avcstrm-ioctl_avcstrm_class)、 [**avcstrm\_関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ne-avcstrm-_avcstrm_function)

 

 





