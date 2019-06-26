---
title: AVC\_関数\_コマンド
description: AVC\_関数\_コマンド
ms.assetid: 5e1f7f93-83ef-4015-a952-f7efd93ccee5
keywords:
- AVC_FUNCTION_COMMAND ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- AVC_FUNCTION_COMMAND
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b897d5afd7ef8d6c3de5b660e85aa5079e00c452
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386757"
---
# <a name="avcfunctioncommand"></a>AVC\_関数\_コマンド


## <span id="ddk_avc_function_command_ks"></span><span id="DDK_AVC_FUNCTION_COMMAND_KS"></span>


**AVC\_関数\_コマンド**AV/C 要求を送信し、1 つの操作として応答を受信する関数のコードを使用します。

### <a name="io-status-block"></a>I/O ステータス ブロック

成功すると、AV/C をプロトコル ドライバーに設定**Irp -&gt;IoStatus.Status**ステータス\_成功します。

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
<td><p>STATUS_TIMEOUT</p></td>
<td><p>要求が行われたが、すべてタイムアウトするまでの応答が受信されず、再試行の処理が完了します。 ターゲット デバイスは、前の要求が処理中の場合、要求を無視します。 いくつか AV/C デバイスを準拠していない、およびいくつかの連続する試行した後でも 100 ミリ秒のタイムアウト以内に応答を拒否します。 AVC_COMMAND_IRB 構造により、既定値の調整<strong>タイムアウト</strong>と<strong>再試行</strong>メンバー (100 ミリ秒、9、それぞれ)、既定の設定は、すべてのための十分なされているが、既知の実装。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_PENDING</p></td>
<td><p>要求が行われ、暫定的な応答を受け取りました。 最後の応答を処理し、IRP と IRB リソースを解放するには、完了ルーチンの役目です。</p></td>
</tr>
<tr class="odd">
<td><p>STATUS_REQUEST_ABORTED</p></td>
<td><p>AV/C 要求を送信して、すぐに中止時に、IRP の完了ステータスが STATUS_REQUEST_ABORTED します。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_*</p></td>
<td><p>他のリターン コードでは、エラーまたは警告が発生したこと、AV/C プロトコルの範囲を超えていたことを示します。</p></td>
</tr>
</tbody>
</table>

 

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
**関数**にこのメンバーのサブメンバーを設定する必要があります**AVC\_関数\_コマンド**、AVC から\_関数の列挙体。

<span id="SubunitAddrFlag"></span><span id="subunitaddrflag"></span><span id="SUBUNITADDRFLAG"></span>**SubunitAddrFlag**  
設定されるアドレスをいずれかのサブユニットをオーバーライドするには、この*avc.sys*サブユニット ドライバーに関連付けます。 オーバーライドする原因が考えられます: サブユニット ドライバーが 1 つのインスタンスで複数のサブユニットを表します単位コマンドを送信する必要があります。に、ドライバーが読み込まれたまたは*avc.sys*サブユニットを特定できませんでしたを入力または id。 設定されている場合、 **SubunitAddr**メンバーは、目的のサブユニット アドレスを含む非ページ メモリを指す必要があります。

これは、いずれかに設定する必要があります (、適切な**SubunitAddr**提供)、呼び出し元に直接要求を送信する場合、 *avc.sys* FDO します。

注:要求が成功した場合からの応答に、要求では、このフラグは設定されていない場合は、このフラグが設定、および**SubunitAddr**サブユニットの実際のアドレスへのポインターします。 内容を変更またはメモリを解放しないでください。 親ドライバーのデバイスの拡張機能の一部になります。 これは、もちろん、戻る 0 に設定されます、および**SubunitAddr**ポインターが別のサブユニットの構造を再利用をクリアします。

<span id="AlternateOpcodesFlag"></span><span id="alternateopcodesflag"></span><span id="ALTERNATEOPCODESFLAG"></span>**AlternateOpcodesFlag**  
この場合は、1 つに、コマンドの種類と、この要求の結果のオペコードで設定異なるオペコードを含む応答。 これを行わないオペコードが一致する応答のみが受け入れられます。 設定されている場合、 **AlternateOpcodes**メンバーには、代替のオペコードの一覧を含んでいる非ページ メモリへのポインターがある必要があります。

<span id="TimeoutFlag"></span><span id="timeoutflag"></span><span id="TIMEOUTFLAG"></span>**TimeoutFlag**  
1 つの場合に既定値を設定このタイムアウトは、サブユニットは適していません。 設定されている場合、**タイムアウト**メンバーは、目的のタイムアウト (100 ナノ秒単位) を設定する必要があります。

<span id="RetryFlag"></span><span id="retryflag"></span><span id="RETRYFLAG"></span>**RetryFlag**  
設定の 1 の場合は、既定の再試行回数には、サブユニットは適していません。 設定されている場合、**再試行**メンバーは、必要な再試行回数を設定する必要があります。

<span id="CommandType"></span><span id="commandtype"></span><span id="COMMANDTYPE"></span>**CommandType**  
要求では、このメンバーをから列挙子のいずれかに設定する必要があります、 **AvcCommandType**列挙体。 これは、必須パラメーターです。

<span id="ResponseCode"></span><span id="responsecode"></span><span id="RESPONSECODE"></span>**ResponseCode**  
応答でこのメンバーがからの値に設定、 **AvcResponseCode**列挙体。

