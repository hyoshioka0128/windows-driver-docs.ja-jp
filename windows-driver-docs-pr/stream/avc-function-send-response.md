---
title: '\_応答を送信\_AVC\_関数'
description: '\_応答を送信\_AVC\_関数'
ms.assetid: f04caed8-8521-4dfa-9bfa-cf71ec7a658e
keywords:
- AVC_FUNCTION_SEND_RESPONSE ストリーミングメディアデバイス
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
ms.openlocfilehash: 7a0dbd6069705f0e05b9d1a465f635f634150a35
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845071"
---
# <a name="avc_function_send_response"></a>\_応答を送信\_AVC\_関数


## <span id="ddk_avc_function_send_response_ks"></span><span id="DDK_AVC_FUNCTION_SEND_RESPONSE_KS"></span>


**\_応答関数コード\_送信する AVC\_関数**は、AV/C ユニットおよびサブユニットの要求に応答するために使用されます。

### <a name="io-status-block"></a>I/O ステータス ブロック

正常に実行された場合は、AV/C プロトコルドライバーによって、 **Irp&gt;iostatus. status**が次のいずれかに設定されている可能性があります。

元の要求以降に1つ以上のバスのリセットが原因で応答が破棄された場合の状態\_成功

応答が*61883*に正常に配信された場合 (要求イニシエーターへの配信が成功したことを意味します)、状態\_保留中です。

その他の戻り値には次のようなものがあります。

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
<td><p>内部バッファーの割り当てに失敗しました。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idheadersspanspan-idheadersspanheaders"></a><span id="headers"></span><span id="HEADERS"></span>ヘッダー

### <a name="comments"></a>コメント

この関数では、次に示すように、AVC\_コマンド\_IRB 構造体を使用します。

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

### <a name="span-idavc_command_irb_inputspanspan-idavc_command_irb_inputspanavc_command_irb-input"></a><span id="avc_command_irb_input"></span><span id="AVC_COMMAND_IRB_INPUT"></span>AVC\_コマンド\_IRB 入力

**的**  
このメンバーの**関数**submember は、AVC\_関数列挙から **\_応答を送信\_には、avc\_関数**に設定されている必要があります。

<span id="SubunitAddrFlag"></span><span id="subunitaddrflag"></span><span id="SUBUNITADDRFLAG"></span>**SubunitAddrFlag**  
は、 **AVC\_関数**から取得した値に設定し、\_要求の完了\_取得します。

<span id="AlternateOpcodesFlag"></span><span id="alternateopcodesflag"></span><span id="ALTERNATEOPCODESFLAG"></span>**Alternateopのフラグ**  
無効.

<span id="TimeoutFlag"></span><span id="timeoutflag"></span><span id="TIMEOUTFLAG"></span>**TimeoutFlag**  
無効.

<span id="RetryFlag"></span><span id="retryflag"></span><span id="RETRYFLAG"></span>**RetryFlag**  
無効.

<span id="CommandType"></span><span id="commandtype"></span><span id="COMMANDTYPE"></span>**CommandType**  
応答では無視されます。

<span id="ResponseCode"></span><span id="responsecode"></span><span id="RESPONSECODE"></span>**ResponseCode**  
このメンバーは、 **AvcResponseCode**列挙体のいずれかの値に設定する必要があります。

<span id="SubunitAddr"></span><span id="subunitaddr"></span><span id="SUBUNITADDR"></span>**SubunitAddr**  
は、 **AVC\_関数**から取得した値に設定し、\_要求の完了\_取得します。

<span id="AlternateOpcodes"></span><span id="alternateopcodes"></span><span id="ALTERNATEOPCODES"></span>**AlternateOpcodes**  
無効.

<span id="Timeout"></span><span id="timeout"></span><span id="TIMEOUT"></span>**タイムアウト**  
無効.

<span id="Retries"></span><span id="retries"></span><span id="RETRIES"></span>**試行**  
無効.

<span id="Opcode"></span><span id="opcode"></span><span id="OPCODE"></span>**オペコード**  
これには、応答に適した AV/C ユニットオペコードが含まれている必要があります (元の要求で提供されたオペコードとは異なる場合があります)。

<span id="OperandLength"></span><span id="operandlength"></span><span id="OPERANDLENGTH"></span>**オペレーティング Andlength**  
応答のオペランドリストのバイト数に設定します。

<span id="Operands"></span><span id="operands"></span><span id="OPERANDS"></span>**オペランド**  
応答のオペランドリスト。

<span id="NodeAddress"></span><span id="nodeaddress"></span><span id="NODEADDRESS"></span>**NodeAddress**  
元の要求のソースのノードアドレス。

<span id="Generation"></span><span id="generation"></span><span id="GENERATION"></span>**Generation**  
元の要求から取得された生成 ID。

\_AVC\_クラスデバイスインターフェイスの GUID のコンテキストでは、 **avc\_関数\_送信\_応答**関数コードを使用して、AV/C ユニット要求にのみ応答します。

Avc の仮想インスタンス (つまり、GUID\_VIRTUAL\_AVC\_クラスのデバイスインターフェイスを登録するインスタンス) の場合、 **avc\_関数\_送信\_応答**関数コードが使用され*ます。* AV/C ユニット*および*サブユニット要求に応答します。

最初の応答で、( **AvcResponseType**列挙からの) 中間応答コード **\_の AVC\_応答**を使用する場合は、フォローアップ処理が必要です。 **AVC\_関数**の完了によって取得された**Nodeaddress**および**Generation**メンバーは\_要求元の関数\_取得するために、後続の応答で使用する必要があります。 どのような場合でも、次の**avc\_関数\_GET\_REQUEST**関数\_から返される前に、 **\_応答**の完了ルーチンを送信する前に送信する必要があります。要求を受信できます。

この構造体の使用を推奨するには、元の要求の内容を使用し、応答に応じて**オペコード**、**演算子**、およびオペランドのメンバーを更新します。

この関数コードは、IRQL &lt;= ディスパッチ\_レベルで呼び出すことができます。

### <a name="see-also"></a>参照

[**Avc\_関数\_\_REQUEST**](avc-function-get-request.md)、 [**AvcResponseCode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavcresponsecode)、 [**AVC\_関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)を取得します。

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
<td>Avc. h (Avc を含む)</td>
</tr>
</tbody>
</table>

 

 





