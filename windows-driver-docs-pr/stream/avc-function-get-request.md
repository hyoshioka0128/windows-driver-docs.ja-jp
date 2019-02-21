---
title: AVC\_関数\_取得\_要求
description: AVC\_関数\_取得\_要求
ms.assetid: b29df7a8-782b-4014-b47e-7cf917f8e99d
keywords:
- AVC_FUNCTION_GET_REQUEST ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- AVC_FUNCTION_GET_REQUEST
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa191f6b7b0b54c562d6aecf2769d0961aeda4ae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549216"
---
# <a name="avcfunctiongetrequest"></a>AVC\_関数\_取得\_要求


## <span id="ddk_avc_function_get_request_ks"></span><span id="DDK_AVC_FUNCTION_GET_REQUEST_KS"></span>


**AVC\_関数\_取得\_要求**AV/C 単体テストとサブユニット要求を受信登録に関数コードを使用します。

### <a name="io-status-block"></a>I/O ステータス ブロック

この関数は常に設定**Irp -&gt;IoStatus.Status**ステータス\_保留します。

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

### <a name="requirements"></a>要件

**ヘッダー:** 宣言されている*avc.h*します。 含める*avc.h*します。

### <a name="span-idavccommandirbinputspanspan-idavccommandirbinputspanavccommandirb-input"></a><span id="avc_command_irb_input"></span><span id="AVC_COMMAND_IRB_INPUT"></span>AVC\_コマンド\_IRB 入力

**一般的です**  
**関数**にこのメンバーのサブメンバーを設定する必要があります**AVC\_関数\_取得\_要求**、AVC から\_関数の列挙体。

<span id="SubunitAddrFlag"></span><span id="subunitaddrflag"></span><span id="SUBUNITADDRFLAG"></span>**SubunitAddrFlag**  
単体のコマンドを受信登録するときにのみを使用します。 この設定を 1 に単位のアドレスを指定し、 **SubunitAddr**パラメーター。 サブユニットの要求の完了時にこれに設定されている、1 に注意してください、 **SubunitAddr**パラメーターがこの仮想サブユニット インスタンスのサブユニット アドレスを格納しているメモリをポイントします。 呼び出し元はこの非ページ メモリにアクセスできますが、解放する必要がありますしません。

<span id="AlternateOpcodesFlag"></span><span id="alternateopcodesflag"></span><span id="ALTERNATEOPCODESFLAG"></span>**AlternateOpcodesFlag**  
単体のコマンドを受信登録するときにのみを使用します。 この設定を 1 で呼び出し元でサポートされているオペコードの一覧を提供し、 **AlternateOpcodes**パラメーター。

<span id="TimeoutFlag"></span><span id="timeoutflag"></span><span id="TIMEOUTFLAG"></span>**TimeoutFlag**  
無視されます。

<span id="RetryFlag"></span><span id="retryflag"></span><span id="RETRYFLAG"></span>**RetryFlag**  
無視されます。

<span id="CommandType"></span><span id="commandtype"></span><span id="COMMANDTYPE"></span>**CommandType**  
入力では無視されます。 出力では、 **CommandType**メンバーから値のいずれかに設定されます、 **AvcCommandType**列挙体。

<span id="ResponseCode"></span><span id="responsecode"></span><span id="RESPONSECODE"></span>**ResponseCode**  
要求は無視されます。

