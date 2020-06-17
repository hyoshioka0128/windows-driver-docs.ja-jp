---
title: AVC \_ 関数 \_ コマンド
description: AVC \_ 関数 \_ コマンド
ms.assetid: 5e1f7f93-83ef-4015-a952-f7efd93ccee5
keywords:
- ストリーミングメディアデバイスの AVC_FUNCTION_COMMAND
topic_type:
- apiref
api_name:
- AVC_FUNCTION_COMMAND
api_type:
- NA
ms.date: 06/16/2020
ms.localizationpriority: medium
ms.openlocfilehash: 4a123f1af870c663cb8528231afadd403f6bd2f2
ms.sourcegitcommit: 97a8d24b1b48602e4ccaa63a113f7c8cdb0c6df5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2020
ms.locfileid: "84812446"
---
# <a name="avc_function_command"></a>AVC \_ 関数 \_ コマンド

**AVC \_ 関数の \_ コマンド**関数コードを使用して、AV/C 要求を送信し、1つの操作として応答を受信します。

## <a name="io-status-block"></a>I/O ステータス ブロック

成功した場合、AV/C プロトコルドライバーは、 **Irp- &gt; iostatus**を status に設定します。 \_

その他の戻り値には次のようなものがあります。

| 戻り値 | 説明 |
|--|--|
| STATUS_TIMEOUT | 要求が行われましたが、すべてのタイムアウトと再試行処理が完了する前に応答が受信されませんでした。 前の要求がまだ処理されている場合、ターゲットデバイスは要求を無視します。 一部の AV/C デバイスは準拠していません。また、連続して複数回試行された後でも、100-ms のタイムアウト時間内に応答を拒否します。 AVC_COMMAND_IRB 構造では、既定の**タイムアウト**メンバーと**再試行**メンバー (それぞれ100ミリ秒と 9) の調整が許可されますが、これらの既定の設定はすべての既知の実装に対して十分です。 |
| STATUS_PENDING | 要求が行われ、中間応答が受信されました。 最終的な応答を処理し、IRP と IRB のリソースを解放するのは、完了ルーチンの役割です。 |
| STATUS_REQUEST_ABORTED | AV/C 要求を送信すると、IRP の完了状態が STATUS_REQUEST_ABORTED になるとすぐに中止されます。 |
| STATUS_ * | その他のリターンコードは、AV/C プロトコルの範囲を超えてエラーまたは警告が発生したことを示します。 |

## <a name="comments"></a>コメント

この関数は、 \_ \_ 次に示すように、AVC コマンド IRB 構造体を使用します。

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

## <a name="requirements"></a>必要条件

**ヘッダー:***Avc*で宣言されています。 *Avc. h*を含めます。

## <a name="avc_command_irb-input"></a>AVC \_ コマンド \_ IRB 入力

**共通**
  
このメンバーの**関数**サブメンバーは、avc 関数の列挙から**avc \_ 関数 \_ コマンド**に設定する必要があり \_ ます。

**SubunitAddrFlag**
  
このを1に設定すると、 *avc.sys*サブユニットドライバーに関連付けられているサブユニットのアドレスが上書きされます。 オーバーライドする理由: サブユニットドライバーは、1つのインスタンス内の複数のサブユニットを表します。unit コマンドを送信する必要があります。または、 *avc.sys*がサブユニットの種類または ID を特定できなかったため、ドライバーが読み込まれました。 これが設定されている場合、 **Subunitaddr**メンバーは、必要なサブユニットアドレスを含む非ページメモリを指している必要があります。

呼び出し元が*avc.sys* FDO に直接要求を送信している場合は、これを 1 (および適切な**subunitaddr**を指定) に設定する必要があります。

> [!NOTE]
> 要求に対してこのフラグが設定されていない場合、成功した要求からの応答時に、このフラグが設定され、 **Subunitaddr**メンバーがサブユニットの実際のアドレスをポイントします。 コンテンツを変更したり、メモリを解放したりしないでください。親ドライバーのデバイス拡張機能の一部です。 もちろん、これはゼロに戻すことができ、サブサブユニットの構造を再利用するために**Subunitaddr**ポインターがクリアされます。

**Alternateopのフラグ**

この要求のコマンドの種類とオペコードによって異なるオペコードの応答が返される場合は、これを1に設定します。 これを使用しない場合は、対応するオペコードのある応答だけが受け入れられます。 これが設定されている場合、 **alternateopcodes**メンバーは、代替オペコードのリストを含む非ページメモリへのポインターである必要があります。

**TimeoutFlag**
  
既定のタイムアウトがサブユニットに適していない場合は、これを1に設定します。 これが設定されている場合は、**タイムアウト**メンバーを目的のタイムアウト (100-ns 単位) に設定する必要があります。

