---
title: AVC\_関数\_\_要求を取得します
description: AVC\_関数\_\_要求を取得します
ms.assetid: b29df7a8-782b-4014-b47e-7cf917f8e99d
keywords:
- AVC_FUNCTION_GET_REQUEST ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- AVC_FUNCTION_GET_REQUEST
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 808b4220dfeaa1aba8a930d23fc16fa30224b67a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845081"
---
# <a name="avc_function_get_request"></a>AVC\_関数\_\_要求を取得します


## <span id="ddk_avc_function_get_request_ks"></span><span id="DDK_AVC_FUNCTION_GET_REQUEST_KS"></span>


\_要求関数コード\_取得するために、 **AVC\_関数**を使用して、AV/C ユニットおよびサブユニットの要求を受信するように登録します。

### <a name="io-status-block"></a>I/O ステータス ブロック

この関数は常に **、Irp&gt;iostatus**を状態\_保留中に設定します。

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

### <a name="requirements"></a>要件

**ヘッダー:** *Avc*で宣言されています。 *Avc. h*を含めます。

### <a name="span-idavc_command_irb_inputspanspan-idavc_command_irb_inputspanavc_command_irb-input"></a><span id="avc_command_irb_input"></span><span id="AVC_COMMAND_IRB_INPUT"></span>AVC\_コマンド\_IRB 入力

**的**  
このメンバーの**関数**submember は、AVC\_関数列挙からの **\_要求\_、avc\_関数**に設定されている必要があります。

<span id="SubunitAddrFlag"></span><span id="subunitaddrflag"></span><span id="SUBUNITADDRFLAG"></span>**SubunitAddrFlag**  
受信単位コマンドに登録するときにのみ使用されます。 これを1に設定し、 **Subunitaddr**パラメーターに単位アドレスを指定します。 サブユニットの要求では、完了時には1に設定され、 **Subunitaddr**パラメーターはこの仮想サブユニットインスタンスのサブユニットアドレスを含むメモリを指します。 呼び出し元はこの非ページメモリにアクセスできますが、解放を試みることはできません。

<span id="AlternateOpcodesFlag"></span><span id="alternateopcodesflag"></span><span id="ALTERNATEOPCODESFLAG"></span>**Alternateopのフラグ**  
受信単位コマンドに登録するときにのみ使用されます。 これを1に設定し、 **alternateopcodes**パラメーターで呼び出し元によってサポートされるオペコードの一覧を提供します。

<span id="TimeoutFlag"></span><span id="timeoutflag"></span><span id="TIMEOUTFLAG"></span>**TimeoutFlag**  
無効.

<span id="RetryFlag"></span><span id="retryflag"></span><span id="RETRYFLAG"></span>**RetryFlag**  
無効.

<span id="CommandType"></span><span id="commandtype"></span><span id="COMMANDTYPE"></span>**CommandType**  
入力では無視されます。 出力時に、 **CommandType**メンバーは**avccommandtype**列挙子のいずれかの値に設定されます。

<span id="ResponseCode"></span><span id="responsecode"></span><span id="RESPONSECODE"></span>**ResponseCode**  
要求では無視されます。

