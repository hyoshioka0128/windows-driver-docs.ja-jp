---
title: WDI_TLV_TCP_SET_OFFLOAD_PARAMETERS
description: WDI_TLV_TCP_SET_OFFLOAD_PARAMETERS は、OID_WDI_SET_TCP_OFFLOAD_PARAMETERS 用のミニポートアダプターの TCP オフロード機能を含む TLV です。
ms.assetid: 1DE1114A-E718-473F-B0EB-92AEFA4E7F13
ms.date: 07/18/2017
keywords:
- WDI_TLV_TCP_SET_OFFLOAD_PARAMETERS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: eafde637f99e6a226fd16f14ef4b6bc548b2e1a5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841728"
---
# <a name="wdi_tlv_tcp_set_offload_parameters"></a>WDI\_TLV\_TCP\_設定\_オフロード\_パラメーター


WDI\_TLV\_TCP\_設定\_オフロード\_パラメーターは TLV で、OID 用のミニポートアダプターの TCP オフロード機能が含まれています\_\_\_[tcp\_オフロード\_パラメーターを設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-tcp-offload-parameters)します。

## <a name="tlv-type"></a>TLV 型


0Xf2 よう

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>タスクバーの検索ボックスに</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT8</td>
<td>ミニポートアダプターの IPv4 チェックサム設定。
<p>有効な値は次のとおりです。</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - ミニポートドライバーは、現在の設定を変更することはできません。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_DISABLED</strong> - 無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_ENABLED_RX_DISABLED</strong> - 送信が有効になっていて、受信が無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RX_ENABLED_TX_DISABLED</strong> - 受信用に有効になっており、送信が無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_ENABLED</strong> - 送信と受信が有効になっています。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>TCP パケットの IPv4 チェックサム設定。
<p>有効な値は次のとおりです。</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - ミニポートドライバーは、現在の設定を変更することはできません。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_DISABLED</strong> - 無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_ENABLED_RX_DISABLED</strong> - 送信が有効になっていて、受信が無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RX_ENABLED_TX_DISABLED</strong> - 受信用に有効になっており、送信が無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_ENABLED</strong> - 送信と受信が有効になっています。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>UDP パケットの IPv4 チェックサム設定。
<p>有効な値は次のとおりです。</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - ミニポートドライバーは、現在の設定を変更することはできません。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_DISABLED</strong> - 無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_ENABLED_RX_DISABLED</strong> - 送信が有効になっていて、受信が無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RX_ENABLED_TX_DISABLED</strong> - 受信用に有効になっており、送信が無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_ENABLED</strong> - 送信と受信が有効になっています。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>TCP パケットの IPv6 チェックサム設定。
<p>有効な値は次のとおりです。</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - ミニポートドライバーは、現在の設定を変更することはできません。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_DISABLED</strong> - 無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_ENABLED_RX_DISABLED</strong> - 送信が有効になっていて、受信が無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RX_ENABLED_TX_DISABLED</strong> - 受信用に有効になっており、送信が無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_ENABLED</strong> - 送信と受信が有効になっています。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>UDP パケットの IPv6 チェックサム設定。
<p>有効な値は次のとおりです。</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - ミニポートドライバーは、現在の設定を変更することはできません。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_DISABLED</strong> - 無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_ENABLED_RX_DISABLED</strong> - 送信が有効になっていて、受信が無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RX_ENABLED_TX_DISABLED</strong> - 受信用に有効になっており、送信が無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_ENABLED</strong> - 送信と受信が有効になっています。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>Large Send Offload version 1 (LSOV1) 設定です。
<p>有効な値は次のとおりです。</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - ミニポートドライバーは、現在の設定を変更することはできません。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_LSOV1_ENABLED</strong> - LSOV1 が有効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_LSOV1_DISABLED</strong> - LSOV1 が無効になっています。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>インターネットプロトコルセキュリティ (IPsec) オフロード設定。
<p>有効な値は次のとおりです。</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - ミニポートドライバーは、現在の設定を変更することはできません。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV1_DISABLED</strong> - IPsec オフロードが無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV1_AH_ENABLED</strong> -、送信と受信に対して IPsec オフロード認証ヘッダー (AH) 機能を有効にする必要があります。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV1_ESP_ENABLED</strong> -、IPsec オフロードカプセル化セキュリティペイロード (ESP) 機能を送信と受信に対して有効にする必要があります。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV1_AH_AND_ESP_ENABLED</strong> -、送信と受信に対して IPsec オフロード AH と ESP 機能が有効になっています。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>IPv4 Large Send Offload version 2 (LSOV2) 設定です。
<p>有効な値は次のとおりです。</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - ミニポートドライバーは、現在の設定を変更することはできません。</li>
<li>IPv4 の<strong>NDIS_OFFLOAD_PARAMETERS_LSOV2_ENABLED</strong> - LSOV2 が有効になっています。</li>
<li>IPv4 の<strong>NDIS_OFFLOAD_PARAMETERS_LSOV2_DISABLED</strong> - LSOV2 が無効になっています。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>IPv6 Large Send Offload version 2 (LSOV2) 設定。
<p>有効な値は次のとおりです。</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - ミニポートドライバーは、現在の設定を変更することはできません。</li>
<li>IPv6 の<strong>NDIS_OFFLOAD_PARAMETERS_LSOV2_ENABLED</strong> - LSOV2 が有効になっています。</li>
<li>IPv6 の<strong>NDIS_OFFLOAD_PARAMETERS_LSOV2_DISABLED</strong> - LSOV2 が無効になっています。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>IPv4 接続のオフロード設定です。
<p>有効な値は次のとおりです。</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - ミニポートドライバーは、現在の設定を変更することはできません。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>IPv6 接続のオフロード設定です。
<p>有効な値は次のとおりです。</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - ミニポートドライバーは、現在の設定を変更することはできません。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>IPv4 の受信セグメント合体状態を示します。
<p>有効な値は次のとおりです。</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - RSC の状態が変更されていません。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RSC_ENABLED</strong> - RSC の状態が有効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RSC_DISABLED</strong> - RSC の状態が無効になっています。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>IPv6 の受信セグメント合体状態を示します。
<p>有効な値は次のとおりです。</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - RSC の状態が変更されていません。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RSC_ENABLED</strong> - RSC の状態が有効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RSC_DISABLED</strong> - RSC の状態が無効になっています。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>値は、フラグのビットごとの OR です。 0に設定する必要があります。 現在定義されているフラグはありません。</td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>IPv6 と IPv4 の両方をサポートするミニポートアダプターのインターネットプロトコルセキュリティ (IPsec) オフロードバージョン2設定。 IPv6 と IPv4 の両方のサポートの設定を指定します。
<p>有効な値は次のとおりです。</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - ミニポートドライバーは、現在の設定を変更することはできません。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_DISABLED</strong> - IPsec オフロードバージョン2が無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_AH_ENABLED</strong> -、送信と受信に対して IPsec オフロードバージョン2認証ヘッダー (AH) 機能を有効にする必要があります。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_ESP_ENABLED</strong> -、IPsec オフロードバージョン2のカプセル化セキュリティペイロード (ESP) 機能は、送信と受信に対して有効にする必要があります。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_AH_AND_ESP_ENABLED</strong> - IPsec オフロードバージョン 2 AH および ESP の機能が送信と受信に対して有効になっています。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>IPv4 をサポートし、IPv6 をサポートしていないミニポートアダプターのインターネットプロトコルセキュリティ (IPsec) オフロードバージョン2設定。 ミニポートドライバーが IPv6 をサポートしている場合、IPsecV2 メンバーは IPv4 設定を指定し、このメンバーは使用されません。
<p>有効な値は次のとおりです。</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - ミニポートドライバーは、現在の設定を変更することはできません。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_DISABLED</strong> - IPsec オフロードバージョン2が無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_AH_ENABLED</strong> -、送信と受信に対して IPsec オフロードバージョン2認証ヘッダー (AH) 機能を有効にする必要があります。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_ESP_ENABLED</strong> -、IPsec オフロードバージョン2のカプセル化セキュリティペイロード (ESP) 機能は、送信と受信に対して有効にする必要があります。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_AH_AND_ESP_ENABLED</strong> - IPsec オフロードバージョン 2 AH および ESP の機能が送信と受信に対して有効になっています。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>カプセル化されたパケットタスクオフロード。 プロトコルドライバーは、このフィールドを次のいずれかの値に設定します。
<p></p>
<ul>
<li><strong>NDIS_OFFLOAD_SET_NO_CHANGE</strong> (0)-nvgre タスクオフロードの状態は変更されていません。</li>
<li><strong>NDIS_OFFLOAD_SET_ON</strong> (1)-nvgre タスクのオフロードを有効にします。</li>
<li><strong>NDIS_OFFLOAD_SET_OFF</strong> (2)-nvgre タスクのオフロードを無効にします。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>カプセル化の種類。 このフィールドは、カプセル化されたパケットタスクオフロードが<strong>NDIS_OFFLOAD_SET_ON</strong>に設定されている場合にのみ有効です。 カプセル化されたパケットタスクのオフロードメンバーが<strong>NDIS_OFFLOAD_SET_ON</strong>に設定されていない場合、このメンバーは0になります。 プロトコルドライバーでは、カプセル化の種類を、必要なカプセル化の型に対応するフラグのビットごとの OR に設定する必要があります。 次のフラグから選択できます。
<p></p>
<ul>
<li><strong>NDIS_ENCAPSULATION_TYPE_GRE_MAC</strong> (0x00000001)-GRE MAC カプセル化 (Nvgre) を指定します。</li>
</ul></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_オフロード\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)

[OID\_WDI\_設定\_TCP\_オフロード\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-tcp-offload-parameters)

 

 