<span id="SubunitAddr"></span><span id="subunitaddr"></span><span id="SUBUNITADDR"></span>**SubunitAddr**  
これは、仕様」のセクション 5.3.3、AV/C デジタル インターフェイス コマンド設定全般、Rev 3.0 に従ってエンコードされた目的のサブユニット アドレスを含む非ページ メモリのアドレスに設定します。 この仕様をご覧、 [1394 貿易](https://go.microsoft.com/fwlink/p/?linkid=8728)web サイト。 長さは必要ありませんので、このことを意味のサブユニット アドレス エンコーディングです。 場合、このパラメーターは無視されます**SubunitAddrFlag**は 0 です。

<span id="AlternateOpcodes"></span><span id="alternateopcodes"></span><span id="ALTERNATEOPCODES"></span>**AlternateOpcodes**  
これは、必要な代替オペコードの一覧を含んでいる非ページ メモリのアドレスに設定します。 オペコードの一覧の最初のバイトは、(バイト数に相当) を実行するオペコードの数です。 代替のオペコードの一覧を含んでいるメモリの合計文字数は AlternateOpcodes\[0\]+1。 場合、このパラメーターは無視されます**AlternateOpcodesFlag**は 0 です。

<span id="Timeout"></span><span id="timeout"></span><span id="TIMEOUT"></span>**タイムアウト**  
これは、100 ナノ秒単位で目的のタイムアウトを設定します。 たとえば、既定のタイムアウト値には。**Timeout.QuadPart** = 1000000 (100 ナノ秒単位で 100 ミリ秒)。 場合、このパラメーターは無視されます**TimeoutFlag**は 0 です。

<span id="Retries"></span><span id="retries"></span><span id="RETRIES"></span>**再試行**  
必要な回数を設定*avc.sys*応答なしには、各タイムアウト後に要求を再試行しようとする必要があります。 再試行回数が 0 では、要求が 1 回試行ということに注意してください。 応答を取得することがなく、コマンドを処理するのにかかる時間の合計量は、次の数式で計算されます。

***タイムアウト***  *\* (* * *<em>再試行</em>* *  *+ 1)*

場合、このパラメーターは無視されます**RetryFlag**は 0 です。

<span id="Opcode"></span><span id="opcode"></span><span id="OPCODE"></span>**オペコード**  
これを設定、目的の AV/C オペコード (サブユニット種類に適した)。 これは、必須パラメーターです。 応答の場合は**AlternateOpcodesFlag**が設定された場合、および応答の一致に使用された代替オペコードのいずれか、これはその代替オペコードに設定します。

<span id="OperandLength"></span><span id="operandlength"></span><span id="OPERANDLENGTH"></span>**OperandLength**  
これでオペランドの格納に使用されるバイト数を設定、**オペランド**メンバー。 これは、必須パラメーターです。 応答では、このパラメーターは、応答で使用されるオペランド リスト内のバイト数に設定されます。

<span id="Operands"></span><span id="operands"></span><span id="OPERANDS"></span>**オペランド**  
このリスト に設定、オペランドのサブユニット型とオペレーション コードに適した。 これは、必須パラメーターです。 応答には、このパラメーターには、応答のオペランドの一覧が含まれています。

<span id="NodeAddress"></span><span id="nodeaddress"></span><span id="NODEADDRESS"></span>**NodeAddress**  
予約済み。 これは、0 でなければなりません。

<span id="Generation"></span><span id="generation"></span><span id="GENERATION"></span>**生成**  
予約済み。 これは、0 でなければなりません。

**AVC\_関数\_コマンド**の仮想インスタンスでは、関数のコードはサポートされていない*avc.sys*します。 呼び出し元の外部のデバイスを制御する場合、そのデバイスの非仮想インスタンスがある、プライベート メカニズムを介して、または、AVC の組み合わせを通じて\_関数\_検索\_ピア\_には、**AVC\_関数\_ピア\_は\_一覧**と**AVC\_関数\_取得\_サブユニット\_情報** IOCTL のコードを関数\_AVC\_クラス I/O 制御コード。

この構造体は、AV/C コマンドの要求の一般的なコンポーネントを定義します。 オペコードと要求、およびオペコードのオペランドと応答 (完了) のオペランドを保持します。 オペランド リストのサイズは、オペランドの 1 バイトのサブユニット アドレスが指定の最大許容数に固定されています。 サブユニット アドレスは、任意の方法で拡張は、オペランドのバイトの最大許容数が適宜減少されます。

この構造体の推奨される使用は、まず、構造体をゼロに (を使用して、 **RtlZeroMemory**) パラメーターを入力する前にします。

これは、IRQL で呼び出す必要がある = パッシブ\_レベル。

### <a name="see-also"></a>関連項目

[**AVC\_関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ne-avc-_tagavc_function)、 [ **AvcCommandType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ne-avc-_tagavccommandtype)、 [ **AvcResponseCode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ne-avc-_tagavcresponsecode)、 [**AVC\_関数\_検索\_ピア\_は**](avc-function-find-peer-do.md)、 [ **AVC\_関数\_ピア\_は\_一覧**](avc-function-peer-do-list.md)、 [ **AVC\_関数\_取得\_サブユニット\_情報**](avc-function-get-subunit-info.md)

 

 





