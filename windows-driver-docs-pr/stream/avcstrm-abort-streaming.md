---
title: AVCSTRM\_中止\_ストリーミング
description: AVCSTRM\_中止\_ストリーミング
ms.assetid: 9a136511-c838-456f-87c5-a4639be0c299
keywords:
- AVCSTRM_ABORT_STREAMING ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- AVCSTRM_ABORT_STREAMING
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1c45fb0e7a6e3154586e508f2dd5a2518d3754c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386721"
---
# <a name="avcstrmabortstreaming"></a>AVCSTRM\_中止\_ストリーミング


## <span id="ddk_avcstrm_abort_streaming_ks"></span><span id="DDK_AVCSTRM_ABORT_STREAMING_KS"></span>


**AVCSTRM\_中止\_ストリーミング**関数コードで取り消します*すべて*保留中のデータを要求し、使用されているリソースを解放します。

### <a name="io-status-block"></a>I/O ステータス ブロック

成功した場合、 *avcstrm.sys*設定**Irp -&gt;IoStatus.Status**ステータス\_成功します。

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

ただし、この機能をキャンセル*すべて*Irp をストリーミングします。 個々 の IRP をキャンセルするには、使用[ **IoCancelIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocancelirp)します。

そのターゲット デバイスを削除または IRP の元のデータがストリームの処理を停止する取り消されるときに、サブユニットでこれを呼び出す必要があります。

この関数はのすべてのメンバーを使用していない、 **CommandData**共用体、AVC の\_ストリーム\_要求\_ブロック構造体。

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

### <a name="requirements"></a>必要条件

**ヘッダー:** 宣言されている*avcstrm.h*します。 含める*avcstrm.h*します。

### <a name="span-idavcstreamrequestblockinputspanspan-idavcstreamrequestblockinputspanavcstreamrequestblock-input"></a><span id="avc_stream_request_block_input"></span><span id="AVC_STREAM_REQUEST_BLOCK_INPUT"></span>AVC\_ストリーム\_要求\_ブロックの入力

<span id="SizeOfThisBlock__Version_and_Function"></span><span id="sizeofthisblock__version_and_function"></span><span id="SIZEOFTHISBLOCK__VERSION_AND_FUNCTION"></span>**SizeOfThisBlock、バージョン、および関数**  
使用して、 [ **INIT\_AVCSTRM\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avcstrm/nf-avcstrm-init_avcstrm_header)マクロをこれらのメンバーを初期化します。 渡す**AVCSTRM\_中止\_ストリーミング**マクロの要求の引数にします。

<span id="AVCStreamContext"></span><span id="avcstreamcontext"></span><span id="AVCSTREAMCONTEXT"></span>**AVCStreamContext**  
によって以前返されるストリームのコンテキスト (ハンドル) を指定します**AVCSTRM\_オープン**データの書き込み操作について、ターゲットで呼び出すされています。

サブユニット ドライバーは IRP を割り当てる必要があります最初、 [ **AVC\_ストリーム\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avcstrm/ns-avcstrm-_avc_stream_request_block)構造体。 次に、使用する必要があります、 [ **INIT\_AVCSTRM\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avcstrm/nf-avcstrm-init_avcstrm_header) 、AVC を初期化するためにマクロ\_ストリーム\_要求\_ブロック構造体渡す**AVCSTRM\_読み取り**マクロに要求の引数として。 次に、サブユニット ドライバーの設定、 **AVCStreamContext**ストリーミングを中止するストリームのストリーム コンテキスト (ハンドル) のメンバー。

この要求を送信するには、サブユニットの送信、 [ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)で IRP、 **IoControlCode** IRP のメンバーに設定[ **IOCTL\_AVCSTRM\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avcstrm/ni-avcstrm-ioctl_avcstrm_class)と **[引数 1]** IRP のメンバーに設定AVC\_ストリーム\_要求\_ストリーミングを行う操作の中止を記述するブロック構造体。

この関数のコードはパッシブで呼び出す必要があります\_レベル。 ディスパッチで実行されることができる場合 IRP が取り消されているデータ、\_レベル。 ここでは、サブユニットが作業項目を起動して、パッシブで実行されている項目で日常的な作業でこの関数を呼び出す必要があります\_レベル。

### <a name="see-also"></a>関連項目

[**INIT\_AVCSTRM\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avcstrm/nf-avcstrm-init_avcstrm_header)、 [ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)、 [ **IOCTL\_AVCSTRM\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avcstrm/ni-avcstrm-ioctl_avcstrm_class)、 [ **AVCSTRM\_関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avcstrm/ne-avcstrm-_avcstrm_function)

 

 





