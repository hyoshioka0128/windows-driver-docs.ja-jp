---
title: MB 操作のセマンティクス
description: MB 操作のセマンティクス
ms.assetid: 5f04b7fd-3df3-4efa-bb26-c7f4cd3c9ebd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35a9abed7921cf569960297964292a7bcc875c90
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374060"
---
# <a name="mb-operational-semantics"></a>MB 操作のセマンティクス


### <a name="asynchronous-transactions"></a>非同期のトランザクション

MB ドライバー モデル、NDIS で提供される非同期通知メカニズムを使用して MB サービスとのミニポート ドライバーの間の演算のセマンティクスを非ブロッキングを前提としています 6.x します。 このメカニズムにより、現在の操作が完了するを待たずに処理用のミニポート ドライバーに OID 要求を送信し続ける MB サービス。

非同期のトランザクションでは、要求の状態の応答の後におよび、最終的なトランザクションを示す値を完了し、最初の要求で始まる 3 ウェイ ハンドシェイクです。 要求の状態の応答は、ミニポート ドライバーが要求を受け取ったことのみ確認される一時的です。 フォロー アップの非同期表示は、トランザクションの完了が通知されるトランザクションです。 ミニポート ドライバーでは、トランザクションの表示で状態コードだけではなく、結果のデータを返します。

### <a name="asynchronous-set-and-query-requests"></a>非同期*設定*と*クエリ*要求

多くは、*設定*と*クエリ*MB サービスによって使用される OID 要求を非同期に処理されます。 詳細については*設定*と*クエリ*OID の要求を参照してください[ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)します。 "WWAN 固有 Oid"テーブルに、 [MB のデータ モデル](mb-data-model.md)トピックを識別する Oid が非同期的に処理します。

次の図は、非同期の相互作用のシーケンスを表す*クエリ*MB サービスと、ミニポート ドライバー間のトランザクション。 太字の表す OID の識別子、またはトランザクションのフロー制御には、ラベルと通常のテキストに表示されるラベルは、OID 構造内で重要なフラグを表します。

![モバイル ブロード バンド サービスと、ミニポート ドライバーの間の非同期クエリ トランザクションの相互作用のシーケンスを示す図](images/wwanasyncquerytransaction.png)

3 ウェイ ハンドシェイクは、両方に同じ*クエリ*と*設定*要求。

除く[OID\_WWAN\_ドライバー\_CAP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-driver-caps)、他のすべての MB に固有の OID 要求 MB のミニポート ドライバーとの間で情報交換の非同期トランザクション メカニズムに従ってください次の他のメモと共にサービス:

-   ミニポート ドライバーに無効な OID 要求など、任意のエラー条件の OID 要求をすぐに失敗する必要があります。

-   ミニポート ドライバーが適切なエラー コードで、WWAN 固有のエラー条件に返す必要があります (たとえば、WWAN\_状態\_XXX) で指定されている、 **uStatus**イベント通知の構造体のメンバー。 ミニポート ドライバーを次のメンバーでも適切に埋める、 **uStatus**必要に応じて、メンバー。 ミニポート ドライバー塗りつぶしなど、 **ContextState.uNwError**のメンバー、 [ **NDIS\_WWAN\_コンテキスト\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_context_state)使用可能な場合、構造体します。 ただし、ピンに関連する Oid を処理するときに、エラーが発生のミニポート ドライバーしない可能性のある現在の PIN 状態情報で指定する、 **PinInfo.PinState**のメンバー [ **NDIS\_WWAN\_PIN\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info)します。

-   ミニポート ドライバーは、NDIS を返す必要があります\_状態\_INDICATION\_provisional すべて非同期 OID 要求の応答として必要です。

-   ミニポート ドライバーでは、OID 要求によって他の原因によって引き起こさデバイス状態の変更と区別できる必要があります。 ミニポート ドライバーは、結果、OID 要求の状態の変更のトランザクション通知を送信する必要があり、その他の原因から状態の変更について、不要なイベント通知を送信する必要があります。

-   MB サービスが要求を最初にメモリを割り当てていますが、ミニポート ドライバーはカーネル モードのメモリを管理する責任を負います。 MB サービスは、ミニポート ドライバーからの応答を受け取た後、サービスは OID 要求に割り当て、ユーザー モード メモリを解放可能性があります。

