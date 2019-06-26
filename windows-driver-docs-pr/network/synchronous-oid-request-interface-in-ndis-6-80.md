---
title: NDIS 6.80 で同期の OID 要求インターフェイス
description: このトピックでは、NDIS 6.80 で新しい同期 OID 要求インターフェイスをについて説明します
ms.assetid: 6BF2E800-90A0-48FC-B702-5AD4EC318A35
keywords: 同期の OID 要求インターフェイス、OID の同期呼び出し、WDK 同期 Oid、同期の OID 要求
ms.date: 09/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf8ad7ac8ec26466ffdf977ba2636d6b772e5259
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377974"
---
# <a name="synchronous-oid-request-interface-in-ndis-680"></a>NDIS 6.80 で同期の OID 要求インターフェイス

Windows ネットワーク ドライバーは、下位の NDIS バインド スタックのコントロール メッセージを送信するのに OID 要求を使用します。 TCPIP または vSwitch などのプロトコルのドライバーは、何十もの基になる NIC ドライバーの各機能を構成する Oid に依存します。 Windows 10 バージョン 1709 では、前に、2 つの方法で OID 要求が送信されました。正規表現とダイレクトします。 

このトピックでは、OID 呼び出しの 3 つ目のスタイルが導入されています。同期します。 同期呼び出しは、低待機時間、非ブロッキング、スケーラブルで信頼性の高いをするものでは。 同期の OID 要求インターフェイスは、以降、Windows 10 バージョン 1709 以降に含まれている NDIS 6.80 で使用できます。

## <a name="comparison-to-regular-and-direct-oid-requests"></a>標準モードと直接 OID 要求との比較

同期の OID の要求 (自体 OID) の呼び出しのペイロードはまったく同じ標準モードと直接 OID 要求と同様です。 唯一の違いは、呼び出し自体では。 そのため、*何*は 3 種類すべて Oid; の間で、同じのみ、*方法*は異なります。

次の表では、通常の Oid、直接 Oid は、同期の Oid の違いについて説明します。

| | 定期的な OID | 直接の OID | 同期の OID |
| --- | --- | --- | --- |
| ペイロード | [NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request) | NDIS_OID_REQUEST | NDIS_OID_REQUEST |
| OID の種類 | クエリの統計情報のセット、メソッド | クエリの統計情報のセット、メソッド | クエリの統計情報のセット、メソッド |
| によってを発行できます。 | プロトコルでフィルター | プロトコルでフィルター | プロトコルでフィルター |
| 行うことができます。 | ミニポート、フィルター | ミニポート、フィルター | ミニポート、フィルター |
| フィルターを変更できます。 | 〇 | 〇 | 〇 |
| NDIS はメモリを割り当てます | 各フィルター (OID クローン) | 各フィルター (OID クローン) | 場合にのみ異常に多数のフィルター (呼び出しコンテキスト) |
| 保留をことができます。 | 〇 | 〇 | X |
| ブロックすることができます。 | 〇 | X | X |
| IRQL | パッシブ = = | \<= ディスパッチ | \<= ディスパッチ |
| [NDIS によってシリアル化](miniport-adapter-oid-request-serialization.md) | 〇 | X | X |
| フィルターが呼び出されます | 再帰的に | 再帰的に | 繰り返し |
| フィルター、OID を複製します。 | 〇 | 〇 | X |

## <a name="filtering"></a>フィルター

型と同様に、他の 2 つの OID の呼び出しのフィルター ドライバーは同期呼び出しで OID 要求に対するフル コントロールがあります。 フィルター ドライバーを確認できます、インターセプト、変更、および同期の Oid を発行します。 ただし、効率を高めるため、同期の OID のしくみが少し異なります。

### <a name="passthrough-interception-and-origination"></a>パススルー、傍受、および発信元

概念的には、OID のすべての要求は、以上のドライバーから発行され、下位のドライバーによって完了します。 過程で、OID 要求は、任意の数のフィルター ドライバーを通過可能性があります。

最も一般的な場合は、プロトコル ドライバー OID 要求を発行して、すべてのフィルターが変更されていないダウン OID 要求を渡すだけで済みます。 次の図は、この一般的なシナリオを示します。

![一般的な OID パスの発生元、プロトコル](images/synchronous_oids_oid_path_full.png "プロトコルから発生した一般的な OID パス")

ただし、任意のフィルター モジュールは OID 要求をインターセプトし、その完了を許可します。 その場合は、要求を通過しません、ドライバーを削減する次の図に示すようにします。

