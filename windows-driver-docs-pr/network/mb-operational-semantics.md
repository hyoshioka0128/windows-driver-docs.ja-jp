---
title: MB 操作のセマンティクス
description: MB 操作のセマンティクス
ms.assetid: 5f04b7fd-3df3-4efa-bb26-c7f4cd3c9ebd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2c26d2ec41b6d136864fdb9752af3560e09b9b9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844277"
---
# <a name="mb-operational-semantics"></a>MB 操作のセマンティクス


### <a name="asynchronous-transactions"></a>非同期トランザクション

MB ドライバーモデルは、NDIS 6.x に用意されている非同期通知メカニズムを使用して、MB サービスとミニポートドライバー間の非ブロッキング操作セマンティクスを前提としています。 このメカニズムにより、MB サービスは、現在の操作の完了を待たずに、処理のために引き続き OID 要求をミニポートドライバーに送信できます。

非同期トランザクションは、最初の要求から始まり、要求ステータス応答、最後のトランザクション通知によって完了する3方向ハンドシェイクです。 要求の状態の応答は、ミニポートドライバーが要求を受信したことのみを確認するため、一時的なものです。 フォローアップの非同期通知はトランザクションの完了を通知するトランザクションです。 ミニポートドライバーは、状態コードだけでなく、結果のデータもトランザクションによって返されます。

### <a name="asynchronous-set-and-query-requests"></a>非同期*セット*と*クエリ*要求

MB サービスによって使用される*設定*および*クエリ*OID 要求の多くは、非同期的に処理されます。 Oid 要求の*設定*と*クエリ*の詳細については、「 [**NDIS\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)」を参照してください。 [MB データモデル](mb-data-model.md)に関するトピックの「WWAN 固有の oid」の表は、どの oid が非同期に処理されるかを示しています。

次の図は、MB サービスとミニポートドライバー間の非同期*クエリ*トランザクションの相互作用シーケンスを示しています。 太字のラベルは OID 識別子 (トランザクションフロー制御) を表し、通常のテキストのラベルは OID 構造内の重要なフラグを表します。

![モバイルブロードバンドサービスとミニポートドライバー間の非同期クエリトランザクションの相互作用シーケンスを示す図](images/wwanasyncquerytransaction.png)

3方向ハンドシェイクは、*クエリ*と*set*要求の両方で同じです。

[Oid\_WWAN\_ドライバー\_cap](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-driver-caps)の場合を除き、他のすべての MB 固有の oid 要求は、ミニポートドライバーと MB サービス間の情報交換に関する非同期トランザクション機構に従います。その他の注意事項を次に示します。:

-   ミニポートドライバーは、無効な OID 要求など、エラー状態に関する OID 要求を直ちに失敗させる必要があります。

-   ミニポートドライバーは、イベント通知構造の**uStatus**メンバーに指定されている正しいエラーコード (たとえば、WWAN\_STATUS\_XXX) を使用して、wwan 固有のエラー条件を返す必要があります。 また、必要に応じて、 **uStatus**メンバーに続くメンバーをミニポートドライバーで適切に入力する必要があります。 たとえば、ミニポートドライバーは、使用可能な場合は、 [**NDIS\_WWAN\_コンテキスト\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_context_state)構造体の**Contextstate. uNwError**メンバーに入力する必要があります。 ただし、Pin に関連する Oid の処理中にエラーが発生した場合、ミニポートドライバーには、 [**NDIS\_\_\_WWAN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info)の**Pininfo. PinState**メンバーで指定するための現在の pin の状態情報が必ずしも含まれるとは限りません。

-   ミニポートドライバーは、すべての非同期 OID 要求に対して一時的な応答として必要な\_を示す\_NDIS\_STATUS を返す必要があります。

-   ミニポートドライバーは、他の原因からの OID 要求によって発生したデバイスの状態の変更を区別できる必要があります。 ミニポートドライバーは、OID 要求によって発生した状態の変更に対してトランザクション通知を送信する必要があります。また、他の原因から状態の変化に対して、一方的なイベント通知を送信します。

-   ミニポートドライバーは、カーネルモードメモリの管理を担当します。ただし、MB サービスは最初に要求のためにメモリを割り当てます。 MB サービスがミニポートドライバーから応答を受信すると、そのサービスは OID 要求に割り当てられたユーザーモードのメモリを解放する可能性があります。

