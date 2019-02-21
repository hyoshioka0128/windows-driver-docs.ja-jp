---
title: MB のデータ モデル
description: MB のデータ モデル
ms.assetid: 922b6b55-c332-4721-bbd1-571b0e154df3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc3dd2bed0ba8d236447879c7bacc2445ddbf991
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550712"
---
# <a name="mb-data-model"></a>MB のデータ モデル


MB ドライバー モデルは、MB デバイスの機能の抽象化として定義されているオブジェクトのセットで構成されるデータ モデルを使用します。 各オブジェクトは、一意のオブジェクト識別子 (OID) で識別され、対応する属性のセットによって定義されます。 一連の属性は、データ構造に編成されます。 デバイスを管理するには、MB サービスと MB のミニポート ドライバー Oid と OID 要求と Network Driver Interface Specification (NDIS) によって提供されている指示に基づいてそれらに関連付けられているデータ構造体を交換します。

のみ MB ドライバー モデルで*設定*と*クエリ*OID 要求の操作が使用されます。 MB ドライバー モデルが使用しない*メソッド*操作。 MB ドライバー モデルは、MB デバイスのオブジェクトの状態の変化を示すイベントとトランザクションの通知の両方を使用します。 トランザクションの通知では、非同期のトランザクションの完了も通知します。

