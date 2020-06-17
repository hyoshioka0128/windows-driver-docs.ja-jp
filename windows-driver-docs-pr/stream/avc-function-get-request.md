---
title: AVC \_ 関数の \_ GET \_ 要求
description: AVC \_ 関数の \_ GET \_ 要求
ms.assetid: b29df7a8-782b-4014-b47e-7cf917f8e99d
keywords:
- ストリーミングメディアデバイスの AVC_FUNCTION_GET_REQUEST
topic_type:
- apiref
api_name:
- AVC_FUNCTION_GET_REQUEST
api_type:
- NA
ms.date: 06/16/2020
ms.localizationpriority: medium
ms.openlocfilehash: 6ff4a57c1a3f97a7b0a9046481fba9c77b4ef2b8
ms.sourcegitcommit: 97a8d24b1b48602e4ccaa63a113f7c8cdb0c6df5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2020
ms.locfileid: "84812448"
---
# <a name="avc_function_get_request"></a>AVC \_ 関数の \_ GET \_ 要求

**AVC \_ 関数の \_ GET \_ 要求**関数コードを使用して、AV/C ユニットおよびサブユニットの要求を受信するように登録します。

## <a name="io-status-block"></a>I/O ステータス ブロック

この関数は常に **、Irp- &gt; iostatus**を PENDING に設定します。 \_

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
  
このメンバーの**関数**サブメンバーは、avc 関数の列挙から**avc \_ 関数の \_ GET \_ 要求**に設定する必要があり \_ ます。

**SubunitAddrFlag**
  
受信単位コマンドに登録するときにのみ使用されます。 これを1に設定し、 **Subunitaddr**パラメーターに単位アドレスを指定します。 サブユニットの要求では、完了時には1に設定され、 **Subunitaddr**パラメーターはこの仮想サブユニットインスタンスのサブユニットアドレスを含むメモリを指します。 呼び出し元はこの非ページメモリにアクセスできますが、解放を試みることはできません。

**Alternateopのフラグ**
  
受信単位コマンドに登録するときにのみ使用されます。 これを1に設定し、 **alternateopcodes**パラメーターで呼び出し元によってサポートされるオペコードの一覧を提供します。

**TimeoutFlag**
  
無視されます。

**RetryFlag**
  
無視されます。

**CommandType**
  
入力では無視されます。 出力時に、 **CommandType**メンバーは**avccommandtype**列挙子のいずれかの値に設定されます。

**ResponseCode**
  
要求では無視されます。

**SubunitAddr**
  