次の図は、MB サービスとミニポートドライバー間の非同期*セット*トランザクションの相互作用シーケンスを示しています。 太字のラベルは OID 識別子 (トランザクションフロー制御) を表し、通常のテキストのラベルは OID 構造内の重要なフラグを表します。

![モバイルブロードバンドサービスとミニポートドライバー間の非同期セットトランザクションの相互作用シーケンスを示す図](images/wwanasyncsettransaction.png)

### <a name="asynchronous-response"></a>非同期応答

(Windows Vista でリリースされた) *ndis 6.0 仕様*では、ミニポートドライバーが、トランザクションの非同期の性質をミニポートの MB サービスに伝達するために、新しいステータスコード、NDIS\_ステータス\_表示\_必要であることを示していました。OID 要求に対するドライバーの一時的な応答。

[「Mb インターフェイスの概要](mb-interface-overview.md)」で説明したように、mb サービスは、mb のミニポートドライバーによって割り当てられたカーネルモードのメモリに直接アクセスすることはできません。 カーネルモードメモリに格納されている実行結果は、WMI や[NDIS フィルタードライバー](ndis-filter-drivers2.md)など、一部の仲介によって、MB サービスで使用できるようになります。 そのため、 [**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)関数の呼び出しがトランザクションの通知で返された後、割り当てられたカーネルモードのメモリをミニポートドライバーが解放できます。

次の手順では、ミニポートドライバーと MB サービスが従う必要があるハンドシェイク手順について説明します。

### <a name="mb-miniport-driver-procedure"></a>MB ミニポートドライバーの手順

ミニポートドライバーは、OID 要求を受信すると、次の手順を実行します。

1.  OID 要求に関連付けられている[**NDIS\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)データ構造の内容をコピーするには、カーネルモードでメモリを割り当てます。

2.  要求のパラメーターの中で、OID 要求構造の**RequestId** **メンバーと要求元**メンバーもコピーされていることを確認します。 これらのメンバーは、後でトランザクション*通知*で使用されます。

3.  要求された状態の応答\_\_を返して、ミニポートドライバーが要求を非同期に完了することを MB サービスに通知する、\_の仮 NDIS の状態を返します。

4.  操作が完了したら、必要に応じて、ローカルまたはドライバーで割り当てられたメモリに結果を格納します。

5.  [**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)関数を呼び出して、未処理の操作が完了したことを MB サービスに通知します。 ミニポートドライバーは、次のように、NDIS\_ステータス\_表示構造のメンバーに入力する必要があります。
    1.  **StatusCode**メンバーを状態通知の種類に設定します。 たとえば、NDIS\_STATUS\_WWAN\_XXX のようになります。
    2.  **Destinationhandle**メンバーを、ミニポートドライバーが対応する oid 要求を受信したときに、NDIS\_OID\_要求データ構造で受信した要求**ハンドル**メンバーに設定します。
    3.  **Requestid**メンバーを、ミニポートドライバーが対応する oid 要求を受信したときに、NDIS\_OID\_要求状態構造の**requestid**メンバーと一致するように設定します。
    4.  **Statusbuffer**と**statusbuffer**のメンバーが、ミニポートドライバーで割り当てられたメモリとメモリバッファーのサイズをそれぞれ指すように設定します。 このメモリバッファーには、完了した操作の結果が格納されます。
    5.  操作が正常に完了した場合は、 **uStatus**メンバーを WWAN\_STATUS\_SUCCESS に設定します。 それ以外の場合は、 **uStatus**メンバーを適切な WWAN\_ステータス\_XXX 値に設定して、エラーの種類を示します。

6.  関数呼び出しが返されると、ミニポートドライバーは OID 要求に割り当てられたメモリを解放する必要があります。

### <a name="mb-service-procedure"></a>MB サービスプロシージャ

MB サービスは、次の手順を使用して非同期トランザクションを処理します。

1.  OID データ構造に基づいて要求のバッファーメモリを割り当てます。 データ構造体のメンバーに適切な値を入力します。

2.  OID 要求の OID データ構造をポイントする**Informationbuffer**メンバーを使用して[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)関数を呼び出し、ミニポートドライバーが応答するのを待ちます。

