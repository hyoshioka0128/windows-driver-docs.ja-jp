---
title: AVCSTRM\_閉じる
description: AVCSTRM\_閉じる
ms.assetid: 2487ba06-3577-409e-ba82-f9a0d3453c5d
keywords:
- AVCSTRM_CLOSE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- AVCSTRM_CLOSE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52004cbcd496b68237d120594e7ec038ca6f8004
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371842"
---
# <a name="avcstrmclose"></a>AVCSTRM\_閉じる


## <span id="ddk_avcstrm_close_ks"></span><span id="DDK_AVCSTRM_CLOSE_KS"></span>


**AVCSTRM\_閉じる**関数コードが、指定したストリームを閉じるし、AVCSTRM に割り当てられたリソースを解放\_開きます。

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

この関数を使用して、 **AVCStreamContext**のメンバー、 **CommandData**共用体、AVC の\_ストリーム\_要求\_ブロック構造の下に示すようにします。

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
使用して、 [ **INIT\_AVCSTRM\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff560750)マクロをこれらのメンバーを初期化します。 渡す**AVCSTRM\_閉じる**マクロの要求の引数にします。

<span id="AVCStreamContext"></span><span id="avcstreamcontext"></span><span id="AVCSTREAMCONTEXT"></span>**AVCStreamContext**  
閉じるストリームのストリーム コンテキスト (ハンドル) を指定します。 場合**AVCSTRM\_閉じる**この値が無効になって、正常に返されます。

閉じるストリームを指定する方法の例を次に示します。

```cpp
    pAVCStrmReq = &amp;pStrmExt->AVCStrmReq;
    RtlZeroMemory(pAVCStrmReq, sizeof(AVC_STREAM_REQUEST_BLOCK));
    INIT_AVCSTRM_HEADER(pAVCStrmReq, AVCSTRM_CLOSE);

    pAVCStrmReq->AVCStreamContext = pStrmExt->AVCStreamContext;

    Status = 
        AVCStrmReqSubmitIrpSynch ( 
            pDevExt->pBusDeviceObject,
            pStrmExt->pIrpReq,
            pAVCStrmReq
            );
```

サブユニット ドライバーは IRP を割り当てる必要があります最初、 [ **AVC\_ストリーム\_要求\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff554194)構造体。 次に、使用する必要があります、 [ **INIT\_AVCSTRM\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff560750) 、AVC を初期化するためにマクロ\_ストリーム\_要求\_ブロック構造体渡す**AVCSTRM\_閉じる**マクロに要求の引数として。 次に、サブユニット ドライバーの設定、 **AVCStreamContext**閉じるストリームのメンバー。

この要求を送信するには、サブユニットの送信、 [ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550766)で IRP、 **IoControlCode** IRP のメンバーに設定[ **IOCTL\_AVCSTRM\_クラス**](https://msdn.microsoft.com/library/windows/hardware/ff560778)と **[引数 1]** IRP のメンバーに設定AVC\_ストリーム\_要求\_行われるように、閉じる操作を記述するブロック構造体。

サブユニット ドライバーは、このコマンドが同期的に完了することができます。 保留中の操作なしですぐに結果が返され*avcstrm.sys*します。

この関数のコードは、IRQL で呼び出す必要があります = パッシブ\_レベル。

### <a name="see-also"></a>関連項目

[**AVC\_ストリーム\_要求\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff554194)、 [ **INIT\_AVCSTRM\_ヘッダー**](https://msdn.microsoft.com/library/windows/hardware/ff560750)、 [ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550766)、 [ **IOCTL\_AVCSTRM\_クラス**](https://msdn.microsoft.com/library/windows/hardware/ff560778)、 [ **AVCSTRM\_関数**](https://msdn.microsoft.com/library/windows/hardware/ff554120)

 

 





