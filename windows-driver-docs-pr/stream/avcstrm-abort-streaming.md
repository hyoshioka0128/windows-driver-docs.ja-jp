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
ms.openlocfilehash: 8d5bd3091accebe678cf577eb54761bdb78790ec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572541"
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

ただし、この機能をキャンセル*すべて*Irp をストリーミングします。 個々 の IRP をキャンセルするには、使用[ **IoCancelIrp**](https://msdn.microsoft.com/library/windows/hardware/ff548338)します。

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
使用して、 [ **INIT\_AVCSTRM\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff560750)マクロをこれらのメンバーを初期化します。 渡す**AVCSTRM\_中止\_ストリーミング**マクロの要求の引数にします。

<span id="AVCStreamContext"></span><span id="avcstreamcontext"></span><span id="AVCSTREAMCONTEXT"></span>**AVCStreamContext**  
によって以前返されるストリームのコンテキスト (ハンドル) を指定します**AVCSTRM\_オープン**データの書き込み操作について、ターゲットで呼び出すされています。

サブユニット ドライバーは IRP を割り当てる必要があります最初、 [ **AVC\_ストリーム\_要求\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff554194)構造体。 次に、使用する必要があります、 [ **INIT\_AVCSTRM\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff560750) 、AVC を初期化するためにマクロ\_ストリーム\_要求\_ブロック構造体渡す**AVCSTRM\_読み取り**マクロに要求の引数として。 次に、サブユニット ドライバーの設定、 **AVCStreamContext**ストリーミングを中止するストリームのストリーム コンテキスト (ハンドル) のメンバー。

この要求を送信するには、サブユニットの送信、 [ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550766)で IRP、 **IoControlCode** IRP のメンバーに設定[ **IOCTL\_AVCSTRM\_クラス**](https://msdn.microsoft.com/library/windows/hardware/ff560778)と **[引数 1]** IRP のメンバーに設定AVC\_ストリーム\_要求\_ストリーミングを行う操作の中止を記述するブロック構造体。

この関数のコードはパッシブで呼び出す必要があります\_レベル。 ディスパッチで実行されることができる場合 IRP が取り消されているデータ、\_レベル。 ここでは、サブユニットが作業項目を起動して、パッシブで実行されている項目で日常的な作業でこの関数を呼び出す必要があります\_レベル。

### <a name="see-also"></a>関連項目

[**INIT\_AVCSTRM\_ヘッダー**](https://msdn.microsoft.com/library/windows/hardware/ff560750)、 [ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550766)、 [ **IOCTL\_AVCSTRM\_クラス**](https://msdn.microsoft.com/library/windows/hardware/ff560778)、 [ **AVCSTRM\_関数**](https://msdn.microsoft.com/library/windows/hardware/ff554120)

 

 