3.  NDIS\_状態\_通知されると、ミニポートドライバーからの必須の一時的な応答\_示され、MB サービスは**RequestId**を保存し、割り当てられたメモリを解放して、トランザクションをオープンとしてマークします。 この時点で、MB サービスは、以降の OID 要求と通知を自由に処理できます。

4.  StatusCode\_ステータス\_WWAN\_XXX の通知が**StatusCode**値として受信されたら、 **RequestId**が open とマークされたトランザクションのいずれかと一致するかどうかを確認します。 一致するものがある場合は、サービスによってトランザクションが閉じられます。 一致するものが見つからない場合は、通知を要請されていないイベント通知として扱います。

5.  **Statusbuffer**メンバーで返されたデータを処理し、必要に応じて状態を MB サービスに変更します。

### <a name="indications"></a>兆候

次の2種類の WWAN 固有の*インジケーター*でミニポートドライバーが生成できます。

-   MB デバイスでのオブジェクトの状態の変更に起因するイベント通知。

-   非同期操作の完了を通知するトランザクション通知。

どちらの場合も、ミニポートドライバーは NdisMIndicateStatusEx 関数を呼び出す必要があります。

### <a name="event-notification"></a>イベント通知

イベント通知は、ミニポートドライバーが状態変更イベントとして MB サービスに対して通知を事前に送信しているという意味では要請されません。 状態の変化は、MB サービス以外のエンティティからのアクションが原因で発生します。 MB サービスでは、ミニポートドライバーが変更の原因を検出できることを前提としています。

すべての WWAN 固有のイベント通知について、ミニポートドライバーは、NDIS\_STATUS\_構造体の**RequestId**メンバーを0に設定する必要があります。 **StatusCode**メンバーは、MB デバイス内のどのオブジェクトが変更されたかを指定します。 ミニポートドライバーは、このオブジェクトを次のいずれかの値に設定できます。

[**NDIS\_ステータス\_WWAN\_デバイス\_CAP**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-caps)

[**NDIS\_ステータス\_WWAN\_準備完了\_情報**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ready-info)

[**NDIS\_ステータス\_WWAN\_ラジオ\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-radio-state)

[**NDIS\_ステータス\_WWAN\_PIN\_情報**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-info)

[**NDIS\_ステータス\_WWAN\_PIN\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-pin-list)

[**NDIS\_ステータス\_WWAN\_ホーム\_プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-home-provider)

[**NDIS\_ステータス\_WWAN\_優先\_プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-providers)

[**NDIS\_ステータス\_WWAN\_表示されている\_プロバイダ**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-visible-providers)

[**NDIS\_ステータス\_WWAN\_登録\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-register-state)

[**NDIS\_ステータス\_WWAN\_パケット\_サービス**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-packet-service)

[**NDIS\_ステータス\_WWAN\_シグナル\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-signal-state)

[**NDIS\_ステータス\_WWAN\_コンテキスト\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-context-state)

[**NDIS\_ステータス\_WWAN\_プロビジョニングされた\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-provisioned-contexts)

[**NDIS\_ステータス\_WWAN\_サービス\_アクティブ化**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-service-activation)

[**NDIS\_ステータス\_WWAN\_SMS\_構成**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-configuration)

[**NDIS\_ステータス\_WWAN\_SMS\_受信**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-receive)

[**NDIS\_ステータス\_WWAN\_SMS\_送信**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-send)

[**NDIS\_ステータス\_WWAN\_SMS\_削除**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-delete)

[**NDIS\_ステータス\_WWAN\_SMS\_の状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sms-status)

[**NDIS\_状態\_WWAN\_ベンダー\_固有**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-vendor-specific)

また、MB サービスでは、NDIS からの他のイベント通知を処理することもできます。 これらの非 MB イベント通知は、必ずしも**RequestId**値がゼロに設定されている必要があるとは限りません。

### <a name="transactional-notifications"></a>トランザクション通知

ミニポートドライバーは、トランザクション通知を使用して、非同期トランザクションが完了したことを MB サービスに通知します。また、MB サービスはトランザクション通知を使用して、開いているトランザクションを閉じ、そのステートマシンを更新します。

MB サービスは、開いているトランザクションを閉じることができるように、トランザクション通知を要求します。 これは、非同期トランザクションでの、MB サービスとミニポートドライバー間の3方向ハンドシェイクの最終的な交換です。 トランザクション通知に示されている、NDIS\_\_STATUS の**RequestId**メンバーの値は0以外である必要があります。これは、同じトランザクション内の対応する要求からコピーされます。

