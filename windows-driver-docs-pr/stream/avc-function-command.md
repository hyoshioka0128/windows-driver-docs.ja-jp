---
title: AVC\_関数\_コマンド
description: AVC\_関数\_コマンド
ms.assetid: 5e1f7f93-83ef-4015-a952-f7efd93ccee5
keywords:
- AVC_FUNCTION_COMMAND ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- AVC_FUNCTION_COMMAND
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ef1a5ed6a0d62bafbbadc55fd94ad76f0d245ab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843557"
---
# <a name="avc_function_command"></a>AVC\_関数\_コマンド


## <span id="ddk_avc_function_command_ks"></span><span id="DDK_AVC_FUNCTION_COMMAND_KS"></span>


**AVC\_関数\_コマンド**関数コードを使用して、AV/C 要求を送信し、1つの操作として応答を受信します。

### <a name="io-status-block"></a>I/O ステータス ブロック

成功した場合、AV/C プロトコルドライバーは、 **Irp&gt;iostatus. status**を STATUS\_SUCCESS に設定します。

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
<td><p>STATUS_TIMEOUT</p></td>
<td><p>要求が行われましたが、すべてのタイムアウトと再試行処理が完了する前に応答が受信されませんでした。 前の要求がまだ処理されている場合、ターゲットデバイスは要求を無視します。 一部の AV/C デバイスは準拠していません。また、連続して複数回試行された後でも、100-ms のタイムアウト時間内に応答を拒否します。 AVC_COMMAND_IRB 構造体では、既定の<strong>タイムアウト</strong>メンバーと<strong>再試行</strong>メンバー (それぞれ100ミリ秒と 9) の調整が許可されますが、これらの既定の設定はすべての既知の実装に対して十分です。</p></td>
</tr>
<tr class="even">
<td><p>あります</p></td>
<td><p>要求が行われ、中間応答が受信されました。 最終的な応答を処理し、IRP と IRB のリソースを解放するのは、完了ルーチンの役割です。</p></td>
</tr>
<tr class="odd">
<td><p>STATUS_REQUEST_ABORTED</p></td>
<td><p>AV/C 要求を送信すると、IRP の完了状態が STATUS_REQUEST_ABORTED になるとすぐに中止されます。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_*</p></td>
<td><p>その他のリターンコードは、AV/C プロトコルの範囲を超えてエラーまたは警告が発生したことを示します。</p></td>
</tr>
</tbody>
</table>

 

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
このメンバーの**関数**サブメンバーは、AVC\_関数の列挙から、 **avc\_function\_コマンド**に設定する必要があります。

<span id="SubunitAddrFlag"></span><span id="subunitaddrflag"></span><span id="SUBUNITADDRFLAG"></span>**SubunitAddrFlag**  
これを1に設定すると、 *avc*がサブユニットドライバーに関連付けているサブシステムアドレスが上書きされます。 オーバーライドする理由: サブユニットドライバーは、1つのインスタンス内の複数のサブユニットを表します。unit コマンドを送信する必要があります。または、 *avc*がサブユニットの種類または ID を特定できなかったため、ドライバーが読み込まれました。 これが設定されている場合、 **Subunitaddr**メンバーは、必要なサブユニットアドレスを含む非ページメモリを指している必要があります。

呼び出し元が*avc* FDO に直接要求を送信している場合は、これを 1 (および適切な**subunitaddr**を指定) に設定する必要があります。

注: このフラグが要求に対して設定されていない場合、要求が成功したときにこのフラグが設定され、 **Subunitaddr**メンバーがサブユニットの実際のアドレスをポイントします。 コンテンツを変更したり、メモリを解放したりしないでください。親ドライバーのデバイス拡張機能の一部です。 もちろん、これはゼロに戻すことができ、サブサブユニットの構造を再利用するために**Subunitaddr**ポインターがクリアされます。

<span id="AlternateOpcodesFlag"></span><span id="alternateopcodesflag"></span><span id="ALTERNATEOPCODESFLAG"></span>**Alternateopのフラグ**  
この要求のコマンドの種類とオペコードによって異なるオペコードの応答が返される場合は、これを1に設定します。 これを使用しない場合は、対応するオペコードのある応答だけが受け入れられます。 これが設定されている場合、 **alternateopcodes**メンバーは、代替オペコードのリストを含む非ページメモリへのポインターである必要があります。

<span id="TimeoutFlag"></span><span id="timeoutflag"></span><span id="TIMEOUTFLAG"></span>**TimeoutFlag**  
既定のタイムアウトがサブユニットに適していない場合は、これを1に設定します。 これが設定されている場合は、**タイムアウト**メンバーを目的のタイムアウト (100-ns 単位) に設定する必要があります。

<span id="RetryFlag"></span><span id="retryflag"></span><span id="RETRYFLAG"></span>**RetryFlag**  
既定の再試行回数がサブユニットに適していない場合は、これを1に設定します。 これが設定されている場合は、**再試行**メンバーを目的の再試行回数に設定する必要があります。

<span id="CommandType"></span><span id="commandtype"></span><span id="COMMANDTYPE"></span>**CommandType**  
要求時には、このメンバーを**Avccommandtype**列挙子の列挙子の1つに設定する必要があります。 これは必須パラメーターです。