次の図は、非同期の相互作用のシーケンスを表す*設定*MB サービスと、ミニポート ドライバー間のトランザクション。 太字の表す OID の識別子、またはトランザクションのフロー制御には、ラベルと通常のテキストに表示されるラベルは、OID 構造内で重要なフラグを表します。

![非同期のセットのトランザクション モバイル ブロード バンド サービスと、ミニポート ドライバーの間の相互作用のシーケンスを示す図](images/wwanasyncsettransaction.png)

### <a name="asynchronous-response"></a>非同期応答

*NDIS 6.0 仕様*(Windows Vista でリリースされた) 新しい状態コードでは、NDIS を導入\_状態\_INDICATION\_ミニポート ドライバーの非同期の性質を伝達するために必要な作業、ミニポート ドライバーの一時的な要求に応答して OID MB サービスにトランザクション。

説明したよう[MB インターフェイスの概要](mb-interface-overview.md)、MB サービスには MB のミニポート ドライバーによって割り当てられているカーネル モード メモリに直接アクセスがありません。 カーネル モード メモリに格納されている実行結果がコピーされると見なされ、WMI などのなんらかの媒介によって MB サービスに提供される、または[NDIS フィルター ドライバー](ndis-filter-drivers2.md)します。 そのため、ミニポート ドライバーが後に割り当てられたカーネル モードのメモリを解放できます、 [ **NdisMIndicateStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)関数呼び出しが、トランザクションを示す値を返します。

ミニポート ドライバーと MB サービスが従う必要があるハンドシェイク プロシージャは、次の手順で説明します。

### <a name="mb-miniport-driver-procedure"></a>MB ミニポート ドライバー プロシージャ

OID 要求を受け取ると、ミニポート ドライバーは、次の手順を実行する必要があります。

1.  内容をコピーするカーネル モードでのメモリを割り当て、 [ **NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request) OID 要求に関連付けられたデータ構造体。

2.  要求のパラメーター、ことを確認、 **RequestId**と**RequestHandle** OID 要求構造体のメンバーでもコピーされます。 これらのメンバーは、トランザクションで後で使用される*indication*します。

3.  Provisional NDIS を返す\_状態\_INDICATION\_MB サービス ミニポート ドライバーが要求を非同期的に実行することを通知するために必要な作業状態の応答。

4.  操作の完了したら、必要に応じて、ローカルまたはドライバーに割り当てられたメモリに結果を格納します。

5.  呼び出す、 [ **NdisMIndicateStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)に未処理の操作が完了したことを MB サービスに通知する関数。 ミニポート ドライバーは、NDIS のメンバーで入力する必要があります\_状態\_を示す値を次のように構成します。
    1.  設定、 **StatusCode**状態通知の種類のメンバー。 たとえば、NDIS\_状態\_WWAN\_XXX。
    2.  設定、 **DestinationHandle**メンバーを**RequestHandle** NDIS で受信したメンバー\_OID\_ミニポート ドライバーが受信したときに、要求データが構造体、対応する OID 要求。
    3.  設定、 **RequestId**と一致するメンバー、 **RequestId**の NDIS メンバー\_OID\_ミニポート ドライバーが、対応する OID 要求を受信したときに要求の状態の構造体。
    4.  設定、 **StatusBuffer**と**StatusBufferSize**それぞれミニポート ドライバーに割り当てられたメモリや、メモリ バッファーのサイズを指定するメンバー。 このメモリ バッファーには、完了した操作の結果が含まれています。
    5.  操作が正常に完了すると、設定、 **uStatus** WWAN メンバー\_状態\_成功します。 それ以外の場合、設定、 **uStatus**メンバーを適切な WWAN\_状態\_XXX エラーの種類を示す値。

6.  関数呼び出しから制御が戻るときに、ミニポート ドライバーは OID 要求に割り当てられたことメモリを解放する必要があります。

### <a name="mb-service-procedure"></a>MB サービス プロシージャ

MB サービスは、次の手順を使用して非同期のトランザクションを処理します。

1.  OID データ構造に基づく要求をバッファー メモリを割り当てください。 適切な値を持つ構造体メンバー データを入力します。

2.  呼び出す、 [ **NdisOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest)関数と、 **InformationBuffer** OID のデータを指すメンバーが、OID 要求用の構造し、ミニポート ドライバーを待機応答します。