次の表には、Oid と関連付けられているデータ構造体として MB ミニポート ドライバーでは、定義されている状態のインジケーターが一覧表示します。 MB のミニポート ドライバーでは、NDIS 6.20 が動作の仕様を必要とするすべての必須全般の Oid を実装する必要があります。 NDIS の一般的な Oid の一覧については、6.x を参照してください[一般的な操作の Oid](https://msdn.microsoft.com/library/windows/hardware/ff552474)します。

さらに、MB ミニポート ドライバーが OID を実装する必要があります\_GEN\_物理\_中の場合でも、NDIS 仕様が実装するためにオプションとして説明します。

構文とセマンティクス MB Oid が次の表に示すは記載[MB 演算のセマンティクス](mb-operational-semantics.md)します。 MB サービスと MB ミニポート ドライバー間の相互作用が記載されて[MB 操作フローチャート](mb-operation-flowcharts.md)します。

## <a name="wwan-specific-oids"></a>WWAN に固有の Oid

| OID と対応するデータ構造体 | 設定操作 |   | クエリ操作 |   | GSM/CDMA |
| ---                                  | ---       | ---       | ---       | ---       |--- |
|                                      | Windows 7 | Windows 8 | Windows 7 | Windows 8 |    |
| [OID\_WWAN\_ドライバー\_CAP](https://msdn.microsoft.com/library/windows/hardware/ff569825)使用[ **NDIS\_WWAN\_ドライバー\_キャップ**](https://msdn.microsoft.com/library/windows/hardware/ff567908) | サポートされない | サポートされない |S | S | GSM、CDMA |
| [OID\_WWAN\_デバイス\_CAP](https://msdn.microsoft.com/library/windows/hardware/ff569824)対応する構造がありません | サポートされない | サポートされない | A | A | GSM、CDMA |
| [OID\_WWAN\_準備\_情報](https://msdn.microsoft.com/library/windows/hardware/ff569833)対応する構造がありません | サポートされている Not がサポートされていません | A | A | GSM、CDMA |
| [OID\_WWAN\_サービス\_アクティベーション](https://msdn.microsoft.com/library/windows/hardware/ff569835)† 使用[ **NDIS\_WWAN\_サービス\_アクティブ化**](https://msdn.microsoft.com/library/windows/hardware/ff567918) | A | A | サポートされない | サポートされない | GSM、CDMA |
| [OID\_WWAN\_ラジオ\_状態](https://msdn.microsoft.com/library/windows/hardware/ff569832)使用[ **NDIS\_WWAN\_設定\_ラジオ\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567925) | A | A | A | A | GSM、CDMA |
| [OID\_WWAN\_PIN](https://msdn.microsoft.com/library/windows/hardware/ff569828)使用[ **NDIS\_WWAN\_設定\_暗証番号 (pin)**](https://msdn.microsoft.com/library/windows/hardware/ff567922) | A | サポートされない | A | サポートされない | GSM、CDMA |
| [OID\_WWAN\_PIN\_一覧](https://msdn.microsoft.com/library/windows/hardware/ff569829)対応する構造がありません | サポートされない | サポートされない | A | A | GSM、CDMA |
| [OID\_WWAN\_PIN\_EX](https://msdn.microsoft.com/library/windows/hardware/hh440095)使用[ **NDIS\_WWAN\_設定\_PIN\_例**](https://msdn.microsoft.com/library/windows/hardware/hh439842) | サポートされない | A | サポートされない | A | GSM、CDMA |
| [OID\_WWAN\_ホーム\_プロバイダー](https://msdn.microsoft.com/library/windows/hardware/ff569826)対応する構造がありません | サポートされない | サポートされない | A | A | GSM、CDMA |
| [OID\_WWAN\_優先\_プロバイダー](https://msdn.microsoft.com/library/windows/hardware/ff569830)† 使用[ **NDIS\_WWAN\_設定\_優先\_プロバイダー**](https://msdn.microsoft.com/library/windows/hardware/ff567923) | A | A | A | A | GSM のみ |
| [OID\_WWAN\_VISIBLE\_プロバイダー](https://msdn.microsoft.com/library/windows/hardware/ff569843)対応する構造がありません | サポートされない | サポートされない | A | A | GSM |
| [OID\_WWAN\_登録\_状態](https://msdn.microsoft.com/library/windows/hardware/ff569834)使用[ **NDIS\_WWAN\_設定\_登録\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567926) | A | A | A | A | CDMA |
| [OID\_WWAN\_信号\_状態](https://msdn.microsoft.com/library/windows/hardware/ff569836)使用[ **NDIS\_WWAN\_設定\_信号\_を示す値**](https://msdn.microsoft.com/library/windows/hardware/ff567928) | A | A | A | A | GSM、CDMA |
| [OID\_WWAN\_パケット\_サービス](https://msdn.microsoft.com/library/windows/hardware/ff569827)使用[ **NDIS\_WWAN\_設定\_パケット\_サービス**](https://msdn.microsoft.com/library/windows/hardware/ff567921) | A | A | A | A | GSM、CDMA |
| [OID\_WWAN\_プロビジョニング済み\_コンテキスト](https://msdn.microsoft.com/library/windows/hardware/ff569831)† を使用して[ **NDIS\_WWAN\_設定\_プロビジョニング済み\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff567924) | A | A | A | A | GSM、CDMA |
| [OID\_WWAN\_CONNECT](https://msdn.microsoft.com/library/windows/hardware/ff569823)使用[ **NDIS\_WWAN\_設定\_コンテキスト\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567920) | A | A | A | A | GSM、CDMA |
| [OID\_WWAN\_SMS\_構成](https://msdn.microsoft.com/library/windows/hardware/ff569837)使用[ **NDIS\_WWAN\_設定\_SMS\_構成**](https://msdn.microsoft.com/library/windows/hardware/ff567929) | A | A | A | A | GSM、CDMA | 
| [OID\_WWAN\_SMS\_読み取り](https://msdn.microsoft.com/library/windows/hardware/ff569839)使用[ **NDIS\_WWAN\_SMS\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff567941) | サポートされない | A | A | A |GSM、CDMA | 
| [OID\_WWAN\_SMS\_送信](https://msdn.microsoft.com/library/windows/hardware/ff569840)使用[ **NDIS\_WWAN\_SMS\_送信**](https://msdn.microsoft.com/library/windows/hardware/ff567943) | A | A | サポートされない | サポートされない | GSM、CDMA |
| [OID\_WWAN\_SMS\_削除](https://msdn.microsoft.com/library/windows/hardware/ff569838)使用[ **NDIS\_WWAN\_SMS\_削除**](https://msdn.microsoft.com/library/windows/hardware/ff567938) | A | A | サポートされない | サポートされない |  GSM、CDMA |
| [OID\_WWAN\_SMS\_状態](https://msdn.microsoft.com/library/windows/hardware/ff569841)使用[ **NDIS\_WWAN\_SMS\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567945) | サポートされない | サポートされない | A | A | GSM、CDMA |
| [OID\_WWAN\_ベンダー\_特定](https://msdn.microsoft.com/library/windows/hardware/ff569842)† はベンダ定義の構造を使用 | A | A | サポートされない | サポートされない | GSM、CDMA |
| [OID\_WWAN\_デバイス\_サービス](https://msdn.microsoft.com/library/windows/hardware/hh440093)対応する構造がありません | サポートされない | サポートされない | サポートされない | A | GSM、CDMA |
| [OID\_WWAN\_購読\_デバイス\_サービス\_イベント](https://msdn.microsoft.com/library/windows/hardware/hh440096)使用[ **NDIS\_WWAN\_購読\_デバイス\_サービス\_イベント**](https://msdn.microsoft.com/library/windows/hardware/hh439843) | サポートされない | A | サポートされない | サポートされない | GSM、CDMA |
| [OID\_WWAN\_AUTH\_チャレンジ](https://msdn.microsoft.com/library/windows/hardware/hh440092)使用[ **NDIS\_WWAN\_AUTH\_チャレンジ**](https://msdn.microsoft.com/library/windows/hardware/hh439833) | サポートされない | サポートされない | サポートされない | A | GSM、CDMA |
| [OID\_WWAN\_USSD](https://msdn.microsoft.com/library/windows/hardware/hh440100)使用[ **NDIS\_WWAN\_USSD\_要求**](https://msdn.microsoft.com/library/windows/hardware/hh439846) | サポートされない | A | サポートされない | サポートされない | GSM |
| [OID\_WWAN\_デバイス\_サービス\_コマンド](https://msdn.microsoft.com/library/windows/hardware/hh440094)使用[ **NDIS\_WWAN\_デバイス\_サービス\_コマンド**](https://msdn.microsoft.com/library/windows/hardware/hh439836) | サポートされない | A | サポートされない | A| GSM、CDMA |

> [!NOTE]
> 前の表を次の注意事項が適用されます: † ミニポート ドライバーがサポートできる省略可能な Oid を表します。 省略可能な Oid をサポートしていないミニポート ドライバー返す必要があるいないに OID\_GEN\_サポートされている\_一覧。
>
> † 表す OID をサポートできる必要に応じて、GSM ベースのデバイスをサポートするミニポート ドライバー\_WWAN\_プロビジョニング済み\_コンテキストの設定し、操作をクエリします。 CDMA ベースのデバイスをサポートするミニポート ドライバーは、OID をサポートできます必要に応じて\_WWAN\_プロビジョニング済み\_コンテキストは、CDMA ベースのデバイスで単純な IP を報告するための操作をクエリ (WWAN\_CTRL\_キャップ\_CDMA\_単純\_IP)。
>
> ミニポート ドライバーでは、すべて省略できない Oid をサポートする必要があります。 MB サービスは、すべての必須の Oid は報告されません任意のミニポート ドライバーを無視することができます。
> 
> "A"と"S"セットおよびクエリ操作列上の表では、OID 要求を完了するため、トランザクションの性質を反映します。"A"の略非同期トランザクションと"S"の同期トランザクションです。
>
> 上記の表に、データ構造には、操作の Oid を設定して、データ同期のクエリ操作の Oid を返しますが対応しています。
> 
> 一般的な可変長のリストのデータ構造と呼ばれる次の Oid 共有[ **WWAN\_一覧\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff571208)対応するデータ構造で。
> -   OID\_WWAN\_準備\_情報
> -   OID\_WWAN\_優先\_プロバイダー
> -   OID\_WWAN\_VISIBLE\_プロバイダー
> -   OID\_WWAN\_プロビジョニング済み\_コンテキスト
> -   OID\_WWAN\_SMS\_読み取り 

## <a name="wwan-specific-indications-corresponding-data-structures-and-os-revisions"></a>WWAN に固有の問題、対応するデータ構造、および OS のバージョン

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Indication</strong>と<strong>対応するデータ構造体</strong></p></td>
<td align="left"><p><strong>Windows 7 のリビジョン</strong></p>
<p><strong>Windows 8 のリビジョン</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567845" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_CAPS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567845)"><strong>NDIS_STATUS_WWAN_DEVICE_CAPS</strong></a></p>
<p>使用して<a href="https://msdn.microsoft.com/library/windows/hardware/ff567907" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_CAPS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567907)"> <strong>NDIS_WWAN_DEVICE_CAPS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_CAPS_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_CAPS_REVISION_2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567856" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_READY_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567856)"><strong>NDIS_STATUS_WWAN_READY_INFO</strong></a></p>
<p>uses <a href="https://msdn.microsoft.com/library/windows/hardware/ff567916" data-raw-source="[&lt;strong&gt;NDIS_WWAN_READY_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567916)"><strong>NDIS_WWAN_READY_INFO</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_READY_INFO_REVISION_1</p>
<p>NDIS_WWAN_READY_INFO_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567855" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_RADIO_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567855)"><strong>NDIS_STATUS_WWAN_RADIO_STATE</strong></a></p>
<p>使用して<a href="https://msdn.microsoft.com/library/windows/hardware/ff567915" data-raw-source="[&lt;strong&gt;NDIS_WWAN_RADIO_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567915)"> <strong>NDIS_WWAN_RADIO_STATE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_RADIO_STATE_REVISION_1</p>
<p>NDIS_WWAN_RADIO_STATE_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567851" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PIN_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567851)"><strong>NDIS_STATUS_WWAN_PIN_INFO</strong></a></p>
<p>uses <a href="https://msdn.microsoft.com/library/windows/hardware/ff567911" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PIN_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567911)"><strong>NDIS_WWAN_PIN_INFO</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PIN_INFO_REVISION_1</p>
<p>NDIS_WWAN_PIN_INFO_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567852" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PIN_LIST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567852)"><strong>NDIS_STATUS_WWAN_PIN_LIST</strong></a></p>
<p>使用して<a href="https://msdn.microsoft.com/library/windows/hardware/ff567912" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PIN_LIST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567912)"> <strong>NDIS_WWAN_PIN_LIST</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PIN_LIST_REVISION_1</p>
<p>NDIS_WWAN_PIN_LIST_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567858" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SERVICE_ACTIVATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567858)"><strong>NDIS_STATUS_WWAN_SERVICE_ACTIVATION</strong></a>†</p>
<p>使用して<a href="https://msdn.microsoft.com/library/windows/hardware/ff567919" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SERVICE_ACTIVATION_STATUS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567919)"> <strong>NDIS_WWAN_SERVICE_ACTIVATION_STATUS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SERVICE_ACTIVATION_STATUS_REVISION_1</p>
<p>NDIS_WWAN_SERVICE_ACTIVATION_STATUS_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567848" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_HOME_PROVIDER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567848)"><strong>NDIS_STATUS_WWAN_HOME_PROVIDER</strong></a></p>
<p>使用して<a href="https://msdn.microsoft.com/library/windows/hardware/ff567909" data-raw-source="[&lt;strong&gt;NDIS_WWAN_HOME_PROVIDER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567909)"> <strong>NDIS_WWAN_HOME_PROVIDER</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_HOME_PROVIDER_REVISION_1</p>
<p>NDIS_WWAN_HOME_PROVIDER_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567853" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PREFERRED_PROVIDERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567853)"><strong>NDIS_STATUS_WWAN_PREFERRED_PROVIDERS</strong></a>†</p>
<p>uses <a href="https://msdn.microsoft.com/library/windows/hardware/ff567913" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PREFERRED_PROVIDERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567913)"><strong>NDIS_WWAN_PREFERRED_PROVIDERS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PREFERRED_PROVIDERS_REVISION_1</p>
<p>NDIS_WWAN_PREFERRED_PROVIDERS_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567866" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567866)"><strong>NDIS_STATUS_WWAN_VISIBLE_PROVIDERS</strong></a></p>
<p>使用して<a href="https://msdn.microsoft.com/library/windows/hardware/ff567948" data-raw-source="[&lt;strong&gt;NDIS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567948)"> <strong>NDIS_WWAN_VISIBLE_PROVIDERS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_VISIBLE_PROVIDERS_REVISION_1</p>
<p>NDIS_WWAN_VISIBLE_PROVIDERS_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567857" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_REGISTER_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567857)"><strong>NDIS_STATUS_WWAN_REGISTER_STATE</strong></a></p>
<p>使用して<a href="https://msdn.microsoft.com/library/windows/hardware/ff567917" data-raw-source="[&lt;strong&gt;NDIS_WWAN_REGISTRATION_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567917)"> <strong>NDIS_WWAN_REGISTRATION_STATE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_REGISTRATION_STATE_REVISION_1</p>
<p>NDIS_WWAN_REGISTRATION_STATE_REVISION_2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567859" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SIGNAL_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567859)"><strong>NDIS_STATUS_WWAN_SIGNAL_STATE</strong></a></p>
<p>使用して<a href="https://msdn.microsoft.com/library/windows/hardware/ff567931" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SIGNAL_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567931)"> <strong>NDIS_WWAN_SIGNAL_STATE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SIGNAL_STATE_REVISION_1</p>
<p>NDIS_WWAN_SIGNAL_STATE_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567850" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PACKET_SERVICE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567850)"><strong>NDIS_STATUS_WWAN_PACKET_SERVICE</strong></a></p>
<p>使用して<a href="https://msdn.microsoft.com/library/windows/hardware/ff567910" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PACKET_SERVICE_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567910)"> <strong>NDIS_WWAN_PACKET_SERVICE_STATE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PACKET_SERVICE_STATE_REVISION_1</p>
<p>NDIS_WWAN_PACKET_SERVICE_STATE_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567854" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567854)"><strong>NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS</strong></a></p>
<p>使用して<a href="https://msdn.microsoft.com/library/windows/hardware/ff567914" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PROVISIONED_CONTEXTS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567914)"> <strong>NDIS_WWAN_PROVISIONED_CONTEXTS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PROVISIONED_CONTEXTS_REVISION_1</p>
<p>NDIS_WWAN_PROVISIONED_CONTEXTS_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567843" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_CONTEXT_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567843)"><strong>NDIS_STATUS_WWAN_CONTEXT_STATE</strong></a></p>
<p>使用して<a href="https://msdn.microsoft.com/library/windows/hardware/ff567906" data-raw-source="[&lt;strong&gt;NDIS_WWAN_CONTEXT_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567906)"> <strong>NDIS_WWAN_CONTEXT_STATE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_CONTEXT_STATE_REVISION_1</p>
<p>NDIS_WWAN_CONTEXT_STATE_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567860" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_CONFIGURATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567860)"><strong>NDIS_STATUS_WWAN_SMS_CONFIGURATION</strong></a></p>
<p>使用して<a href="https://msdn.microsoft.com/library/windows/hardware/ff567935" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_CONFIGURATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567935)"> <strong>NDIS_WWAN_SMS_CONFIGURATION</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_CONFIGURATION_REVISION_1</p>
<p>NDIS_WWAN_SMS_CONFIGURATION_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567862" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_RECEIVE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567862)"><strong>NDIS_STATUS_WWAN_SMS_RECEIVE</strong></a></p>
<p>使用して<a href="https://msdn.microsoft.com/library/windows/hardware/ff567942" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_RECEIVE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567942)"> <strong>NDIS_WWAN_SMS_RECEIVE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_RECEIVE_REVISION_1</p>
<p>NDIS_WWAN_SMS_RECEIVE_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567863" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_SEND&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567863)"><strong>NDIS_STATUS_WWAN_SMS_SEND</strong></a></p>
<p>使用して<a href="https://msdn.microsoft.com/library/windows/hardware/ff567944" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_SEND_STATUS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567944)"> <strong>NDIS_WWAN_SMS_SEND_STATUS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_SEND_STATUS_REVISION_1</p>
<p>NDIS_WWAN_SMS_SEND_STATUS_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567861" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_DELETE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567861)"><strong>NDIS_STATUS_WWAN_SMS_DELETE</strong></a></p>
<p>使用して<a href="https://msdn.microsoft.com/library/windows/hardware/ff567940" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_DELETE_STATUS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567940)"> <strong>NDIS_WWAN_SMS_DELETE_STATUS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_DELETE_STATUS_REVISION_1</p>
<p>NDIS_WWAN_SMS_DELETE_STATUS_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567864" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_STATUS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567864)"><strong>NDIS_STATUS_WWAN_SMS_STATUS</strong></a></p>
<p>使用して<a href="https://msdn.microsoft.com/library/windows/hardware/ff567945" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_STATUS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567945)"> <strong>NDIS_WWAN_SMS_STATUS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_SMS_STATUS_REVISION_1</p>
<p>NDIS_WWAN_SMS_STATUS_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567865" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VENDOR_SPECIFIC&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567865)"><strong>NDIS_STATUS_WWAN_VENDOR_SPECIFIC</strong></a>†</p>
<p>ベンダー定義の構造体を使用します。</p></td>
<td align="left"><p>なし</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439822" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_USSD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439822)"><strong>NDIS_STATUS_WWAN_USSD</strong></a></p>
<p>使用して<a href="https://msdn.microsoft.com/library/windows/hardware/hh439844" data-raw-source="[&lt;strong&gt;NDIS_WWAN_USSD_EVENT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439844)"> <strong>NDIS_WWAN_USSD_EVENT</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_USSD_EVENT_REVISION_1</p>
<p>NDIS_WWAN_USSD_EVENT_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh846210" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh846210)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS</strong></a></p>
<p>使用して<a href="https://msdn.microsoft.com/library/windows/hardware/hh846214" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh846214)"> <strong>NDIS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_SERVICES_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_SERVICES_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh846205" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh846205)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE</strong></a></p>
<p>使用して<a href="https://msdn.microsoft.com/library/windows/hardware/hh439838" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_SERVICE_RESPONSE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439838)"> <strong>NDIS_WWAN_DEVICE_SERVICE_RESPONSE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_SERVICE_RESPONSE_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_SERVICE_RESPONSE_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh846204" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh846204)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT</strong></a></p>
<p>使用して<a href="https://msdn.microsoft.com/library/windows/hardware/hh439837" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_SERVICE_EVENT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439837)"> <strong>NDIS_WWAN_DEVICE_SERVICE_EVENT</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_SERVICE_EVENT_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_SERVICE_EVENT_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh846209" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh846209)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION</strong></a></p>
<p>使用して<a href="https://msdn.microsoft.com/library/windows/hardware/hh439839" data-raw-source="[&lt;strong&gt;NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439839)"> <strong>NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION_REVISION_1</p>
<p>NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION_REVISION_1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439821" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_AUTH_RESPONSE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439821)"><strong>NDIS_STATUS_WWAN_AUTH_RESPONSE</strong></a></p>
<p>使用して<a href="https://msdn.microsoft.com/library/windows/hardware/hh439834" data-raw-source="[&lt;strong&gt;NDIS_WWAN_AUTH_RESPONSE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439834)"> <strong>NDIS_WWAN_AUTH_RESPONSE</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_AUTH_RESPONSE_REVISION_1</p>
<p>NDIS_WWAN_AUTH_RESPONSE_REVISION_1</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh846212" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SET_HOME_PROVIDER_COMPLETE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh846212)"><strong>NDIS_STATUS_WWAN_SET_HOME_PROVIDER_COMPLETE</strong></a></p>
<p>uses <a href="https://msdn.microsoft.com/library/windows/hardware/hh439841" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SET_HOME_PROVIDER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439841)"><strong>NDIS_WWAN_SET_HOME_PROVIDER</strong></a></p></td>
<td align="left"><p>なし</p>
<p>NDIS_WWAN_HOME_PROVIDER_REVISION_2</p></td>
</tr>
</tbody>
</table>

> [!NOTE]
> 前の表を次の注意事項が適用されます: † ミニポート ドライバーがサポートできる省略可能なインジケーターを表します。 ミニポート ドライバーでは、省略可能な OID をサポートする場合、ミニポート ドライバーもをサポートするように、対応するを示す値を認識します。 

## <a name="wwan-specific-indication-support-for-gsm-cdma-and-unsolicited-indications"></a>GSM、CDMA、一方的な兆候を WWAN 固有を示す値のサポート

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>示す値</strong></p></td>
<td align="left"><p><strong>GSM</strong></p></td>
<td align="left"><p><strong>CDMA</strong></p></td>
<td align="left"><p><strong>要請されていません。</strong></p>
<p><strong>indication</strong></p>
<p><strong>許可しますか。</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567845" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_CAPS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567845)"><strong>NDIS_STATUS_WWAN_DEVICE_CAPS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567856" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_READY_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567856)"><strong>NDIS_STATUS_WWAN_READY_INFO</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567855" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_RADIO_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567855)"><strong>NDIS_STATUS_WWAN_RADIO_STATE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567851" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PIN_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567851)"><strong>NDIS_STATUS_WWAN_PIN_INFO</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567852" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PIN_LIST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567852)"><strong>NDIS_STATUS_WWAN_PIN_LIST</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567858" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SERVICE_ACTIVATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567858)"><strong>NDIS_STATUS_WWAN_SERVICE_ACTIVATION</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567848" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_HOME_PROVIDER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567848)"><strong>NDIS_STATUS_WWAN_HOME_PROVIDER</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567853" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PREFERRED_PROVIDERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567853)"><strong>NDIS_STATUS_WWAN_PREFERRED_PROVIDERS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567866" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567866)"><strong>NDIS_STATUS_WWAN_VISIBLE_PROVIDERS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567857" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_REGISTER_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567857)"><strong>NDIS_STATUS_WWAN_REGISTER_STATE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567859" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SIGNAL_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567859)"><strong>NDIS_STATUS_WWAN_SIGNAL_STATE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567850" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PACKET_SERVICE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567850)"><strong>NDIS_STATUS_WWAN_PACKET_SERVICE</strong></a></p>
<p>使用して<a href="https://msdn.microsoft.com/library/windows/hardware/ff567910" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PACKET_SERVICE_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567910)"> <strong>NDIS_WWAN_PACKET_SERVICE_STATE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567854" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567854)"><strong>NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567843" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_CONTEXT_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567843)"><strong>NDIS_STATUS_WWAN_CONTEXT_STATE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567860" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_CONFIGURATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567860)"><strong>NDIS_STATUS_WWAN_SMS_CONFIGURATION</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567862" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_RECEIVE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567862)"><strong>NDIS_STATUS_WWAN_SMS_RECEIVE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567863" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_SEND&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567863)"><strong>NDIS_STATUS_WWAN_SMS_SEND</strong></a></p>
<p>使用して<a href="https://msdn.microsoft.com/library/windows/hardware/ff567944" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SMS_SEND_STATUS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567944)"> <strong>NDIS_WWAN_SMS_SEND_STATUS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567861" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_DELETE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567861)"><strong>NDIS_STATUS_WWAN_SMS_DELETE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567864" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SMS_STATUS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567864)"><strong>NDIS_STATUS_WWAN_SMS_STATUS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567865" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VENDOR_SPECIFIC&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567865)"><strong>NDIS_STATUS_WWAN_VENDOR_SPECIFIC</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439822" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_USSD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439822)"><strong>NDIS_STATUS_WWAN_USSD</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh846210" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh846210)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh846205" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh846205)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh846204" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh846204)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh846209" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh846209)"><strong>NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439821" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_AUTH_RESPONSE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439821)"><strong>NDIS_STATUS_WWAN_AUTH_RESPONSE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh846212" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_SET_HOME_PROVIDER_COMPLETE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh846212)"><strong>NDIS_STATUS_WWAN_SET_HOME_PROVIDER_COMPLETE</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
</tbody>
</table> 