非同期メカニズムが正常に機能するためには、NDIS\_STATUS\_構造体の**RequestId**メンバーを正しく設定する必要があります。 MB サービスは、 **RequestId**値が一意であり、すべての未処理の要求の間で0以外の値を持つことを保証します。 ミニポートドライバーは、対応する表示で同じ**RequestId**値を返す必要があります。これは、MB サービスが開いているトランザクションに示されている情報を関連付ける*ためのもの*です。

### <a name="status-indication-structure"></a>状態を示す構造

指定された OID 要求と要請されていないイベント通知構造の非同期応答の両方で、 *statusbuffer*パラメーターの**statusbuffer**メンバーが指す次の構造体メンバーをに[**共有します。NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex):

```C++
typedef struct _NDIS_WWAN_XXX {
  NDIS_OBJECT_HEADER Header;
  WWAN_STATUS uStatus;
  ULONG uNwError;//Optional. Only used for network operations.
  WWAN_XXX XxxStruct;
} NDIS_WWAN_XXX, *PNDIS_WWAN_XXX;
```

NDIS\_ステータス\_示す構造体の**RequestId**メンバーの値が0の場合は、それが要請されていないイベント通知であり、いつでも発生する可能性があります。

*Set*または*query* OID 要求の返された表示の**uStatus**メンバーが、wwan\_STATUS\_SUCCESS に一致しない場合、関連付けられている NDIS\_WWAN\_XXX 構造体のメンバーは有効である必要はありません。

ネットワークイベントに基づく要請されていないイベント通知の場合は、必要に応じて、 **uNwError**メンバーにミニポートドライバーを入力する必要があります。

次の表に、GSM ベースのネットワークの*3GPP TS 24.008 仕様*で定義されているコードエラー値の原因となる、登録、パケット接続、およびパケットデタッチの例を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">3GPP 24.008 の原因コード</th>
<th align="left">原因コードの解釈</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>2-国際モバイルサブスクライバー Id (IMSI) が HLR で不明</p></td>
<td align="left"><p>SIM またはデバイスがアクティブ化されていないか、サブスクリプションの有効期限が切れているため、ネットワークの非アクティブ化が発生しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>VLR に通知では、4-IMSI は不明です。</p></td>
<td align="left"><p>ローミング機能がサブスクライブされていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>6-無効な ME</p></td>
<td align="left"><p>レポートが盗まれたため、ネットワークによってブロックされました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>7-GPRS サービスは使用できません</p></td>
<td align="left"><p>ユーザーには GPRS サブスクリプションがありません。 ユーザーは、音声接続のサブスクリプションのみを持っています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>8-GPRS および GPRS 以外のサービスは使用できません</p></td>
<td align="left"><p>GPRS および GPRS 以外のサービスは許可されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>11 PLMN 使用できません</p></td>
<td align="left"><p>サブスクリプションが期限切れになったか、別の原因により、サービスがネットワークによってブロックされています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>12-場所領域は使用できません</p></td>
<td align="left"><p>ユーザーサブスクリプションでは、[現在の場所] 領域でのアクセスが許可されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>13-この場所ではローミングは許可されていません</p></td>
<td align="left"><p>サブスクリプションはローミングを許可しますが、現在の場所ではローミングは許可されていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>14-このプランでは、GPRS サービスは許可されていません</p></td>
<td align="left"><p>選択したネットワークプロバイダーは、MS に GPRS サービスを提供していません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>15-ロケーション領域に適切なセルがありません</p></td>
<td align="left"><p>サービスのサブスクリプションがありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>17-ネットワークエラー</p></td>
<td align="left"><p>登録に失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>22-輻輳</p></td>
<td align="left"><p>ネットワークの混雑により、登録に失敗しました。</p></td>
</tr>
</tbody>
</table>

 

たとえば、ローミングが [場所] 領域で許可されていないためにネットワークが非アクティブ化コンテキストイベントを開始する場合、ミニポートドライバーは、GSM ベースのネットワークの 3GPP TS 24.008 原因コードに従って、 **uNwError**メンバーを13に設定する必要があります。