![一般的な OID パス プロトコルの発生元し、フィルターによってインターセプト](images/synchronous_oids_oid_path_intercepted.png "一般的な OID パスは、プロトコルの発生元し、フィルターによってインターセプト")

場合によっては、フィルター モジュールを独自の OID 要求を送信することがあります。 この要求フィルター モジュールのレベルで開始し、として次の図は、下位のドライバーのみを行き来します。

![フィルターから発生した一般的な OID パス](images/synchronous_oids_oid_path_filter_originated.png "フィルターから発生した一般的な OID パス")

OID のすべての要求があるこの基本的なフロー: 以上のドライバー (プロトコルまたはフィルター ドライバー) 要求を発行して、下位のドライバー (フィルターまたはミニポート ドライバー) は、それを完了します。

### <a name="how-regular-and-direct-oid-requests-work"></a>OID が作業を要求する正規表現と直接方法

定期的なバックアップまたは直接 OID 要求は、ディスパッチを再帰的にです。 次の図は、関数の呼び出しシーケンスを示します。 シーケンス自体が、図、前のセクションからで説明されているシーケンスと似ていますが、要求の再帰的な性質を表示する配置されていることに注意してください。

![関数の呼び出しシーケンスを標準モードと直接 OID 要求](images/synchronous_oids_regular_oid_request_sequence.png "関数呼び出しのシーケンスの標準モードと直接 OID 要求")

インストールされているための十分なフィルターがある場合は、NDIS はより深い再帰を保持する新しいスレッド スタックの割り当てが強制されます。

NDIS 考慮、 [NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)構造体が、スタックを利用のシングル ホップでのみ有効です。 フィルター ドライバーが (つまり Oid のほとんどの場合) [次へ] の下ドライバー、要求を渡すかどうか、フィルター ドライバー*する必要があります*OID 要求を複製する定型コードのいくつかの数十行を挿入します。 この定型コードでは、いくつかの問題があります。

1. OID のクローンを作成するメモリの割り当てを強制的にされます。 メモリ プールに達すると、低速の両方が、OID 要求の転送の進行状況を保証することはできません。
2. OID の構造の設計が同じである時間の経過と共にすべてのフィルター ドライバー ハード コード別に 1 つ NDIS_OID_REQUEST の内容のコピー メカニズムであるためです。
3. 多くの定型コードを必要とするフィルターが本当に何不明になります。

### <a name="the-filtering-model-for-synchronous-oid-requests"></a>同期の OID 要求のフィルタ リング モデル

OID の同期要求のフィルタ リング、モデルでは、前のセクションで説明した問題を解決するために、呼び出しの同期特性を利用します。

#### <a name="issue-and-complete-handlers"></a>問題および完了ハンドラー

通常、直接 OID 要求とは異なりがフックをフィルター処理の要求を同期 OID の 2 つ: 問題のハンドラーを完了ハンドラー。 フィルター ドライバーには、どちらも、1 つ、または両方のフックを登録できます。

問題の呼び出しは、スタックの一番下までスタックの一番上からフィルター ドライバーごとに呼び出されます。 フィルターの問題の呼び出しが、OID の下に、続行を停止し、いくつかの状態コードの OID を完了します。 OID をインターセプトする決定したフィルターがない場合は、OID、OID を同期的に完了する必要があります NIC ドライバーに到達します。

OID が完了すると、完全な呼び出しは任意の場所スタックの OID 完了しましたが、スタックの最上部からフィルター ドライバーごとに呼び出されます。 完全な呼び出しは、検査、OID 要求の変更または検査しまたは OID の完了ステータス コードを変更できます。

次の図は、一般的な例をプロトコル同期 OID 要求を発行して、フィルターは、要求をインターセプトできません。

![関数の呼び出しシーケンスを同期 OID 要求](images/synchronous_oids_synchronous_oid_request_sequence.png "同期 OID 要求の関数の呼び出しシーケンス")

同期 Oid の呼び出しモデルは反復的なことに注意してください。 これにより、スタックの使用制限定数の場合、これまで、スタックを展開する必要はありません。

フィルター ドライバーでは、その問題のハンドラーでの同期の OID はインターセプト、アプリケーションの OID は低いフィルターまたは NIC ドライバーを付与しません。 ただしより高いフィルターの完了ハンドラーは呼び出さも次の図に示すように。

![OID の同期要求をインターセプトの呼び出しシーケンスをフィルターで関数](images/synchronous_oids_synchronous_oid_request_sequence_intercepted.png "同期 OID 要求フィルターによってインターセプタの関数の呼び出しシーケンス")