3.  NDIS の受信時に\_状態\_を示す値\_MB サービスの保存、ミニポート ドライバーから provisional 応答が必要な作業、 **RequestId**、割り当て済みのメモリを解放し、マーク、開いているとトランザクション。 この時点では、MB サービスが後続の OID 要求と通知を処理します。

4.  NDIS を使用して、通知の受信時に\_状態\_WWAN\_として XXX、 **StatusCode**値をチェックするかどうか、 **RequestId**と一致するすべてのトランザクションのオープンでマークされます。 一致がある場合、サービスは、トランザクションを閉じます。 一致が検出されない場合は、通知を要請していないイベント通知として扱います。

5.  返されるデータの処理、 **StatusBuffer**メンバーと状態の変更に応じて MB サービスを作成します。

### <a name="indications"></a>表示

WWAN に固有の 2 種類があります*兆候*ミニポート ドライバーを生成できます。

-   オブジェクトの状態に起因するイベント通知は、MB デバイスで変更します。

-   非同期操作の完了を知らせるトランザクション通知します。

どちらの場合も、ミニポート ドライバーが NdisMIndicateStatusEx 関数を呼び出す必要があります。

### <a name="event-notification"></a>イベント通知

イベント通知は、ミニポート ドライバーは、状態変更イベントとして MB サービスに示す値を事前に送信するという意味で要請されたです。 状態の変更が MB サービス以外のいくつかのエンティティからアクションに起因します。 MB サービスでは、ミニポート ドライバーは、変更の原因を検出することが前提としています。

任意 WWAN に固有のイベント通知のミニポート ドライバーを設定する必要があります、 **RequestId**の NDIS メンバー\_状態\_をゼロに構造体を示す値。 **StatusCode** MB デバイスのどのオブジェクトが変更されたメンバーを指定します。 ミニポート ドライバーでは、次の値のいずれかをこのオブジェクトを設定できます。

[**NDIS\_状態\_WWAN\_デバイス\_キャップ**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-caps)

[**NDIS\_状態\_WWAN\_準備\_情報**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ready-info)

[**NDIS\_状態\_WWAN\_ラジオ\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-radio-state)

[**NDIS\_状態\_WWAN\_PIN\_情報**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-info)

[**NDIS\_状態\_WWAN\_PIN\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-list)

[**NDIS\_状態\_WWAN\_ホーム\_プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-home-provider)

[**NDIS\_状態\_WWAN\_優先\_プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-providers)

[**NDIS\_状態\_WWAN\_VISIBLE\_プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-visible-providers)

[**NDIS\_状態\_WWAN\_登録\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-register-state)

[**NDIS\_状態\_WWAN\_パケット\_サービス**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service)

[**NDIS\_状態\_WWAN\_信号\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-signal-state)

[**NDIS\_状態\_WWAN\_コンテキスト\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-context-state)

[**NDIS\_状態\_WWAN\_プロビジョニング済み\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-provisioned-contexts)

[**NDIS\_状態\_WWAN\_サービス\_アクティブ化**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-service-activation)

[**NDIS\_状態\_WWAN\_SMS\_構成**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-configuration)

[**NDIS\_状態\_WWAN\_SMS\_受信**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-receive)

[**NDIS\_状態\_WWAN\_SMS\_送信**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-send)

[**NDIS\_状態\_WWAN\_SMS\_削除**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-delete)

[**NDIS\_状態\_WWAN\_SMS\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-status)

[**NDIS\_状態\_WWAN\_ベンダー\_特定**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-vendor-specific)

MB サービスでは、NDIS から他のイベント通知は処理も可能性があります。 これらの非 MB イベント通知とは限りませんが適用されない、要件を**RequestId**値は 0 に設定します。

### <a name="transactional-notifications"></a>トランザクション通知

ミニポート ドライバーでは、トランザクション通知を使用して、MB サービスには、非同期のトランザクションが完了したらに通知し、開いているトランザクションを終了し、そのステート マシンを更新する、MB サービスがトランザクション通知を使用します。