<span id="ResponseCode"></span><span id="responsecode"></span><span id="RESPONSECODE"></span>**ResponseCode**  
応答では、このメンバーは**AvcResponseCode**列挙体の値に設定されます。

<span id="SubunitAddr"></span><span id="subunitaddr"></span><span id="SUBUNITADDR"></span>**SubunitAddr**  
これを、AV/C デジタルインターフェイスのコマンドセット全般仕様の5.3.3 のセクションに従ってエンコードされた、必要なサブユニットアドレスを含む非ページメモリのアドレスに設定します。リビジョン3.0。 この仕様は、 [1394 貿易 Association](https://go.microsoft.com/fwlink/p/?linkid=8728) web サイトにあります。 サブユニットアドレスエンコーディングはこれを意味するため、長さは必要ありません。 **Subunitaddrflag**が0の場合、このパラメーターは無視されます。

<span id="AlternateOpcodes"></span><span id="alternateopcodes"></span><span id="ALTERNATEOPCODES"></span>**AlternateOpcodes**  
これを、目的の代替オペコードリストを含む非ページメモリのアドレスに設定します。 オペコードリストの最初のバイトは、後に続くオペコードの数です (バイト数と同じです)。 代替オペコードリストを含むメモリの合計の長さは、AlternateOpcodes\[0\]+ 1 です。 **Alternateopのフラグ**が0の場合、このパラメーターは無視されます。

<span id="Timeout"></span><span id="timeout"></span><span id="TIMEOUT"></span>**タイムアウト**  
これを 100-ns ユニットの目的のタイムアウトに設定します。 たとえば、既定のタイムアウト値は、 **QuadPart** = 100万 (100 ナノ秒単位の100ミリ秒) です。 **Timeoutflag**が0の場合、このパラメーターは無視されます。

<span id="Retries"></span><span id="retries"></span><span id="RETRIES"></span>**試行**  
これを必要な回数に設定し*ます。* この回数を過ぎると、各タイムアウトの後に、応答なしで要求を再試行します。 再試行回数が0の場合は、要求が1回試行されることを意味します。 応答を取得せずにコマンドを処理するために費やされた合計時間は、次の式によって計算されます。

***タイムアウト*** *\* (* * *<em>再試行</em>* *  *+ 1)*

**Retryflag**が0の場合、このパラメーターは無視されます。

<span id="Opcode"></span><span id="opcode"></span><span id="OPCODE"></span>**オペコード**  
これを目的の AV/C オペコード (サブユニットの種類に適したもの) に設定します。 これは必須パラメーターです。 応答時に、 **Alternateopのフラグ**が設定されていて、代替オペコードの1つが応答に一致するために使用された場合、これは代替オペコードに設定されます。

<span id="OperandLength"></span><span id="operandlength"></span><span id="OPERANDLENGTH"></span>**オペレーティング Andlength**  
**オペランドメンバーに**オペランドを格納するために使用するバイト数を設定します。 これは必須パラメーターです。 応答では、このパラメーターは、応答によって使用されるオペランドリストのバイト数に設定されます。

<span id="Operands"></span><span id="operands"></span><span id="OPERANDS"></span>**オペランド**  
これを、サブユニットの種類とオペコードに適したオペランドリストに設定します。 これは必須パラメーターです。 応答時に、このパラメーターには応答のオペランドリストが含まれます。

<span id="NodeAddress"></span><span id="nodeaddress"></span><span id="NODEADDRESS"></span>**NodeAddress**  
予約済み。 0にする必要があります。

<span id="Generation"></span><span id="generation"></span><span id="GENERATION"></span>**Generation**  
予約済み。 0にする必要があります。

Avc **\_関数\_コマンド**関数のコードは、 *avc*の仮想インスタンスではサポートされていません。 呼び出し元が外部デバイスを制御する必要がある場合、そのデバイスの非仮想インスタンスは、プライベートメカニズムを使用して、または AVC\_関数の組み合わせによって、\_ピア\_DO、Avc\_関数を検索\_ことによって見つけることができ **\_ピア\_DO\_LIST**および**avc\_\_関数**は、IOCTL\_avc\_クラス i/o 制御コードの\_サブユニット\_情報関数コードを取得します。

この構造体は、AV/C コマンド要求の共通コンポーネントを定義します。 これには、要求のオペコードとオペランド、および応答のオペコードとオペランド (完了時) が格納されます。 オペランドリストのサイズは、1バイトサブレベルアドレスを指定した場合に許容される最大オペランド数で固定されます。 サブユニットアドレスが何らかの方法で拡張されている場合、オペランドバイトの最大許容数はそれに応じて小さくなります。

この構造体の使用を推奨するには、最初に構造体をゼロにしてから ( **Rtlzero memory**を使用して)、パラメーターを入力します。

これは、IRQL = パッシブ\_レベルで呼び出す必要があります。

### <a name="see-also"></a>参照

[**Avc\_関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)、 [**avccommandtype**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavccommandtype)、 [**AvcResponseCode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavcresponsecode)、 [**AVC\_関数\_\_ピア\_do**](avc-function-find-peer-do.md)、 [**avc\_関数\_ピア\_do\_LIST**](avc-function-peer-do-list.md)、[**AVC\_関数\_\_サブユニット\_情報を取得**](avc-function-get-subunit-info.md)します

 

 





