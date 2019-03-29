---
title: AVCSTRM\_設定\_状態
description: AVCSTRM\_設定\_状態
ms.assetid: 890ae8d1-d7e2-40a4-af7f-b6df32d845e4
keywords:
- AVCSTRM_SET_STATE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- AVCSTRM_SET_STATE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a33167243624d7ce144d3d449ea1ff3430ac987e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572832"
---
# <a name="avcstrmsetstate"></a>AVCSTRM\_設定\_状態


## <span id="ddk_avcstrm_set_state_ks"></span><span id="DDK_AVCSTRM_SET_STATE_KS"></span>


**AVCSTRM\_設定\_状態**関数コードでは、新しいストリームの状態に、指定したストリームが配置されます。

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
<td><p>IRP で指定されたパラメーターが正しくありません。</p></td>
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

この関数を使用して、 **StreamState**のメンバー、 **CommandData**共用体、AVC の\_ストリーム\_要求\_ブロック構造の下に示すようにします。

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

### <a name="requirements"></a>必要条件

**ヘッダー:** 宣言されている*avcstrm.h*します。 含める*avcstrm.h*します。

### <a name="span-idavcstreamrequestblockinputspanspan-idavcstreamrequestblockinputspanavcstreamrequestblock-input"></a><span id="avc_stream_request_block_input"></span><span id="AVC_STREAM_REQUEST_BLOCK_INPUT"></span>AVC\_ストリーム\_要求\_ブロックの入力

<span id="SizeOfThisBlock__Version_and_Function"></span><span id="sizeofthisblock__version_and_function"></span><span id="SIZEOFTHISBLOCK__VERSION_AND_FUNCTION"></span>**SizeOfThisBlock、バージョン、および関数**  
使用して、 [ **INIT\_AVCSTRM\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff560750)マクロをこれらのメンバーを初期化します。 渡す**AVCSTRM\_設定\_状態**マクロの要求の引数にします。

<span id="AVCStreamContext"></span><span id="avcstreamcontext"></span><span id="AVCSTREAMCONTEXT"></span>**AVCStreamContext**  
によって以前返されるストリームのコンテキスト (ハンドル) を示す**AVCSTRM\_オープン**を新しいストリーム状態への呼び出し。

<span id="StreamState"></span><span id="streamstate"></span><span id="STREAMSTATE"></span>**StreamState**  
ストリームを配置する新しいストリームの状態を指定します。

サブユニット ドライバーは IRP を割り当てる必要があります最初、 [ **AVC\_ストリーム\_要求\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff554194)構造体。 次に、使用する必要があります、 [ **INIT\_AVCSTRM\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff560750) 、AVC を初期化するためにマクロ\_ストリーム\_要求\_ブロック構造体渡す**AVCSTRM\_取得\_状態**マクロに要求の引数として。 次に、サブユニット ドライバーの設定、 **AVCStreamContext**からストリームの状態を取得する、ストリームのストリーム コンテキスト (ハンドル) のメンバー。

この要求を送信するには、サブユニットの送信、 [ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550766)で IRP、 **IoControlCode** IRP のメンバーに設定[ **IOCTL\_AVCSTRM\_クラス**](https://msdn.microsoft.com/library/windows/hardware/ff560778)と **[引数 1]** IRP のメンバーに設定AVC\_ストリーム\_要求\_新しいストリームの状態に格納するストリームを記述するブロック構造体。

サブユニット ドライバーは、同期的に完了するには、このコマンドが期待できます。 保留中の操作なしですぐに結果が返され*avcstrm.sys*します。

この関数のコードは、IRQL で呼び出す必要があります = パッシブ\_レベル。

### <a name="see-also"></a>関連項目

[**AVC\_ストリーム\_要求\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff554194)、 [ **INIT\_AVCSTRM\_ヘッダー**](https://msdn.microsoft.com/library/windows/hardware/ff560750)、 [ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550766)、 [ **IOCTL\_AVCSTRM\_クラス**](https://msdn.microsoft.com/library/windows/hardware/ff560778)、 [ **KSSTATE**](https://msdn.microsoft.com/library/windows/hardware/ff566856)、 [ **AVCSTRM\_関数**](https://msdn.microsoft.com/library/windows/hardware/ff554120)

 

 