<span id="SubunitAddr"></span><span id="subunitaddr"></span><span id="SUBUNITADDR"></span>**SubunitAddr**  
受信単位コマンドに登録するときにのみ使用されます。 これを、 **AV/C**デジタルインターフェイスコマンドセットの全般仕様 (リビジョン 3.0 (0xff)) の5.3.3 セクションに従ってエンコードされたユニットアドレスを含む非ページメモリのアドレスに設定します。 この仕様は、 [1394 貿易 Association](https://go.microsoft.com/fwlink/p/?linkid=8728) web サイトにあります。 サブユニット要求の場合、これは、この仮想サブユニットインスタンスのサブユニットアドレスを含むメモリを指します。 呼び出し元はこの非ページメモリにアクセスできますが、解放を試みることはできません。

<span id="AlternateOpcodes"></span><span id="alternateopcodes"></span><span id="ALTERNATEOPCODES"></span>**AlternateOpcodes**  
受信単位コマンドに登録するときにのみ使用されます。 これを、呼び出し元によってサポートされる単体オペコードのリストを含む非ページメモリのアドレスに設定します。 オペコードリストの最初のバイトは、後に続くオペコードの数です (バイト数と同じです)。 代替オペコードリストを含むメモリの合計の長さは、 **alternateopcodes**\[0\]+ 1 です。

<span id="Timeout"></span><span id="timeout"></span><span id="TIMEOUT"></span>**タイムアウト**  
無効.

<span id="Retries"></span><span id="retries"></span><span id="RETRIES"></span>**試行**  
無効.

<span id="Opcode"></span><span id="opcode"></span><span id="OPCODE"></span>**オペコード**  
入力時には無視されます。 出力時に、これには AV/C ユニットオペコードが含まれています。 これは、 **Alternateopcodes**によって指定されたオペコードの1つです。

<span id="OperandLength"></span><span id="operandlength"></span><span id="OPERANDLENGTH"></span>**オペレーティング Andlength**  
入力時には無視されます。 出力時には、要求で使用されるオペランドリストのバイト数に設定されます。

<span id="Operands"></span><span id="operands"></span><span id="OPERANDS"></span>**オペランド**  
入力時には無視されます。 出力時に、このパラメーターには、要求のオペランドリストが含まれます。

<span id="NodeAddress"></span><span id="nodeaddress"></span><span id="NODEADDRESS"></span>**NodeAddress**  
入力時には無視されます。 出力時には、要求の送信元のノードアドレスに設定されます。 このパラメーターは、応答を送信するときに使用されます (詳細については、「 [**AVC\_関数\_送信\_応答**](avc-function-send-response.md))」を参照してください。

<span id="Generation"></span><span id="generation"></span><span id="GENERATION"></span>**Generation**  
入力時には無視されます。 出力時には、ノードアドレスが有効と見なされたときに、このが強制的に生成されます。 このパラメーターは、応答を送信するときに使用されます (詳細については、「 [**AVC\_関数\_送信\_応答**](avc-function-send-response.md))」を参照してください。

\_AVC\_クラスデバイスインターフェイスの GUID のコンテキストでは、 **avc\_関数\_GET\_** 要求関数コードを使用して、AV/C ユニット要求のみを受信するように登録します (サブユニット要求ではありません)。 通常、この関数は、( *avc* FDO の) 上位フィルタードライバーによって、ピアデバイス機能をサポートするために使用されます (つまり、非仮想スタックからターゲットデバイスからのユニット要求を処理します)。 サブユニットドライバーがユニット要求を処理するために登録することはできませんが、同じユニットオペコードをサポートするために登録されているサブユニットドライバーインスタンスは、互いに連携して状態情報を共有する必要があります。 *Avc*は、同じユニットオペコードに対して複数の登録を直接サポートしていません。

この関数では、AVC\_コマンド\_IRB 構造体を使用します。 この構造体は、AV/C コマンド要求の共通コンポーネントを定義します。 有効な入力パラメーターは、 **Subunitaddrflag**、 **alternateopのフラグ**、 **Alternateオペコード**、および**subunitaddr**だけです。すべてが必要です。 **Alternateopcodes**は、呼び出し元によってサポートされる単体オペコードのリストを格納しているバッファーを指す必要があります。 **Subunitaddr**は、ユニットアドレス (0xff) を含むバッファーを指している必要があります。

Avc の仮想インスタンス (つまり、GUID\_VIRTUAL\_AVC\_クラスのデバイスインターフェイス) のインスタンスの場合、 **avc\_関数\_GET\_要求**を使用して、AV/C を受信するように登録し*ます。* ユニットおよびサブユニットの要求。 上位フィルタードライバー (FDO) は、通常、ユニット要求を処理するために登録さ*れますが*、サブユニットドライバーは、特定の種類のサブユニットの要求を処理するように登録します。 サブユニットドライバーがユニット要求を処理するために登録することはできませんが、同じユニットオペコードをサポートするために登録されているサブユニットドライバーインスタンスは、互いに連携して状態情報を共有する必要があります。 *Avc*は、同じユニットオペコードに対して複数の登録を直接サポートしていません。

サブユニットドライバーは、サブユニット固有の要求を受信するために登録するときに、入力パラメーターを設定しません。

この関数は常にステータス\_を返します。そのため、すべての処理を完了ルーチンで実行する必要があります。 完了時に、AVC\_コマンド\_IRB 構造体は、要求のオペコードとオペランドを保持します。 AV/C プロトコルでは、100ミリ秒内で応答を送信する必要があります。 これを行うには、 **AVC\_関数\_SEND\_RESPONSE**関数を使用して、完了ルーチンから行うことができます。

最初の応答で、( **AvcResponseType**列挙からの) 中間応答コード **\_の AVC\_応答**を使用する場合は、フォローアップ処理が必要です。 **AVC\_関数**の完了によって取得された**Nodeaddress**および**Generation**メンバーは\_要求元の関数\_取得するために、後続の応答で使用する必要があります。 どのような場合でも、次の**avc\_関数\_GET\_REQUEST**関数\_から返される前に、 **\_応答**の完了ルーチンを送信する前に送信する必要があります。要求を受信できます。

この構造体の使用を推奨するには、最初に構造体をゼロにしてから ( **Rtlzero memory**を使用して)、パラメーターを入力します。

この関数コードは、IRQL &lt;= ディスパッチ\_レベルで呼び出すことができます。

### <a name="see-also"></a>参照

\_RESPONSE、 [**AvcResponseCode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavcresponsecode)、 [**avc\_関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)、 [**RTLゼロメモリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlzeromemory)を[**送信する AVC\_関数\_** ](avc-function-send-response.md)

 

 