#### <a name="minimal-memory-allocations"></a>最小限のメモリ割り当て

標準モードと直接 OID 要求、NDIS_OID_REQUEST を複製するフィルター ドライバーが必要です。 これに対し、OID の同期要求は、クローンを作成するのには使用できません。 この設計の利点は、ことがある低待機時間の同期の Oid – フィルター stack – ダウンをたどる際、OID 要求されていない複製繰り返しと失敗の可能性があります。

ただし、新しい問題が発生します。 OID のクローンを作成することはできない場合は、フィルター ドライバーを格納、要求ごとの状態ですか。 たとえば、フィルター ドライバーを別の 1 つの OID を変換します。 下位のスタックで、フィルターは、古い OID を保存する必要があります。 スタックのバックアップ方法では、古い OID を復元するフィルターが必要です。

この問題を解決するには、NDIS は実行中の同期の OID 要求ごとに、各フィルター ドライバーのポインター-サイズのスロットを割り当てます。 NDIS は、その完了ハンドラーには、フィルターの問題のハンドラーからの呼び出しでこのスロットを保持します。 これにより、完了ハンドラーによって後で使用される状態を保存する問題のハンドラーができます。 次のコード スニペットでは、例を示します。

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

NDIS は、フィルターは 1 回の呼び出しごとの 1 つの PVOID を保存します。 NDIS は、一般的なケースで 0 個のプール割り当てが存在するようにヒューリスティックによって、スタック上のスロットの合理的な数を割り当てます。 これは、通常は、7 個のフィルターです。 場合、ユーザーが異常なケースを設定 NDIS はクリアテキスト プールの割り当てにします。

#### <a name="reduced-boilerplate"></a>定型の削減

定型コードを検討してください[定期的なバックアップまたは直接 OID の要求を処理するための例の定型](example-boilerplate-for-handling-regular-or-direct-oid-requests.md)します。 このコードでは、OID ハンドラーを登録するだけのエントリのコストです。 独自の Oid を発行する場合は、別の数十行の定型コードを追加する必要があります。 同期の Oid には、非同期の完了を処理の複雑さを増加の必要はありません。 そのため、定型の多くを減らすことができます。

同期の Oid と最小限の問題のハンドラーを次に示します。

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

インターセプトまたは特定の OID を変更する場合は、2 つの行のコードを追加することで実行できます。 最小限の完了ハンドラーはもっとシンプルです。

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

同様に、フィルター ドライバーは、独自ののみを使用して 1 行のコードの新しい同期 OID 要求を発行できます。

```cpp
status = NdisFSynchronousOidRequest(binding->NdisBindingHandle, &oid);
```

これに対し、通常または OID を直接発行する必要があるフィルター ドライバーは、非同期の完了ハンドラーを設定して、複製した Oid の入力候補から独自の OID 入力候補を区別するためにいくつかのコードを実装する必要があります。 この定型コードの例が示すように[正規 OID 要求を発行するための例の定型](example-boilerplate-for-issuing-a-regular-oid-request.md)します。

## <a name="interoperability"></a>相互運用性

通常、直接、および同期呼び出し元は、同じデータ構造をすべての使用にスタイル、パイプラインは、ミニポートに同じハンドラーには移動できません。 さらに、いくつかの Oid は、パイプラインの一部では使用できません。 たとえば、 [OID_PNP_SET_POWER](oid-pnp-set-power.md)注意が必要な同期が必要ですし、多くの場合、ブロッキング呼び出しを実行するミニポートを強制します。 これは、処理されることを直接 OID コールバックでは困難と同期 OID コールバックでは、使用できなくなります。 

そのため、直接 OID 要求と同様に、同期の OID の呼び出しは、Oid のサブセットは使用のみすることができます。 Windows 10 バージョン 1709 でのみで、 [OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md)で使用される OID[受信側のスケーリングのバージョン 2 (RSSv2)](receive-side-scaling-version-2-rssv2-.md)同期 OID パスではサポートされてです。

## <a name="implementing-synchronous-oid-requests"></a>OID の同期要求を実装します。

ドライバーで、同期の OID 要求インターフェイスを実装する方法の詳細については、次のトピックを参照してください。

- [ミニポート アダプタの OID 要求](miniport-adapter-oid-requests.md)
- [モジュールの OID 要求をフィルター処理します。](filter-module-oid-requests.md)
- [プロトコル ドライバー OID 要求](protocol-driver-oid-requests.md)