<span id="SubunitAddr"></span><span id="subunitaddr"></span><span id="SUBUNITADDR"></span>**SubunitAddr**  
単体のコマンドを受信登録するときにのみを使用します。 これのセクション 5.3.3 に従ってエンコード ユニットのアドレスを含む非ページ メモリのアドレスを設定、 **AV/C**デジタル インターフェイス コマンド Set 全般の仕様、Rev 3.0 (0 xff)。 この仕様をご覧、 [1394 貿易](https://go.microsoft.com/fwlink/p/?linkid=8728)web サイト。 サブユニットの要求の完了時にこれを指しているこの仮想サブユニット インスタンスのサブユニット アドレスを格納しているメモリに注意してください。 呼び出し元はこの非ページ メモリにアクセスできますが、解放する必要がありますしません。

<span id="AlternateOpcodes"></span><span id="alternateopcodes"></span><span id="ALTERNATEOPCODES"></span>**AlternateOpcodes**  
単体のコマンドを受信登録するときにのみを使用します。 これは、呼び出し元でサポートされている単位オペコードの一覧を含んでいる非ページ メモリのアドレスに設定します。 オペコードの一覧の最初のバイトは、(バイト数に相当) を実行するオペコードの数です。 代替のオペコードの一覧を含んでいるメモリの合計文字数は**AlternateOpcodes**\[0\]+1。

<span id="Timeout"></span><span id="timeout"></span><span id="TIMEOUT"></span>**タイムアウト**  
無視されます。

<span id="Retries"></span><span id="retries"></span><span id="RETRIES"></span>**再試行**  
無視されます。

<span id="Opcode"></span><span id="opcode"></span><span id="OPCODE"></span>**オペコード**  
入力は無視されます。 出力では、AV/C 単位オペコードが含まれます。 これは 1 つを使用して指定するオペコードの**AlternateOpcodes**します。

<span id="OperandLength"></span><span id="operandlength"></span><span id="OPERANDLENGTH"></span>**OperandLength**  
入力は無視されます。 出力では、これは、要求で使用されるオペランド リスト内のバイト数に設定されます。

<span id="Operands"></span><span id="operands"></span><span id="OPERANDS"></span>**オペランド**  
入力は無視されます。 出力では、このパラメーターには、要求のオペランドの一覧が含まれています。

<span id="NodeAddress"></span><span id="nodeaddress"></span><span id="NODEADDRESS"></span>**NodeAddress**  
入力は無視されます。 出力では、これは、要求元のノードのアドレスに設定します。 このパラメーターは、応答を送信するときに使用されます (詳細については、次を参照してください。 [ **AVC\_関数\_送信\_応答**](avc-function-send-response.md))。

<span id="Generation"></span><span id="generation"></span><span id="GENERATION"></span>**生成**  
入力は無視されます。 出力では、これは場合に設定で生成数ノード アドレスが有効と見なされます。 このパラメーターは、応答を送信するときに使用されます (詳細については、次を参照してください。 [ **AVC\_関数\_送信\_応答**](avc-function-send-response.md))。

GUID のコンテキストで\_AVC\_クラス デバイスのインターフェイス、 **AVC\_関数\_取得\_要求**関数コードを使用して、AV/C 単位の受け取りを登録するには要求にのみ (サブユニット要求ではなく)。 この関数は、上位のフィルター ドライバーで使用が一般的に (の*avc.sys* FDO) ピア デバイスの機能をサポートするために (つまり、ユニット要求を処理する非仮想スタックからターゲット デバイスから)。 Nothing の部署の要求を処理するために登録のサブユニット ドライバーが防止されますが、サブユニット ドライバーのインスタンスが同じ単位のオペコードをサポートするために登録が状態情報を共有する互いと連携する必要があります。 *Avc.sys*同じ単位オペコードの複数の登録直接サポートしません。

この関数は、AVC\_コマンド\_IRB 構造体。 この構造体は、AV/C コマンドの要求の一般的なコンポーネントを定義します。 唯一の有効な入力パラメーターが**SubunitAddrFlag**、 **AlternateOpcodesFlag**、 **AlternateOpcodes**と**SubunitAddr**、および all必要です。 **AlternateOpcodes**呼び出し元でサポートされている単位オペコードの一覧を格納するバッファーを指す必要があります。 **SubunitAddr**単位アドレス (0 xff) を格納するバッファーを指す必要があります。

仮想インスタンスの場合*avc.sys* (つまり、GUID 登録インスタンス\_仮想\_AVC\_クラス デバイス インターフェイス) **AVC\_関数\_取得\_要求**AV/C 単体テストとサブユニット要求を受信登録するために使用します。 上部のフィルター ドライバー (仮想の*avc.sys* FDO) サブユニットの特定の型に対してサブユニット ドライバーの登録を処理する単位の要求を処理するのには登録が一般的に要求します。 Nothing の部署の要求を処理するために登録のサブユニット ドライバーが防止されますが、サブユニット ドライバーのインスタンスが同じ単位のオペコードをサポートするために登録が状態情報を共有する互いと連携する必要があります。 *Avc.sys*同じ単位オペコードの複数の登録直接サポートしません。

サブユニット ドライバーは、サブユニットに固有の要求を受信登録するときに、すべての入力パラメーターを設定しないでください。

この関数は、常にステータスを返します\_PENDING、ため、どのような処理を完了ルーチンで実行する必要があります。 完了、AVC\_コマンド\_IRB 構造体は、オペコードと要求のオペランドを保持します。 AV/C プロトコルでは、100 ミリ秒以内の応答を送信することが必要です。 これは、ことがありますから実行して完了ルーチンを使用して、 **AVC\_関数\_送信\_応答**関数。

最初の応答で使用する場合、 **AVC\_応答\_中間**応答コード (から、 **AvcResponseType**列挙型)、フォロー アップ処理が必要です。 **NodeAddress**と**生成**メンバー、取得、完了した、 **AVC\_関数\_取得\_要求**その後の応答では、元の関数を使用する必要があります。 次の場合も、 **AVC\_関数\_取得\_要求**関数は、最初から戻る前に送信する必要があります**AVC\_関数\_送信\_応答**完了ルーチンの場合は、次の単位の要求を受信する可能性がありますようにします。

この構造体の推奨される使用は、まず、構造体をゼロに (を使用して、 **RtlZeroMemory**) パラメーターを入力する前にします。

この関数のコードは、IRQL で呼び出すことができます&lt;= ディスパッチ\_レベル。

### <a name="see-also"></a>参照

[**AVC\_関数\_送信\_応答**](avc-function-send-response.md)、 [ **AvcResponseCode**](https://msdn.microsoft.com/library/windows/hardware/ff554105)、 [ **AVC\_関数**](https://msdn.microsoft.com/library/windows/hardware/ff554145)、 [ **RtlZeroMemory**](https://msdn.microsoft.com/library/windows/hardware/ff563610)

 

 