## <a name="multi-carrier-specific-oids"></a>特定の Oid を複数の通信事業者

マルチ キャリア モードをサポートする NDIS 6.30 ミニポート ドライバーに、次の変更が適用されます。 ミニポート ドライバーのマルチ キャリア モードをサポートし、前の表を参照してくださいはしないかどうか。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>OID</strong>と<strong>Windows 8 の対応するデータ構造体</strong></p></td>
<td align="left"><p><strong>クエリ操作</strong></p></td>
<td align="left"><p><strong>設定操作</strong></p></td>
<td align="left"><p><strong>GSM/CDMA</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569826" data-raw-source="[OID_WWAN_HOME_PROVIDER](https://msdn.microsoft.com/library/windows/hardware/ff569826)">OID_WWAN_HOME_PROVIDER</a></p>
<p>uses <a href="https://msdn.microsoft.com/library/windows/hardware/hh439841" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SET_HOME_PROVIDER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439841)"><strong>NDIS_WWAN_SET_HOME_PROVIDER</strong></a></p></td>
<td align="left"><p>A</p></td>
<td align="left"><p>A</p></td>
<td align="left"><p>GSM、CDMA</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569830" data-raw-source="[OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS](https://msdn.microsoft.com/library/windows/hardware/ff569830)">OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS</a></p>
<p>使用して<a href="https://msdn.microsoft.com/library/windows/hardware/hh831866" data-raw-source="[&lt;strong&gt;NDIS_WWAN_SET_PREFERRED_MULTICARRIER_PROVIDERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh831866)"> <strong>NDIS_WWAN_SET_PREFERRED_MULTICARRIER_PROVIDERS</strong></a>します。 <strong>PreferredListHeader.ElementType</strong>に設定する必要があります<strong>WwanStructProvider2</strong> WWAN_PROVIDER2 であり、構造体。</p></td>
<td align="left"><p>A</p></td>
<td align="left"><p>A</p></td>
<td align="left"><p>GSM、CDMA</p></td>
</tr>
</tbody>
</table> 

## <a name="multi-carrier-specific-indications-corresponding-data-structures-and-os-revisions"></a>複数の通信事業者の特定がない、対応するデータ構造体、および OS のバージョン

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Indication</strong>と<strong>対応するデータ構造体</strong></p></td>
<td align="left"><p><strong>Windows 8 のリビジョン</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567848" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_HOME_PROVIDER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567848)"><strong>NDIS_STATUS_WWAN_HOME_PROVIDER</strong></a></p>
<p>uses <a href="https://msdn.microsoft.com/library/windows/hardware/hh439840" data-raw-source="[&lt;strong&gt;NDIS_WWAN_HOME_PROVIDER2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439840)"><strong>NDIS_WWAN_HOME_PROVIDER2</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_HOME_PROVIDER_REVISION_2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh846211" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh846211)"><strong>NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS</strong></a></p>
<p>uses <a href="https://msdn.microsoft.com/library/windows/hardware/hh831864" data-raw-source="[&lt;strong&gt;NDIS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh831864)"><strong>NDIS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS_REVISION_1. <strong>PreferredListHeader.ElementType</strong>に設定する必要があります<strong>WwanStructProvider2</strong>し、一覧は WWAN_PROVIDER2 構造体を含める必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567866" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567866)"><strong>NDIS_STATUS_WWAN_VISIBLE_PROVIDERS</strong></a></p>
<p>使用して<a href="https://msdn.microsoft.com/library/windows/hardware/ff567948" data-raw-source="[&lt;strong&gt;NDIS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567948)"> <strong>NDIS_WWAN_VISIBLE_PROVIDERS</strong></a></p></td>
<td align="left"><p>NDIS_WWAN_VISIBLE_PROVIDERS_REVISION_1. <strong>VisibleListHeader.ElementType</strong>に設定する必要があります<strong>WwanStructProvider2</strong>し、一覧は WWAN_PROVIDER2 構造体を含める必要があります。</p></td>
</tr>
</tbody>
</table> 

## <a name="multi-carrier-specific-indication-support-for-gsm-cdma-and-unsolicited-indications"></a>GSM、CDMA、一方的な兆候をマルチ キャリア具体的な表示のサポート

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Indication</strong>と<strong>対応するデータ構造体</strong></p></td>
<td align="left"><p><strong>GSM</strong></p></td>
<td align="left"><p><strong>CDMA</strong></p></td>
<td align="left"><p><strong>要請されていません。</strong></p>
<p><strong>indication</strong></p>
<p><strong>許可しますか。</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567848" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_HOME_PROVIDER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567848)"><strong>NDIS_STATUS_WWAN_HOME_PROVIDER</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh846211" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh846211)"><strong>NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>Y</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567866" data-raw-source="[&lt;strong&gt;NDIS_STATUS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567866)"><strong>NDIS_STATUS_WWAN_VISIBLE_PROVIDERS</strong></a></p>
<p>使用して<a href="https://msdn.microsoft.com/library/windows/hardware/ff567948" data-raw-source="[&lt;strong&gt;NDIS_WWAN_VISIBLE_PROVIDERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567948)"> <strong>NDIS_WWAN_VISIBLE_PROVIDERS</strong></a></p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>N</p></td>
</tr>
</tbody>
</table>
