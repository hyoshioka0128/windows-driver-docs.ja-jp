---
title: NDIS 6.80 の同期 OID 要求インターフェイス
description: このトピックでは、NDIS 6.80 の新しい同期 OID 要求インターフェイスについて説明します。
ms.assetid: 6BF2E800-90A0-48FC-B702-5AD4EC318A35
keywords: 同期 oid 要求インターフェイス、同期 OID 呼び出し、WDK 同期 oid、同期 OID 要求
ms.date: 09/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1787e8ba74dba5f2e69674cd9272c33e601670d1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841783"
---
# <a name="synchronous-oid-request-interface-in-ndis-680"></a>NDIS 6.80 の同期 OID 要求インターフェイス

Windows ネットワークドライバーは、OID 要求を使用して、制御メッセージを NDIS バインドスタックに送信します。 TCPIP や vSwitch などのプロトコルドライバーは、基になる NIC ドライバーの各機能を構成するために多数の Oid に依存しています。 Windows 10 バージョン1709より前では、OID 要求は2つの方法 (Regular と Direct) で送信されました。 

このトピックでは、OID 呼び出しの3番目のスタイルである同期を紹介します。 同期呼び出しは、待機時間の短い、非ブロッキング、拡張性、および信頼性が高いことを目的としています。 同期 OID 要求インターフェイスは、Windows 10 バージョン1709以降に含まれる NDIS 6.80 以降で使用できます。

## <a name="comparison-to-regular-and-direct-oid-requests"></a>正規および直接の OID 要求との比較

同期 OID 要求では、呼び出しのペイロード (OID 自体) は、標準および直接の OID 要求とまったく同じです。 唯一の違いは呼び出し自体です。 このため、3種類の Oid すべてで同じ*ことが言え*ます。*方法*は異なります。

次の表では、正規 Oid、直接 Oid、および同期 Oid の違いについて説明します。

| | 標準 OID | 直接 OID | 同期 OID |
| --- | --- | --- | --- |
| ペイロード | [NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request) | NDIS_OID_REQUEST | NDIS_OID_REQUEST |
| OID 型 | Stats、Query、Set、メソッド | Stats、Query、Set、メソッド | Stats、Query、Set、メソッド |
| 発行元 | プロトコル、フィルター | プロトコル、フィルター | プロトコル、フィルター |
| 完了可能 | ミニポート、フィルター | ミニポート、フィルター | ミニポート、フィルター |
| フィルターを変更できます。 | [はい] | [はい] | [はい] |
| NDIS はメモリを割り当てます | 各フィルター (OID 複製) | 各フィルター (OID 複製) | 異常に多数のフィルター (呼び出しコンテキスト) がある場合のみ |
| 保留可能 | [はい] | [はい] | 必須ではない |
| ブロック可能 | [はい] | 必須ではない | 必須ではない |
| IRQL | = = パッシブ | \<= ディスパッチ | \<= ディスパッチ |
| [NDIS によるシリアル化](miniport-adapter-oid-request-serialization.md) | [はい] | 必須ではない | 必須ではない |
| フィルターが呼び出されます | 調べ | 調べ | 繰り返し |
| フィルターで OID が複製されます | [はい] | [はい] | 必須ではない |

## <a name="filtering"></a>フィルター

他の2種類の OID 呼び出しと同様に、フィルタードライバーは同期呼び出しで OID 要求を完全に制御できます。 フィルタードライバーは、同期 Oid の監視、インターセプト、変更、および発行を行うことができます。 ただし、効率を高めるために、同期 OID のしくみは多少異なります。

### <a name="passthrough-interception-and-origination"></a>パススルー、傍受、および発信

概念的には、すべての OID 要求が上位のドライバーから発行され、下位のドライバーによって完了されます。 その過程で、OID 要求は任意の数のフィルタードライバーを通過することがあります。

最も一般的なケースでは、プロトコルドライバーは OID 要求を発行し、すべてのフィルターは OID 要求を変更せずに渡します。 次の図は、この一般的なシナリオを示しています。

![一般的な OID パスがプロトコルから生成](images/synchronous_oids_oid_path_full.png "一般的な OID パスがプロトコルから生成")

ただし、すべてのフィルターモジュールは OID 要求をインターセプトして完了することができます。 その場合、次の図に示すように、要求は下位のドライバーに渡されません。

![一般的な OID パスがプロトコルから生成され、フィルターによってインターセプトされています](images/synchronous_oids_oid_path_intercepted.png "一般的な OID パスがプロトコルから生成され、フィルターによってインターセプトされています")

場合によっては、フィルターモジュールが独自の OID 要求を生成することがあります。 この要求は、次の図に示すように、フィルターモジュールのレベルから開始し、下位のドライバーのみを走査します。

![フィルターから生成した一般的な OID パス](images/synchronous_oids_oid_path_filter_originated.png "フィルターから生成した一般的な OID パス")

すべての OID 要求には、次の基本的なフローがあります。上位のドライバー (プロトコルまたはフィルタードライバー) が要求を発行し、下位のドライバー (ミニポートドライバーまたはフィルタードライバー) が完了します。