同様のロジックは、CDMA ベースのネットワークにも適用する必要があります。 ただし、CDMA ベースのネットワークエラーコードには標準はありません。 CDMA ベースのデバイスでは、ネットワーク固有またはデバイス固有のエラーコードを使用する必要があります。

ミニポートドライバーが OID 要求に対して非同期応答を行う場合、NDIS の\_ステータス\_表示構造体の**RequestId**メンバーは、*セット*またはクエリの一部としてミニポートドライバーに渡された0以外の数値になります。要求。 ミニポートドライバーは、必要に応じて**uStatus**メンバーに入力する必要があります。 たとえば、次のセクションに示すように、WWAN\_STATUS\_SUCCESS、または適切なエラー値が表示されます。 さらに、ミニポートドライバーは、適切であり、使用可能な場所に**uNwError**メンバーを入力する必要があります。

### <a name="event-notification-status"></a>イベント通知の状態

次の表は、(MB) ミニポートドライバーが NDIS\_WWAN\_XXX イベント通知構造の**uStatus**メンバーで指定できる、wwan\_のステータスコードを示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_SUCCESS</p></td>
<td align="left"><p>操作は成功しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_FAILURE</p></td>
<td align="left"><p>操作が失敗しました (一般的なエラー)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_BUSY</p></td>
<td align="left"><p>デバイスがビジー状態のため、操作に失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_SIM_NOT_INSERTED</p></td>
<td align="left"><p>SIM カードがデバイスに完全に挿入されていないため、操作に失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_BAD_SIM</p></td>
<td align="left"><p>SIM カードが正しくないため、これ以上使用できないため、操作に失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_PIN_REQUIRED</p></td>
<td align="left"><p>操作を実行できませんでした。続行するには、PIN を入力する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_PIN_DISABLED</p></td>
<td align="left"><p>PIN が無効になっているため、操作に失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_NOT_REGISTERED</p></td>
<td align="left"><p>デバイスがネットワークに登録されていないため、操作に失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_PROVIDERS_NOT_FOUND</p></td>
<td align="left"><p>ネットワークプロバイダーが見つからなかったため、操作に失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_NO_DEVICE_SUPPORT</p></td>
<td align="left"><p>デバイスで操作がサポートされていないため、操作に失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_PROVIDER_NOT_VISIBLE</p></td>
<td align="left"><p>サービスプロバイダーが現在表示されていないため、操作に失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_DATA_CLASS_NOT_AVAILABLE</p></td>
<td align="left"><p>要求されたデータクラスが使用できなかったため、操作に失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_PACKET_SVC_DETACHED</p></td>
<td align="left"><p>パケットサービスがデタッチされているため、操作に失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_MAX_ACTIVATED_CONTEXTS</p></td>
<td align="left"><p>アクティブ化されたコンテキストの最大数に達したため、操作に失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_NOT_INITIALIZED</p></td>
<td align="left"><p>デバイスが初期化処理中のため、操作に失敗しました。 デバイスの状態が<strong>WwanReadyStateInitialized</strong>に変更された後、操作を再試行してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_VOICE_CALL_IN_PROGRESS</p></td>
<td align="left"><p>音声通話が進行中のため、操作に失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_CONTEXT_NOT_ACTIVATED</p></td>
<td align="left"><p>コンテキストがアクティブ化されていないため、操作に失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_SERVICE_NOT_ACTIVATED</p></td>
<td align="left"><p>サービスがアクティブ化されていないため、操作に失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_INVALID_ACCESS_STRING</p></td>
<td align="left"><p>アクセス文字列が無効であるため、操作に失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_INVALID_USER_NAME_PWD</p></td>
<td align="left"><p>指定されたユーザー名またはパスワードが無効であるため、操作に失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_RADIO_POWER_OFF</p></td>
<td align="left"><p>ラジオが現在電源オフになっているため、操作に失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_INVALID_PARAMETERS</p></td>
<td align="left"><p>無効なパラメーターのため、操作に失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_READ_FAILURE</p></td>
<td align="left"><p>読み取りエラーが発生したため、操作に失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_WRITE_FAILURE</p></td>
<td align="left"><p>書き込みエラーのため、操作に失敗しました。</p></td>
</tr>
</tbody>
</table>

 