開いているトランザクションを閉じることができます、MB、サービスがトランザクション通知を要求します。 MB サービスと非同期のトランザクションでミニポート ドライバーの間に 3 ウェイ ハンドシェイクの最後の exchange になります。 値**RequestId**の NDIS メンバー\_状態\_で任意のトランザクション通知を示す値があります 0 以外の場合、これは、同じトランザクションに対応する要求からコピーします。

設定する必要があります、 **RequestId**の NDIS メンバー\_状態\_正しく、適切に機能する非同期メカニズムを示す値構造体。 MB サービスにより、 **RequestId**値が一意であり、すべての未処理の要求間で 0 以外の場合。 ミニポート ドライバーは、同じを返す必要があります**RequestId** 、対応する値*indication* MB サービスに、開いているトランザクションを示す値を関連付けるためにします。

### <a name="status-indication-structure"></a>ステータスを示す値構造体

特定の OID 要求と要請していないイベント通知の構造体の両方、非同期応答によってポイントされている次の構造体メンバーの共有**StatusBuffer**のメンバー、 *StatusIndication*パラメーターを[ **NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex):

```C++
typedef struct _NDIS_WWAN_XXX {
  NDIS_OBJECT_HEADER Header;
  WWAN_STATUS uStatus;
  ULONG uNwError;//Optional. Only used for network operations.
  WWAN_XXX XxxStruct;
} NDIS_WWAN_XXX, *PNDIS_WWAN_XXX;
```

値 0、 **RequestId**の NDIS メンバー\_状態\_INDICATION 構造により、要請されていないイベント通知は、いつでも実行できます。

場合、 **uStatus**メンバーのいずれかを示す、返される値で*設定*または*クエリ*OID 要求と等しく WWAN\_状態\_成功、関連付けられている NDIS のメンバー\_WWAN\_XXX 構造体を有効にする必要はありません。

ネットワーク イベントに基づく要請されていないイベント通知の場合のミニポート ドライバーを入力して、 **uNwError**該当する場合は、適切なメンバー。

次の表は、登録パケット アタッチ、デタッチ パケット原因コードの失敗の値で定義されていると、 *3 gpp TS 24.008 仕様*GSM ベースのネットワーク。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">3 gpp 24.008 原因コード</th>
<th align="left">原因のコードの解釈</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>2-International Mobile IMSI (Subscriber Identity) 隠線消去に不明です</p></td>
<td align="left"><p>SIM またはデバイスがアクティブ化されていません、またはサブスクリプションが期限切れ、ネットワークの非アクティブ化の原因となった。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4-IMSI VLR に不明です</p></td>
<td align="left"><p>ローミング機能がサブスクライブしていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>6-不正な ME</p></td>
<td align="left"><p>MS が盗難にあったレポートのためのネットワークによってブロックされています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>7-GPRS サービスが許可されていません</p></td>
<td align="left"><p>ユーザーには、GPRS サブスクリプションはありません。 ユーザーは、音声接続のサブスクリプションのみを持っています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>8-GPRS および GPRS 以外のサービスが許可されていません</p></td>
<td align="left"><p>GPRS など GPRS 以外のサービスを指定することはできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>11-PLMN が許可されていません</p></td>
<td align="left"><p>サービスは、期限切れのサブスクリプションまたは別の原因により、ネットワークによってブロックされます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>12-場所領域が許可されていません</p></td>
<td align="left"><p>ユーザー サブスクリプションでは、存在する場所 領域のアクセスを許可しません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>13-roaming この場所の領域では使用できません。</p></td>
<td align="left"><p>サブスクリプションが、ローミングを許可しますが、ローミングは、存在する場所 領域では許可されていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>14-GPRS サービスがこの PLMN で許可されていません</p></td>
<td align="left"><p>選択したネットワーク プロバイダーは、ms GPRS サービスを提供していません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>15 - 場所領域内で適切なセル</p></td>
<td align="left"><p>サービスのサブスクリプションがありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>17-ネットワーク エラー</p></td>
<td align="left"><p>登録に失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>22-輻輳</p></td>
<td align="left"><p>ネットワークの混雑により登録が失敗しました。</p></td>
</tr>
</tbody>
</table>

 

たとえば、ネットワークは、ローミングは、[場所] で許可されていないために、非アクティブ化コンテキストのイベントを開始する場合のミニポート ドライバー設定する必要があります、 **uNwError** GSM ベースのネットワーク 3 gpp TS 24.008 原因コードに従って 13 メンバー。