受信単位コマンドに登録するときにのみ使用されます。 これを、 **AV/C**デジタルインターフェイスコマンドセットの全般仕様 (リビジョン 3.0 (0xff)) の5.3.3 セクションに従ってエンコードされたユニットアドレスを含む非ページメモリのアドレスに設定します。 この仕様は、 [1394 貿易 Association](https://1394ta.org/library-2/) web サイトにあります。 サブユニット要求の場合、これは、この仮想サブユニットインスタンスのサブユニットアドレスを含むメモリを指します。 呼び出し元はこの非ページメモリにアクセスできますが、解放を試みることはできません。

**AlternateOpcodes**
  
受信単位コマンドに登録するときにのみ使用されます。 これを、呼び出し元によってサポートされる単体オペコードのリストを含む非ページメモリのアドレスに設定します。 オペコードリストの最初のバイトは、後に続くオペコードの数です (バイト数と同じです)。 代替オペコードリストを含むメモリの合計の長さは**alternateopcodes** \[ 0 \] + 1 です。

**タイムアウト**
  
無視されます。

**再試行**
  
無視されます。

**オペコード**
  
インポート時には無視されます。 出力時に、これには AV/C ユニットオペコードが含まれています。 これは、 **Alternateopcodes**によって指定されたオペコードの1つです。

**オペレーティング Andlength**
  
インポート時には無視されます。 出力時には、要求で使用されるオペランドリストのバイト数に設定されます。

**オペランド**
  
インポート時には無視されます。 出力時に、このパラメーターには、要求のオペランドリストが含まれます。

**NodeAddress**
  
インポート時には無視されます。 出力時には、要求の送信元のノードアドレスに設定されます。 このパラメーターは、応答を送信するときに使用されます (詳細については、「 [**AVC \_ 関数の \_ 送信 \_ 応答**](avc-function-send-response.md)」を参照してください)。

**Generation**
  
インポート時には無視されます。 出力時には、ノードアドレスが有効と見なされたときに、このが強制的に生成されます。 このパラメーターは、応答を送信するときに使用されます (詳細については、「 [**AVC \_ 関数の \_ 送信 \_ 応答**](avc-function-send-response.md)」を参照してください)。

GUID \_ avc クラスのデバイスインターフェイスのコンテキストで \_ は、 **avc 関数 \_ の \_ GET \_ 要求**関数コードを使用して、AV/C ユニット要求のみを受信するように登録します (サブユニット要求ではありません)。 この関数は、一般に、上位フィルタードライバー ( *avc.sys* FDO) によって、ピアデバイス機能 (つまり、非仮想スタックからターゲットデバイスからのユニット要求を処理するため) をサポートするために使用されます。 サブユニットドライバーがユニット要求を処理するために登録することはできませんが、同じユニットオペコードをサポートするために登録されているサブユニットドライバーインスタンスは、互いに連携して状態情報を共有する必要があります。 *Avc.sys*は、同じ単体オペコードに対して複数の登録を直接サポートしているわけではありません。

この関数は、AVC \_ コマンド \_ IRB 構造体を使用します。 この構造体は、AV/C コマンド要求の共通コンポーネントを定義します。 有効な入力パラメーターは、 **Subunitaddrflag**、 **alternateopのフラグ**、 **Alternateオペコード**、および**subunitaddr**だけです。すべてが必要です。 **Alternateopcodes**は、呼び出し元によってサポートされる単体オペコードのリストを格納しているバッファーを指す必要があります。 **Subunitaddr**は、ユニットアドレス (0xff) を含むバッファーを指している必要があります。

*avc.sys*の仮想インスタンス (つまり、GUID 仮想 AVC クラスのデバイスインターフェイスを登録するインスタンス) の場合、 \_ \_ \_ **AVC \_ 関数 \_ GET \_ 要求**を使用して、AV/C ユニットおよびサブユニットの要求を受信するように登録します。 上位フィルタードライバー (仮想*avc.sys* FDO) は、通常、ユニット要求を処理するために登録されますが、サブユニットドライバーは、特定の種類のサブユニットの要求を処理するように登録します。 サブユニットドライバーがユニット要求を処理するために登録することはできませんが、同じユニットオペコードをサポートするために登録されているサブユニットドライバーインスタンスは、互いに連携して状態情報を共有する必要があります。 *Avc.sys*は、同じ単体オペコードに対して複数の登録を直接サポートしているわけではありません。

サブユニットドライバーは、サブユニット固有の要求を受信するために登録するときに、入力パラメーターを設定しません。

この関数は常に PENDING 状態を返し \_ ます。そのため、すべての処理を完了ルーチンで実行する必要があります。 完了時に、AVC \_ コマンド \_ IRB 構造体は、要求のオペコードとオペランドを保持します。 AV/C プロトコルでは、100ミリ秒内で応答を送信する必要があります。 これは、 **AVC \_ 関数 \_ 送信 \_ 応答**関数を使用して、完了ルーチンから行うことができます。

最初の応答で、 **AVC \_ 応答の \_ 中間**応答コード ( **AvcResponseType**列挙) が使用されている場合は、フォローアップ処理が必要です。 **AVC \_ 関数 \_ GET \_ REQUEST** original 関数の完了によって取得された**nodeaddress**と**Generation**メンバーは、後続の応答で使用する必要があります。 どのような場合でも、次の Avc 関数の** \_ \_ GET \_ 要求**関数は、最初の**avc \_ 関数 \_ 送信 \_ 応答**の完了ルーチンから戻る前に送信して、次の単体要求を受信できるようにする必要があります。

この構造体の使用を推奨するには、最初に構造体をゼロにしてから ( **Rtlzero memory**を使用して)、パラメーターを入力します。

この関数コードは、IRQL <= ディスパッチレベルで呼び出すことができ \_ ます。

### <a name="see-also"></a>関連項目

[**AVC \_ 関数の \_ 送信 \_ 応答**](avc-function-send-response.md)

[**AvcResponseCode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavcresponsecode)

[**AVC \_ 関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)

[**Rtlゼロメモリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlzeromemory)