次の表は、SMS 固有のステータス値を示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_SMS_OPERATION_NOT_ALLOWED</p></td>
<td align="left"><p>この操作は許可されていないため、SMS 操作に失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_SMS_MEMORY_FAILURE</p></td>
<td align="left"><p>メモリエラーのため、SMS 操作に失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_SMS_INVALID_MEMORY_INDEX</p></td>
<td align="left"><p>無効なメモリインデックスが原因で SMS 操作が失敗しました-- <em>Wwansmsflagindex</em> for OID_WWAN_SMS_READ。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_SMS_UNKNOWN_SMSC_ADDRESS</p></td>
<td align="left"><p>サービスセンター番号が無効であるか不明であるため、SMS 操作に失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_SMS_NETWORK_TIMEOUT</p></td>
<td align="left"><p>ネットワークがタイムアウトしたため、SMS 操作に失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_SMS_MEMORY_FULL</p></td>
<td align="left"><p>Sms メッセージストアがいっぱいのため、SMS 操作に失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_SMS_UNKNOWN_ERROR</p></td>
<td align="left"><p>不明なエラーが発生したため、SMS 操作に失敗しました (一般的なエラー)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_SMS_FILTER_NOT_SUPPORTED</p></td>
<td align="left"><p>要求されたフィルターの種類がサポートされていないため、SMS 操作に失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_SMS_MORE_DATA</p></td>
<td align="left"><p>このトランザクションはまだ完了していません。 いくつかのデータが返され、さらに多くのデータが返されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_SMS_LANG_NOT_SUPPORTED</p></td>
<td align="left"><p>Sms 言語がサポートされていないため、SMS 操作に失敗しました。 これは、CDMA ベースのデバイスにのみ適用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WWAN_STATUS_SMS_ENCODING_NOT_SUPPORTED</p></td>
<td align="left"><p>Sms エンコードがサポートされていないため、SMS 操作に失敗しました。 これは、CDMA ベースのデバイスにのみ適用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WWAN_STATUS_SMS_FORMAT_NOT_SUPPORTED</p></td>
<td align="left"><p>Sms 形式がサポートされていないため、SMS 操作に失敗しました。</p></td>
</tr>
</tbody>
</table>

 

これらの WWAN 固有の状態コードは、NDIS\_WWAN\_XXX 構造体の**uStatus**メンバーの非同期トランザクションに対してのみ使用されます **。  **

 

ミニポートドライバーは、最初に OID 要求を受信しなくても、mb デバイスでのオブジェクトの状態の変化について MB サービスに通知するために、イベント通知を使用します。 MB サービスは、イベント通知を使用して、そのステートマシンのみを更新します。

ミニポートドライバーに送信されるすべての要求が NDIS によってシリアル化されるのに対し、ミニポートドライバーは応答を同じ順序で返さない場合があることに注意してください。 これは、ミニポートドライバーでキューに置かれた要求が並列処理される可能性があるためです。 このため、MB サービスにより、2つの要求が互いに依存している場合、ミニポートドライバーが最初の要求を完了するまで2番目の要求は送信されません。

### <a name="state-change-notification"></a>状態変更通知

一般に、ミニポートドライバーは、トランザクション通知または要請されていないイベント通知を使用して、mb デバイスの更新状態を常に MB サービスに通知する必要があります。 次のシナリオでは、ミニポートドライバーが更新された状態情報で応答しないという例外がいくつかあります。 MB サービスは、他の操作の完了ステータスから更新された状態を特定できます。

1.  Pin を有効または無効にするように MB サービスが要求したために PIN の状態の変更が発生したときに、ミニポートドライバーは NDIS\_ステータス\_WWAN\_\_PIN を送信する必要はありません。

2.  ミニポートドライバーは、トランザクション応答内のプロビジョニングされたコンテキストの更新された一覧を、\_コンテキストの*設定*操作をプロビジョニングされた\_\_WWAN に返す必要はありません。

3.  ミニポートドライバーは、OID\_WWAN に対するトランザクション応答内の優先プロバイダーの更新された一覧を使用して応答する必要はありません。\_優先\_プロバイダーの*設定*操作です。 MB サービスは、*設定*操作の初期リストと成功の状態に基づいてこの情報を決定できます。

4.  ミニポートドライバーは、現在の WWAN\_SMS\_構成値を OID\_WWAN\_SMS\_構成*設定*操作で応答する必要はありません。

 

 





