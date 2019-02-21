---
title: AVC\_関数\_送信\_応答
description: AVC\_関数\_送信\_応答
ms.assetid: f04caed8-8521-4dfa-9bfa-cf71ec7a658e
keywords:
- AVC_FUNCTION_SEND_RESPONSE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- AVC_FUNCTION_SEND_RESPONSE
api_location:
- avc.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e9b95a36e7703f247eaee1bb02f7e8168b42384
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528347"
---
# <a name="avcfunctionsendresponse"></a>AVC\_関数\_送信\_応答


## <span id="ddk_avc_function_send_response_ks"></span><span id="DDK_AVC_FUNCTION_SEND_RESPONSE_KS"></span>


**AVC\_関数\_送信\_応答**AV/C 単体テストとサブユニット要求に応答する関数のコードを使用します。

### <a name="io-status-block"></a>I/O ステータス ブロック

成功すると、AV/C プロトコル ドライバー設定可能性があります**Irp -&gt;IoStatus.Status**いずれかに。

ステータス\_成功の場合は、応答が 1 つまたは複数のバスのため破棄を元の要求以降リセットまたは

ステータス\_PENDING 場合に、応答が正常に配信*61883.sys* (要求の発信側に正常に配信を意味します)。

その他の戻り値には、考えられる。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>戻り値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>STATUS_INSUFFICIENT_RESOURCES</p></td>
<td><p>内部バッファーを割り当てられませんでした。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idheadersspanspan-idheadersspanheaders"></a><span id="headers"></span><span id="HEADERS"></span>ヘッダー

### <a name="comments"></a>コメント

この関数は、AVC\_コマンド\_IRB 構造の下に示すようにします。

```cpp
typedef struct _AVC_COMMAND_IRB {
  AVC_IRB  Common;
  UCHAR  SubunitAddrFlag : 1;
  UCHAR  AlternateOpcodesFlag : 1;
  UCHAR  TimeoutFlag : 1;
  UCHAR  RetryFlag : 1;
  union {
    UCHAR  CommandType;
    UCHAR  ResponseCode;
  };
  PUCHAR  SubunitAddr;
  PUCHAR  AlternateOpcodes;
  LARGE_INTEGER  Timeout;
  UCHAR  Retries;
  UCHAR  Opcode;
  ULONG  OperandLength;
  UCHAR  Operands[MAX_AVC_OPERAND_BYTES];
  NODE_ADDRESS  NodeAddress;
  ULONG  Generation;
} AVC_COMMAND_IRB, *PAVC_COMMAND_IRB;
```

### <a name="span-idavccommandirbinputspanspan-idavccommandirbinputspanavccommandirb-input"></a><span id="avc_command_irb_input"></span><span id="AVC_COMMAND_IRB_INPUT"></span>AVC\_コマンド\_IRB 入力

**一般的です**  
**関数**にこのメンバーのサブメンバーを設定する必要があります**AVC\_関数\_送信\_応答**、AVC から\_関数の列挙体。

<span id="SubunitAddrFlag"></span><span id="subunitaddrflag"></span><span id="SUBUNITADDRFLAG"></span>**SubunitAddrFlag**  
取得した値に設定、 **AVC\_関数\_取得\_要求**完了します。

<span id="AlternateOpcodesFlag"></span><span id="alternateopcodesflag"></span><span id="ALTERNATEOPCODESFLAG"></span>**AlternateOpcodesFlag**  
無視されます。

<span id="TimeoutFlag"></span><span id="timeoutflag"></span><span id="TIMEOUTFLAG"></span>**TimeoutFlag**  
無視されます。

<span id="RetryFlag"></span><span id="retryflag"></span><span id="RETRYFLAG"></span>**RetryFlag**  
無視されます。

<span id="CommandType"></span><span id="commandtype"></span><span id="COMMANDTYPE"></span>**CommandType**  
応答は無視されます。

<span id="ResponseCode"></span><span id="responsecode"></span><span id="RESPONSECODE"></span>**ResponseCode**  
このメンバーから値のいずれかに設定する必要があります、 **AvcResponseCode**列挙体。

<span id="SubunitAddr"></span><span id="subunitaddr"></span><span id="SUBUNITADDR"></span>**SubunitAddr**  
取得した値に設定、 **AVC\_関数\_取得\_要求**完了します。

<span id="AlternateOpcodes"></span><span id="alternateopcodes"></span><span id="ALTERNATEOPCODES"></span>**AlternateOpcodes**  
無視されます。

<span id="Timeout"></span><span id="timeout"></span><span id="TIMEOUT"></span>**タイムアウト**  
無視されます。

<span id="Retries"></span><span id="retries"></span><span id="RETRIES"></span>**再試行**  
無視されます。

<span id="Opcode"></span><span id="opcode"></span><span id="OPCODE"></span>**オペコード**  
これは、(元の要求で指定されたオペコードとは異なる場合があります) の応答を適切な AV/C 単位のオペコードを含める必要があります。

<span id="OperandLength"></span><span id="operandlength"></span><span id="OPERANDLENGTH"></span>**OperandLength**  
応答のオペランドのリスト内のバイト数を設定します。

<span id="Operands"></span><span id="operands"></span><span id="OPERANDS"></span>**オペランド**  
応答のオペランドの一覧。

<span id="NodeAddress"></span><span id="nodeaddress"></span><span id="NODEADDRESS"></span>**NodeAddress**  
元の要求のソースのノードのアドレス。

<span id="Generation"></span><span id="generation"></span><span id="GENERATION"></span>**生成**  
生成 ID は、元の要求から取得します。

GUID のコンテキストで\_AVC\_クラス デバイスのインターフェイス、 **AVC\_関数\_送信\_応答**AV/C 単位の要求のみに対応する関数のコードを使用します。

仮想インスタンスの場合*avc.sys* (つまり、GUID 登録インスタンス\_仮想\_AVC\_クラス デバイス インターフェイス)、 **AVC\_関数\_送信\_応答**AV/C 単位に応答する関数コードが使用される*と*サブユニット要求。

最初の応答で使用する場合、 **AVC\_応答\_中間**応答コード (から、 **AvcResponseType**列挙型)、フォロー アップ処理が必要です。 **NodeAddress**と**生成**メンバー、取得、完了した、 **AVC\_関数\_取得\_要求**その後の応答では、元の関数を使用する必要があります。 次の場合も、 **AVC\_関数\_取得\_要求**関数は、最初から戻る前に送信する必要があります**AVC\_関数\_送信\_応答**完了ルーチンの場合は、次の単位の要求を受信する可能性がありますようにします。

この構造体の推奨される使用は、元の要求の内容を使用して、更新、**オペコード**、 **OperandLength**、および**オペランド**に応じて適切なメンバー応答です。

この関数のコードは、IRQL で呼び出すことができます&lt;= ディスパッチ\_レベル。

### <a name="see-also"></a>参照

[**AVC\_FUNCTION\_GET\_REQUEST**](avc-function-get-request.md), [**AvcResponseCode**](https://msdn.microsoft.com/library/windows/hardware/ff554105), [**AVC\_FUNCTION**](https://msdn.microsoft.com/library/windows/hardware/ff554145)

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Avc.h (include Avc.h)</td>
</tr>
</tbody>
</table>

 

 