同様のロジックは、CDMA ベースのネットワークで同様に適用する必要があります。 ただし、CDMA ベースのネットワーク エラー コードの標準ではありません。 CDMA ベースのデバイスがネットワークを使用する必要があります-特定のまたはデバイスに固有のエラー コード。

OID 要求に対する非同期応答のミニポート ドライバーの場合、 **RequestId**の NDIS メンバー\_状態\_を示す値構造体が一部として、ミニポート ドライバーに渡された、0 以外の数値*設定*または*クエリ*要求。 ミニポート ドライバーを入力する必要があります、 **uStatus**として適切なメンバー。 たとえば、WWAN\_状態\_成功した場合、または該当するエラー値のいずれか、次のセクションに表示します。 さらに、ミニポート ドライバーを入力して、 **uNwError**メンバー適切かつ使用可能な場所。

### <a name="event-notification-status"></a>イベント通知の状態

次の表は、WWAN\_MB ミニポート ドライバーがで指定できるステータス コード、 **uStatus**の NDIS メンバー\_WWAN\_XXX イベント通知の構造体。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_SUCCESS</p></td>
<td align="left"><p>操作に成功しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_FAILURE</p></td>
<td align="left"><p>操作には、(一般的なエラー) が失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_BUSY</p></td>
<td align="left"><p>デバイスがビジー状態、操作が失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_SIM_NOT_INSERTED</p></td>
<td align="left"><p>デバイスに SIM カードが完全に挿入されなかったため、操作が失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_BAD_SIM</p></td>
<td align="left"><p>SIM カードが無効であると、これ以上使用することはできませんので、操作が失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_PIN_REQUIRED</p></td>
<td align="left"><p>続行する PIN を入力する必要があるため操作に失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_PIN_DISABLED</p></td>
<td align="left"><p>PIN が無効になっているため、操作に失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_NOT_REGISTERED</p></td>
<td align="left"><p>ネットワーク デバイスが登録されていないため、操作が失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_PROVIDERS_NOT_FOUND</p></td>
<td align="left"><p>操作は、ネットワーク プロバイダーが見つかりませんでしたが失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_NO_DEVICE_SUPPORT</p></td>
<td align="left"><p>デバイスは、操作をサポートしていないため、操作が失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_PROVIDER_NOT_VISIBLE</p></td>
<td align="left"><p>サービス プロバイダーが現在表示されていないため、操作が失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_DATA_CLASS_NOT_AVAILABLE</p></td>
<td align="left"><p>要求されたデータ クラスが使用できないため、操作が失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_PACKET_SVC_DETACHED</p></td>
<td align="left"><p>パケットのサービスをデタッチ操作が失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_MAX_ACTIVATED_CONTEXTS</p></td>
<td align="left"><p>アクティブ化されたコンテキストの最大数に達したため、操作が失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_NOT_INITIALIZED</p></td>
<td align="left"><p>デバイスが初期化中にあるため、操作が失敗しました。 デバイスの準備完了状態を変更した後には、操作をやり直してください<strong>WwanReadyStateInitialized</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_VOICE_CALL_IN_PROGRESS</p></td>
<td align="left"><p>音声通話が進行中のため、操作が失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_CONTEXT_NOT_ACTIVATED</p></td>
<td align="left"><p>コンテキストがアクティブでないため、操作に失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_SERVICE_NOT_ACTIVATED</p></td>
<td align="left"><p>操作は、サービスがアクティブ化が失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_INVALID_ACCESS_STRING</p></td>
<td align="left"><p>アクセス文字列が無効であるため、操作が失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_INVALID_USER_NAME_PWD</p></td>
<td align="left"><p>ユーザー名または指定されたパスワードに無効なため、操作に失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_RADIO_POWER_OFF</p></td>
<td align="left"><p>オプションは現在電源オフ操作が失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_INVALID_PARAMETERS</p></td>
<td align="left"><p>無効なパラメーターのため、操作が失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_READ_FAILURE</p></td>
<td align="left"><p>読み取りエラーのため、操作が失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_WRITE_FAILURE</p></td>
<td align="left"><p>書き込みエラーのため、操作が失敗しました。</p></td>
</tr>
</tbody>
</table>

 

