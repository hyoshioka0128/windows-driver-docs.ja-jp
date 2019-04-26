---
title: 複数の無線アクセス テクノロジの実装に関する IHV ガイダンス
description: このトピックでは、Windows の複数の無線アクセス テクノロジ (RAT) および複数の演算子のサポートを実装の詳細情報を提供します。
ms.assetid: 17BB2478-F98D-4AE6-A62D-F65E2E1DCDFF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a53128bdde33dc24ccefd68f9fa611fc891680b7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349519"
---
# <a name="ihv-guidance-for-implementing-multimode-and-multicarrier-capable-mb-devices"></a>マルチモードおよびマルチキャリア対応 MB デバイスの実装に関する IHV ガイダンス


このトピックでは、Windows の複数の無線アクセス テクノロジ (RAT) および複数の演算子のサポートを実装の詳細情報を提供します。 これを補足するもの、 [USB NCM モバイル ブロード バンド インターフェイス モデル (MBIM) V1.0 仕様](https://go.microsoft.com/fwlink/p/?linkid=320791)マルチモードおよび multicarrier のシナリオをサポートするために必要な Cid の概要を説明します。

このトピックの情報に適用されます。

-   Windows 8

## <a name="supporting-multimode-devices-with-firmware-switching"></a>ファームウェアの切り替えによるマルチモードのデバイスのサポート


このトピックでは、Windows で複数の無線アクセス テクノロジ (RAT) および複数の演算子のサポートを実装するためを ihv 向けガイダンスを示します。 仕様の最も関連するセクションの簡単な概要を以下に示します。

マルチモード ネットワークには、複数の Rat または携帯電話のクラスがあります。 および multicarrier のデバイスでは、同じデバイス内の複数のネットワーク プロバイダーをサポートします。 マルチモード ネットワーク サポートされている多くのネットワークのいずれかのことができます。

このドキュメントで多くの場所では必須および multicarrier のプロバイダーは、CID が処理の一部がホーム プロバイダーとしてセット-できる必要があります、および multicarrier デバイスによって報告されます。 このセクションでは、プロバイダーは、ホーム プロバイダーとして設定可能なかどうかを判断する方法について説明します。 ホーム プロバイダーとプロバイダーを設定する機能は表示されず、ファームウェアのサポート、プロバイダーのプロバイダーを登録するには、SIM またはそれと同等のことなどに依存しているデバイスでは多くの要因によって異なります。 その他の要因である可能性があります。 デバイスでは、設定可能なホーム プロバイダーとして報告および multicarrier のプロバイダーのデバイスの要件を満たしていることを確認する必要があります。

## <a name="1041-cidmbimdevicecaps"></a>10.4.1 CID\_MBIM\_デバイス\_キャップ


対応のデバイスの MBIM bmCellularClass の複数のサポートされている方法で携帯電話にクラスが報告されます\_デバイス\_キャップとしてで指定されているテーブル 10-13 の仕様。 MBIM で MBIMCtrlCapsMultiCarrier マスクを使用して複数の運送業者のサポートもレポート\_CTRL\_キャップ (表 10 ~ 13)。

通信事業者の 1 つマルチモードのデバイスは、GSM デバイスと同様に動作する必要があります。 このようなデバイスは、CDMA に設定することはできません、MBIM で機能に関連する\_デバイス\_CAP\_情報。

## <a name="1046-cidmbimhomeprovider"></a>10.4.6 CID\_MBIM\_ホーム\_プロバイダー


ホーム プロバイダーを設定することで指定されている**10.3.6.4 します。**

## <a name="1048-cidmbimvisibleproviders"></a>10.4.8 CID\_MBIM\_VISIBLE\_プロバイダー


表示されているプロバイダー CID には、ホストが必要かどうかを指定するアクション フィールドが含まれます。

1.  値 0 で、デバイスがホーム プロバイダーの現在のコンテキストでフル スキャンを実行します。
2.  値 1、デバイスをホーム プロバイダーとして設定できる表示および multicarrier のプロバイダーを検索するクエリが対象です。 デバイスは、フル スキャン、部分的なスキャン、または静的なリストを使用してこれを行うことができます。 プロバイダーは、MBIM としてタグ付けするか、マルチの優先\_プロバイダー\_状態\_優先\_マルチ仕様のプロバイダーが表示される結果で指定されている表 10 34 として。

デバイスが位置情報に基づいて、表示および multicarrier プロバイダーの静的な一覧を報告プログラム CID を使用して\_MBIM\_場所\_については、リストはその場所への有効なプロバイダーを含めるだけです。 その MCC (Mobile 国コード) で表される場所は現在、デバイスでプログラムを作成する場所と異なる場合、デバイスとして上記のルールの拡張機能は、現在登録されているプロバイダーはレポートでする必要がありますされません。

## <a name="1049-cidmbimregisterstate"></a>10.4.9 CID\_MBIM\_登録\_状態


デバイスが MBIM の dwCurrentCellularClass フィールドを使用して、現在の移動体通信クラスを示します\_登録\_仕様の状態 10-48 します。

## <a name="10430-cidmbimdeviceservices"></a>10.4.30 CID\_MBIM\_デバイス\_サービス


および multicarrier のデバイスは、UUID を報告するために必要な\_(後述) マルチ デバイス サービスには、この CID 応答します。

通信事業者の 1 つマルチモードのデバイスは、UUID をレポートする必要はありません\_この CID への応答および MULTICARRIER デバイス サービス。

## <a name="10439-cidmbimmulticarrierproviders"></a>10.4.39 CID\_MBIM\_マルチ\_プロバイダー


デバイスは、この CID を使用して、現在を報告し、優先および multicarrier のプロバイダーを追加しました。 デバイスが MBIMCtrlCapsMultiCarrier をサポートしている場合、この CID はサポートされています。 ないおよび multicarrier 優先プロバイダーを設定すると、ホスト プロバイダーは、ホーム プロバイダーとして設定可能なことが必要です。 デバイスが、ホーム プロバイダーとして設定できるおよび multicarrier の優先プロバイダーを返す必要がありますのみ、ホストによって一覧が照会されたとき。

次の図は、デバイス、ホストで指定された場所のヒントに基づく、現在のモードからの切り替えの手順のシーケンス図を提供します。 操作には、デバイスのサービス、デバイスから追加情報を取得または設定するには以下の説明の使用が必要です。 1 つの特定の要件は、バス転落前に、デバイスからの保留中の通知を回復する機会がホストに提供するかをデバイスが確認する必要があります。 ダイアグラムには、時間の境界とさまざまな操作のパフォーマンスの予測値も指定します。

![デバイス、ホストで指定された場所のヒントに基づく、現在のモードからの切り替えの手順。](images/cid-mbim-multicarrier-providers.png)

## <a name="multi-carrier-device-service"></a>通信事業者のマルチ デバイス サービス


IHV デバイスが実装して、CID が照会すると、次のデバイス サービスをレポート\_MBIM\_デバイス\_サービス。 既存の既知のサービスは、セクション 10.1 NCM MBIM 仕様で定義されます。 次のサービス定義に拡張されています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">サービス名</th>
<th align="left">UUID</th>
<th align="left">UUID 値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>複数の通信事業者</p></td>
<td align="left"><p>UUID_MULTICARRIER</p></td>
<td align="left"><p>8b569648- 628d-4653-9b9f- 1025404424e1</p></td>
</tr>
</tbody>
</table>

 

UUID の次の Cid を定義する具体的には、\_および MULTICARRIER デバイス サービス。

<table>
<colgroup>
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">CID</th>
<th align="left">コマンド コード</th>
<th align="left">Query</th>
<th align="left">Set</th>
<th align="left">event</th>
<th align="left">InformationBuffer ペイロードを設定します。</th>
<th align="left">クエリ InformationBuffer ペイロード</th>
<th align="left">完了 InformationBuffer ペイロード</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>CID_MBIM_MULTICARRIER_CAPABILITIES</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Y</p></td>
<td align="left"><p>N</p></td>
<td align="left"><p>N</p></td>
<td align="left"><p>N/A</p></td>
<td align="left"><p>N/A</p></td>
<td align="left"><p>MBIM_MULTICARRIER_CAPABILITIES</p></td>
</tr>
<tr class="even">
<td align="left"><p>CID_MBIM_LOCATION_INFO</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>Y</p></td>
<td align="left"><p>Y</p></td>
<td align="left"><p>N</p></td>
<td align="left"><p>MBIM_LOCATION_INFO</p></td>
<td align="left"><p>N/A</p></td>
<td align="left"><p>MBIM_LOCATION_INFO</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CID_MBIM_MULTICARRIER_CURRENT_CID_LIST</p></td>
<td align="left"><p>3</p></td>
<td align="left"><p>Y</p></td>
<td align="left"><p>N</p></td>
<td align="left"><p>N</p></td>
<td align="left"><p>N/A</p></td>
<td align="left"><p>UUID</p></td>
<td align="left"><p>MBIM_MULTICARRIERMODE_CURRENT_CID_LIST</p></td>
</tr>
</tbody>
</table>

 

## <a name="cidmbimmulticarriercapabilities"></a>CID\_MBIM\_マルチ\_機能


コマンドは、デバイスのマルチ キャリア機能、MB に関する情報を返します。 ファームウェア再起動、および対応デバイスの削除/到着を必要とするデバイスは、適切なユーザー エクスペリエンスを提供するホストを有効にする適切なフラグを使用してヒントを持つホストを提供する必要があります。

クエリ = **MBIM で InformationBuffer\_コマンド\_MSG は使用されません。MBIM\_マルチ\_InformationBuffer MBIM で機能が返される\_コマンド\_完了**

設定 =**サポートされていません。**

要請されていないイベント =**サポートされていません。**

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">MBIM_MC_FLAGS_NONE</th>
<th align="left">0 h</th>
<th align="left">フラグが設定されていません</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>MBIM_MC_FLAGS_STATIC_SCAN</p></td>
<td align="left"><p>1 時間</p></td>
<td align="left"><p>完全なネットワークのスキャンからのスキャン結果に表示されているプロバイダーの報告結果が取得されないことを示します。 結果は、ハードコーディングされたリストから取得できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MBIM_MC_FLAGS_¬¬FW_REQUIRES_REBOOT</p></td>
<td align="left"><p>2 時間</p></td>
<td align="left"><p>デバイスには、サイクルを強化し、スイッチのファームウェアに再起動が必要であることを示します。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Offset</th>
<th align="left">サイズ</th>
<th align="left">フィールド</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>dwCapabilities</p></td>
<td align="left"><p>MBIM_MULTICARRIER_FLAGS から機能を返します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="cidmbimlocationinfo"></a>CID\_MBIM\_場所\_情報


コマンドは、クエリ、ホストの現在の場所情報の設定に使用されます。 これは、機能は、現在のユーザーの場所に関連するものを静的 (物理スキャンされません) 表示されているプロバイダーの一覧をフィルター処理する必要がある場合、デバイスに便利です。

クエリ = **MBIM で InformationBuffer\_コマンド\_MSG は使用されません。MBIM\_場所\_InformationBuffer MBIM で情報が返される\_コマンド\_完了**

設定 = **MBIM で InformationBuffer\_コマンド\_MSG には MBIM が含まれています\_場所\_情報**

要請されていないイベント =**サポートされていません。**

ホストで指定された国コードは Windows で使用可能な地理的場所 GEOID に基づいて構築します。 詳細については、次を参照してください。[テーブルの地理的な場所 (Windows)](https://msdn.microsoft.com/library/windows/desktop/dd374073)します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Offset</th>
<th align="left">サイズ</th>
<th align="left">フィールド</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>Country</p></td>
<td align="left"><p>地理的な場所は、GEOID に基づいています。</p></td>
</tr>
</tbody>
</table>

 

## <a name="cidmbimmulticarriercurrentcidlist"></a>CID\_MBIM\_マルチ\_現在\_CID\_一覧


このコマンドは、現在デバイス サービスによって想定 Cid をクエリに使用されます。

クエリ = **MBIM で InformationBuffer\_コマンド\_メッセージは、デバイス サービス用の UUID。MBIM\_MULTICARRIERMODE\_現在\_CID\_InformationBuffer MBIM で一覧が返される\_コマンド\_完了**

設定 =**サポートされていません。**

要請されていないイベント =**サポートされていません。**

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Offset</th>
<th align="left">サイズ</th>
<th align="left">フィールド</th>
<th align="left">種類</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>CidCount</p></td>
<td align="left"><p>UINT32</p></td>
<td align="left"><p>Cid がこのデバイスのサービスのサポートの数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p></p></td>
<td align="left"><p>DataBuffer</p></td>
<td align="left"><p>DATABUFFER</p></td>
<td align="left"><p>CidList:Cid がこのデバイスのサービスのサポートの一覧です。 このリストのエントリの CID カウント数が必要があります。 各 CID は型は UINT32 です。</p></td>
</tr>
</tbody>
</table>

 

 

 