**RetryFlag**
  
既定の再試行回数がサブユニットに適していない場合は、これを1に設定します。 これが設定されている場合は、**再試行**メンバーを目的の再試行回数に設定する必要があります。

**CommandType**

要求時には、このメンバーを**Avccommandtype**列挙子の列挙子の1つに設定する必要があります。 これは必須パラメーターです。

**ResponseCode**

応答では、このメンバーは**AvcResponseCode**列挙体の値に設定されます。

**SubunitAddr**
  
これを、AV/C デジタルインターフェイスのコマンドセット全般仕様の5.3.3 のセクションに従ってエンコードされた、必要なサブユニットアドレスを含む非ページメモリのアドレスに設定します。リビジョン3.0。 この仕様は、 [1394 貿易 Association](https://1394ta.org/library-2/) web サイトにあります。 サブユニットアドレスエンコーディングはこれを意味するため、長さは必要ありません。 **Subunitaddrflag**が0の場合、このパラメーターは無視されます。

**AlternateOpcodes**

これを、目的の代替オペコードリストを含む非ページメモリのアドレスに設定します。 オペコードリストの最初のバイトは、後に続くオペコードの数です (バイト数と同じです)。 代替オペコードリストを含むメモリの合計の長さは AlternateOpcodes \[ 0 \] + 1 です。 **Alternateopのフラグ**が0の場合、このパラメーターは無視されます。

**タイムアウト**  

これを 100-ns ユニットの目的のタイムアウトに設定します。 たとえば、既定のタイムアウト値は、 **QuadPart** = 100万 (100 ナノ秒単位の100ミリ秒) です。 **Timeoutflag**が0の場合、このパラメーターは無視されます。

**再試行**

この値は、応答なしでタイムアウトが発生するたびに要求の再試行を試行*avc.sys*回数に設定します。 再試行回数が0の場合は、要求が1回試行されることを意味します。 応答を取得せずにコマンドを処理するために費やされた合計時間は、次の式によって計算されます。

***タイムアウト*** * \* (* * *<em>再試行</em>* *  *+ 1)*

**Retryflag**が0の場合、このパラメーターは無視されます。

**オペコード**

これを目的の AV/C オペコード (サブユニットの種類に適したもの) に設定します。 これは必須パラメーターです。 応答時に、 **Alternateopのフラグ**が設定されていて、代替オペコードの1つが応答に一致するために使用された場合、これは代替オペコードに設定されます。

**オペレーティング Andlength**  

**オペランドメンバーに**オペランドを格納するために使用するバイト数を設定します。 これは必須パラメーターです。 応答では、このパラメーターは、応答によって使用されるオペランドリストのバイト数に設定されます。

**オペランド**
  
これを、サブユニットの種類とオペコードに適したオペランドリストに設定します。 これは必須パラメーターです。 応答時に、このパラメーターには応答のオペランドリストが含まれます。

**NodeAddress**

予約済み。 0にする必要があります。

**Generation**
  
予約済み。 0にする必要があります。

**AVC \_ 関数 \_ コマンド**関数のコードは、 *avc.sys*の仮想インスタンスではサポートされていません。 呼び出し元が外部デバイスを制御する必要がある場合、そのデバイスの非仮想インスタンスは、プライベートメカニズムを通じて、または AVC 関数を組み合わせて使用することによって、 \_ \_ \_ \_ IOCTL avc クラスの i/o 制御コードのサブ** \_ \_ \_ ユニット \_ 情報**関数コードを取得でき** \_ \_ \_ \_ ** \_ \_ ます。

この構造体は、AV/C コマンド要求の共通コンポーネントを定義します。 これには、要求のオペコードとオペランド、および応答のオペコードとオペランド (完了時) が格納されます。 オペランドリストのサイズは、1バイトサブレベルアドレスを指定した場合に許容される最大オペランド数で固定されます。 サブユニットアドレスが何らかの方法で拡張されている場合、オペランドバイトの最大許容数はそれに応じて小さくなります。

この構造体の使用を推奨するには、最初に構造体をゼロにしてから ( **Rtlzero memory**を使用して)、パラメーターを入力します。

これは、IRQL = パッシブレベルで呼び出す必要があり \_ ます。

## <a name="see-also"></a>関連項目

[**AVC \_ 関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)

[**AvcCommandType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavccommandtype)

[**AvcResponseCode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavcresponsecode)

[**AVC \_ 関数 \_ FIND \_ ピア \_ DO**](avc-function-find-peer-do.md)

[**AVC \_ 関数 \_ の \_ ピア \_ リスト**](avc-function-peer-do-list.md)

[**AVC \_ 関数のサブ \_ \_ ユニット情報の取得 \_**](avc-function-get-subunit-info.md)