### <a name="how-regular-and-direct-oid-requests-work"></a>正規および直接の OID 要求の動作

標準または直接の OID 要求が再帰的にディスパッチされます。 次の図は、関数呼び出しシーケンスを示しています。 シーケンス自体は、前のセクションの図で説明したシーケンスとよく似ていますが、要求の再帰的な性質を示すように配置されています。

![正規および直接の OID 要求の関数呼び出しシーケンス](images/synchronous_oids_regular_oid_request_sequence.png "正規および直接の OID 要求の関数呼び出しシーケンス")

十分なフィルターがインストールされている場合、NDIS は recursing を深く保つために新しいスレッドスタックを強制的に割り当てます。

NDIS では、スタック上で1つのホップに対してのみ、 [NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体が有効であると見なされます。 フィルタードライバーが要求を次の下位のドライバーに渡す必要がある場合 (ほとんどの場合、Oid の大部分)、フィルタードライバーは OID 要求を複製するために数十行の定型コードを挿入する*必要があり*ます。 この定型句にはいくつかの問題があります。

1. これにより、OID を複製するためのメモリ割り当てが強制的に行われます。 メモリプールを使用すると、どちらも低速で、OID 要求の進行状況を保証できなくなります。
2. OID 構造体の設計は、すべてのフィルタードライバーが NDIS_OID_REQUEST の内容を別のものにコピーするメカニズムをハードコーディングするため、時間の経過と共に変わらないようにする必要があります。
3. 多くの定型句を必要とすると、フィルターが実際に実行されていることがわかります。

### <a name="the-filtering-model-for-synchronous-oid-requests"></a>同期 OID 要求のフィルター処理モデル

同期 OID 要求のフィルター処理モデルでは、呼び出しの同期の性質を利用して、前のセクションで説明した問題を解決します。

#### <a name="issue-and-complete-handlers"></a>問題と完全なハンドラー

標準および直接の OID 要求とは異なり、同期 OID 要求には2つのフィルターフックがあります。問題ハンドラーと完全なハンドラーです。 フィルタードライバーで登録できるフックは、いずれのフックでも、どちらでもかまいません。

問題の呼び出しは、スタックの一番上からスタックの一番下まで順に、各フィルタードライバーに対して呼び出されます。 フィルターの問題を呼び出すと、OID が下方に向かって続行されなくなり、何らかの状態コードで OID を完了できます。 Oid をインターセプトするフィルターがない場合、oid は NIC ドライバーに到達します。この場合、OID は同期的に完了する必要があります。

OID が完了すると、すべてのフィルタードライバーに対して完全な呼び出しが呼び出されます。これは、OID が完了したスタック内のどこからでも、スタックの最上位に向かって開始されます。 完全な呼び出しで OID 要求を検査または変更し、OID の完了ステータスコードを検査または変更できます。

次の図は、プロトコルが同期 OID 要求を発行し、フィルターが要求をインターセプトしない一般的なケースを示しています。

![同期 OID 要求の関数呼び出しシーケンス](images/synchronous_oids_synchronous_oid_request_sequence.png "同期 OID 要求の関数呼び出しシーケンス")

同期 Oid の呼び出しモデルは反復的であることに注意してください。 これにより、スタックの使用が定数によって制限され、スタックを拡張する必要がなくなります。

フィルタードライバーが問題ハンドラーで同期 OID をインターセプトすると、その OID は低いフィルターや NIC ドライバーに与えられません。 ただし、次の図に示すように、上位のフィルターの完全なハンドラーがまだ呼び出されています。

![フィルターによるインターセプトを使用した同期 OID 要求の関数呼び出しシーケンス](images/synchronous_oids_synchronous_oid_request_sequence_intercepted.png "フィルターによるインターセプトを使用した同期 OID 要求の関数呼び出しシーケンス")

#### <a name="minimal-memory-allocations"></a>最小メモリ割り当て

標準および直接の OID 要求では、NDIS_OID_REQUEST を複製するためにフィルタードライバーが必要です。 これに対して、同期 OID 要求を複製することはできません。 この設計の利点は、同期 Oid の待機時間が短くなることです。つまり、OID 要求がフィルタースタックの下に移動すると繰り返し複製されず、障害の可能性が少なくなります。

ただし、これによって新しい問題が発生します。 OID を複製できない場合は、フィルタードライバーが要求ごとの状態を格納する場所を指定します。 たとえば、フィルタードライバーがある OID を別の OID に変換したとします。 スタックの途中で、フィルターは古い OID を保存する必要があります。 スタックをバックアップする方法では、フィルターは古い OID を復元する必要があります。

この問題を解決するために、NDIS は、各フィルタードライバーに対して、各インフライト同期 OID 要求に対してポインターサイズのスロットを割り当てます。 NDIS は、フィルターの Issue ハンドラーから完全なハンドラーへの呼び出しでこのスロットを保持します。 これにより、問題ハンドラーは、後で完全なハンドラーによって使用される状態を保存できます。 次のコードスニペットは例を示しています。

```cpp
NDIS_STATUS
MyFilterSynchronousOidRequest(
  _In_ NDIS_HANDLE FilterModuleContext,
  _Inout_ NDIS_OID_REQUEST *OidRequest,
  _Outptr_result_maybenull_ PVOID *CallContext)
{
  if ( . . . should intercept this OID . . . )
  {
    // preserve the original buffer in the CallContext
    *CallContext = OidRequest->DATA.SET_INFORMATION.InformationBuffer;

    // replace the buffer with a new one
    OidRequest->DATA.SET_INFORMATION.InformationBuffer = . . . something . . .;
  }

  return NDIS_STATUS_SUCCESS;
}

VOID
MyFilterSynchronousOidRequestComplete(
  _In_ NDIS_HANDLE FilterModuleContext,
  _Inout_ NDIS_OID_REQUEST *OidRequest,
  _Inout_ NDIS_STATUS *Status,
  _In_ PVOID CallContext)
{
  // if the context is not null, we must have replaced the buffer.
  if (CallContext != null)
  {
    // Copy the data from the miniport back into the protocol’s original buffer.
    RtlCopyMemory(CallContext, OidRequest->DATA.SET_INFORMATION.InformationBuffer,...);
     
    // restore the original buffer into the OID request
    OidRequest->DATA.SET_INFORMATION.InformationBuffer = CallContext;
  }
}
```

NDIS は、呼び出しごとにフィルターごとに1つの PVOID を保存します。 NDIS ヒューリスティックでは、スタックに適切な数のスロットが割り当てられるため、一般的なケースでプール割り当てがゼロになります。 通常、これは7個以下のフィルターです。 ユーザーが pathological のケースを設定した場合、NDIS はプール割り当てにフォールバックします。

#### <a name="reduced-boilerplate"></a>短縮された定型句

[標準または直接の OID 要求を処理するための](example-boilerplate-for-handling-regular-or-direct-oid-requests.md)定型句の例を考えてみましょう。 このコードは、OID ハンドラーを登録するだけのコストです。 独自の Oid を発行する場合は、もう1行の定型句を追加する必要があります。 同期 Oid を使用すると、非同期の完了を処理する必要がなくなります。 そのため、その定型句の多くを切り取ることができます。

同期 Oid を持つ最小の問題ハンドラーを次に示します。

```cpp
NDIS_STATUS
MyFilterSynchronousOidRequest(
  NDIS_HANDLE FilterModuleContext,
  NDIS_OID_REQUEST *OidRequest,
  PVOID *CallContext)
{
  return NDIS_STATUS_SUCCESS;
}
```

特定の OID をインターセプトまたは変更する場合は、数行のコードを追加するだけで済みます。 最小の完全なハンドラーは、さらに単純です。

```cpp
VOID
MyFilterSynchronousOidRequestComplete(
  NDIS_HANDLE FilterModuleContext,
  NDIS_OID_REQUEST *OidRequest,
  NDIS_STATUS *Status,
  PVOID CallContext)
{
  return;
}
```

同様に、フィルタードライバーは、1行のコードだけを使用して、独自の新しい同期 OID 要求を発行できます。

```cpp
status = NdisFSynchronousOidRequest(binding->NdisBindingHandle, &oid);
```

これに対して、通常の OID または直接の OID を発行する必要があるフィルタードライバーでは、非同期の完了ハンドラーを設定し、独自の OID 入力候補を、複製した Oid の入力候補と区別するためのコードを実装する必要があります。 [通常の OID 要求を発行するための定型句](example-boilerplate-for-issuing-a-regular-oid-request.md)の例を次に示します。

## <a name="interoperability"></a>相互運用性

標準、直接、および同期呼び出しスタイルはすべて同じデータ構造を使用しますが、パイプラインはミニポートの同じハンドラーには移動しません。 また、一部の Oid は一部のパイプラインでは使用できません。 たとえば、 [OID_PNP_SET_POWER](oid-pnp-set-power.md)は慎重に同期する必要があり、多くの場合、ミニポートがブロック呼び出しを行うように強制します。 これにより、直接の OID コールバックでは困難な処理が行われ、同期 OID コールバックで使用できなくなります。 

したがって、直接 OID 要求と同様に、同期 OID 呼び出しは Oid のサブセットでのみ使用できます。 Windows 10 バージョン1709では、同期 OID パスでは、 [Receive Side Scaling version 2 (RSSv2)](receive-side-scaling-version-2-rssv2-.md)で使用されている[OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md) OID のみがサポートされています。

## <a name="implementing-synchronous-oid-requests"></a>同期 OID 要求の実装

ドライバーに同期 OID 要求インターフェイスを実装する方法の詳細については、次のトピックを参照してください。

- [ミニポートアダプターの OID 要求](miniport-adapter-oid-requests.md)
- [フィルターモジュール OID 要求](filter-module-oid-requests.md)
- [プロトコルドライバー OID 要求](protocol-driver-oid-requests.md)