次の表では、SMS の特定のステータス値を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_SMS_OPERATION_NOT_ALLOWED</p></td>
<td align="left"><p>操作が許可されていないために、SMS 操作が失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_SMS_MEMORY_FAILURE</p></td>
<td align="left"><p>メモリ エラーのために、SMS の操作が失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_SMS_INVALID_MEMORY_INDEX</p></td>
<td align="left"><p>SMS 操作に失敗しました--無効なメモリのインデックスが原因<em>WwanSmsFlagIndex</em> OID_WWAN_SMS_READ の。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_SMS_UNKNOWN_SMSC_ADDRESS</p></td>
<td align="left"><p>サービス中心の番号が無効であるか、不明な SMS 操作が失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_SMS_NETWORK_TIMEOUT</p></td>
<td align="left"><p>SMS 操作は、ネットワーク タイムアウトのため失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_SMS_MEMORY_FULL</p></td>
<td align="left"><p>SMS 操作は、SMS メッセージ ストアがいっぱいのため失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_SMS_UNKNOWN_ERROR</p></td>
<td align="left"><p>不明なエラー (一般的なエラー) ため、SMS の操作が失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_SMS_FILTER_NOT_SUPPORTED</p></td>
<td align="left"><p>要求フィルターの種類がサポートされていないために、SMS の操作が失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_SMS_MORE_DATA</p></td>
<td align="left"><p>このトランザクションはまだ完全ではありません。 一部のデータが返されたより多くのデータが返されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_SMS_LANG_NOT_SUPPORTED</p></td>
<td align="left"><p>SMS の言語がサポートされていないために、SMS の操作が失敗しました。 これは、CDMA ベースのデバイスのみに適用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_SMS_ENCODING_NOT_SUPPORTED</p></td>
<td align="left"><p>SMS のエンコードはサポートされていないために、SMS 操作が失敗しました。 これは、CDMA ベースのデバイスのみに適用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_SMS_FORMAT_NOT_SUPPORTED</p></td>
<td align="left"><p>SMS の形式がサポートされていないために、SMS の操作が失敗しました。</p></td>
</tr>
</tbody>
</table>

 

**注**  これら WWAN に固有の状態コードでトランザクションを非同期にのみ使用、 **uStatus**の NDIS メンバー\_WWAN\_XXX 構造体。

 

ミニポート ドライバーでは、イベント通知を使用して、MB サービスに最初に、MB デバイスでのオブジェクト状態変更に関する通知 OID 要求を受信します。 MB サービスでは、イベント通知を使用して、そのステート マシンのみを更新します。

NDIS ミニポート ドライバーに送信されるすべての要求をシリアル化、中にミニポート ドライバーが返されないこと、応答と同じ順序で注意します。 これはため、ミニポート ドライバーでキューに置かれた要求を並列で処理される可能性があります。 そのため MB サービスによりを 2 つの要求が互いに依存している場合は、これは送信しません 2 番目の要求、ミニポート ドライバーには、最初の要求が完了するまで。

### <a name="state-change-notification"></a>状態変更通知

一般に、ミニポート ドライバーは、トランザクション通知または不要なイベント通知のいずれかが MB デバイスの更新の状態に関する MB サービスを常に通知する必要があります。 次のシナリオでは、場所のミニポート ドライバーは、更新された状態情報で応答する許可されていない例外があります。 MB サービスは、その他の操作の完了状態から更新された状態を判断できます。

1.  ミニポート ドライバーは、NDIS を送信する必要はありません\_状態\_WWAN\_PIN\_MB サービスが要求を有効にまたは PIN を無効にするために PIN の状態の変更が発生するときに一覧イベントを示す値。

2.  ミニポート ドライバーは OID にトランザクションの応答で更新されたプロビジョニングのコンテキストの一覧を返す必要はありません\_WWAN\_プロビジョニング済み\_コンテキスト*設定*操作。

3.  ミニポート ドライバーが更新された OID をトランザクションの応答で優先プロバイダーの一覧で応答する必要はありません\_WWAN\_優先\_プロバイダー*設定*操作。 MB サービスの初期リストと成功状態を状態に基づいてこの情報を調べる、*設定*操作。

4.  ミニポート ドライバーは、現在 WWAN で応答する必要はありません\_SMS\_OID の構成値\_WWAN\_SMS\_構成*設定*操作。

 

 





