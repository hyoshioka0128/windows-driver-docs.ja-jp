---
title: WDI_TLV_TCP_SET_OFFLOAD_PARAMETERS
description: WDI_TLV_TCP_SET_OFFLOAD_PARAMETERS は、OID_WDI_SET_TCP_OFFLOAD_PARAMETERS のミニポート アダプターの TCP オフロード機能を含む TLV です。
ms.assetid: 1DE1114A-E718-473F-B0EB-92AEFA4E7F13
ms.date: 07/18/2017
keywords:
- WDI_TLV_TCP_SET_OFFLOAD_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: fb8119b7da3fca7f705e0773e8ea4280f5dfb872
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357316"
---
# <a name="wditlvtcpsetoffloadparameters"></a>WDI\_TLV\_TCP\_設定\_オフロード\_パラメーター


WDI\_TLV\_TCP\_設定\_オフロード\_パラメーターはミニポート アダプターの TCP オフロード機能を含む TLV [OID\_WDI\_セット\_TCP\_オフロード\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-tcp-offload-parameters)します。

## <a name="tlv-type"></a>TLV 型


0xf2 の後ろ

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>型</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT8</td>
<td>ミニポート アダプターの IPv4 チェックサムの設定です。
<p>有効な値は次のとおりです。</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> -ミニポート ドライバーでは、現在の設定を変更しないでください。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_DISABLED</strong> -無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_ENABLED_RX_DISABLED</strong> -に対応した送信と受信を無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RX_ENABLED_TX_DISABLED</strong> -に対応した受信と送信を無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_ENABLED</strong> -送信を有効になっていると受信します。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>TCP パケットの IPv4 チェックサムの設定。
<p>有効な値は次のとおりです。</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> -ミニポート ドライバーでは、現在の設定を変更しないでください。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_DISABLED</strong> -無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_ENABLED_RX_DISABLED</strong> -に対応した送信と受信を無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RX_ENABLED_TX_DISABLED</strong> -に対応した受信と送信を無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_ENABLED</strong> -送信を有効になっていると受信します。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>UDP パケットを IPv4 チェックサムの設定です。
<p>有効な値は次のとおりです。</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> -ミニポート ドライバーでは、現在の設定を変更しないでください。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_DISABLED</strong> -無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_ENABLED_RX_DISABLED</strong> -に対応した送信と受信を無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RX_ENABLED_TX_DISABLED</strong> -に対応した受信と送信を無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_ENABLED</strong> -送信を有効になっていると受信します。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>TCP パケットの IPv6 チェックサムの設定。
<p>有効な値は次のとおりです。</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> -ミニポート ドライバーでは、現在の設定を変更しないでください。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_DISABLED</strong> -無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_ENABLED_RX_DISABLED</strong> -に対応した送信と受信を無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RX_ENABLED_TX_DISABLED</strong> -に対応した受信と送信を無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_ENABLED</strong> -送信を有効になっていると受信します。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>UDP パケットの IPv6 チェックサムの設定です。
<p>有効な値は次のとおりです。</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> -ミニポート ドライバーでは、現在の設定を変更しないでください。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_DISABLED</strong> -無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_ENABLED_RX_DISABLED</strong> -に対応した送信と受信を無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RX_ENABLED_TX_DISABLED</strong> -に対応した受信と送信を無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_ENABLED</strong> -送信を有効になっていると受信します。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>Large Send Offload バージョン 1 (LSOV1) 設定します。
<p>有効な値は次のとおりです。</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> -ミニポート ドライバーでは、現在の設定を変更しないでください。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_LSOV1_ENABLED</strong> - LSOV1 を有効にします。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_LSOV1_DISABLED</strong> - LSOV1 が無効になっています。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>インターネット プロトコル セキュリティ (IPsec) はオフロード設定です。
<p>有効な値は次のとおりです。</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> -ミニポート ドライバーでは、現在の設定を変更しないでください。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV1_DISABLED</strong> - IPsec オフロードを無効にします。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV1_AH_ENABLED</strong> - IPsec 認証ヘッダー (AH) 機能は、送信を有効にして、受信の負荷を軽減します。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV1_ESP_ENABLED</strong> - IPsec カプセル化のセキュリティ ペイロード (ESP) 機能は、送信を有効にして、受信の負荷を軽減します。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV1_AH_AND_ESP_ENABLED</strong> - IPsec オフロード AH と ESP 機能は、送信を有効になっているし、受信します。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>大規模な用の送信にオフロード IPv4 バージョン 2 (LSOV2) 設定します。
<p>有効な値は次のとおりです。</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> -ミニポート ドライバーでは、現在の設定を変更しないでください。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_LSOV2_ENABLED</strong> - LSOV2 ipv4 を有効にします。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_LSOV2_DISABLED</strong> - ipv4 LSOV2 が無効になっています。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>大規模な用の送信にオフロード IPv6 バージョン 2 (LSOV2) 設定します。
<p>有効な値は次のとおりです。</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> -ミニポート ドライバーでは、現在の設定を変更しないでください。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_LSOV2_ENABLED</strong> - LSOV2 ipv6 が有効にします。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_LSOV2_DISABLED</strong> - ipv6 LSOV2 が無効になっています。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>IPv4 接続はオフロード設定です。
<p>有効な値は次のとおりです。</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> -ミニポート ドライバーでは、現在の設定を変更しないでください。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>IPv6 接続はオフロード設定です。
<p>有効な値は次のとおりです。</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> -ミニポート ドライバーでは、現在の設定を変更しないでください。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>IPv4 のセグメントの結合の表示状態を示します。
<p>有効な値は次のとおりです。</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - RSC の状態は変更されません。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RSC_ENABLED</strong> - RSC の状態が有効にします。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RSC_DISABLED</strong> - RSC の状態が無効になっています。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>IPv6 のセグメントの結合の表示状態を示します。
<p>有効な値は次のとおりです。</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - RSC の状態は変更されません。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RSC_ENABLED</strong> - RSC の状態が有効にします。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RSC_DISABLED</strong> - RSC の状態が無効になっています。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>値は、フラグのビットごとの OR です。 これは、0 に設定する必要があります。 現在定義されているフラグはありません。</td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>インターネット プロトコル セキュリティ (IPsec) は、IPv6 と IPv4 の両方をサポートするミニポート アダプターのバージョン 2 の設定をオフロードします。 これには、IPv6 と IPv4 の両方のサポートの設定を指定します。
<p>有効な値は次のとおりです。</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> -ミニポート ドライバーでは、現在の設定を変更しないでください。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_DISABLED</strong> - IPsec オフロード バージョン 2 が無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_AH_ENABLED</strong> - IPsec オフロード バージョン 2 の認証ヘッダー (AH) 機能は、送信を有効にして、受信します。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_ESP_ENABLED</strong> - IPsec オフロード バージョン 2 のカプセル化セキュリティ ペイロード (ESP) 機能は、送信を有効にして、受信します。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_AH_AND_ESP_ENABLED</strong> - IPsec オフロード バージョン 2 の AH と ESP の機能は、送信を有効になっているし、受信します。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>インターネット プロトコル セキュリティ (IPsec) は、IPv4 をサポートし、IPv6 をサポートしないミニポート アダプターのバージョン 2 の設定をオフロードします。 IPsecV2 メンバーを指定すると、ミニポート ドライバーでは、IPv6 をサポートする場合、IPv4 設定とこのメンバーは使用されません。
<p>有効な値は次のとおりです。</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> -ミニポート ドライバーでは、現在の設定を変更しないでください。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_DISABLED</strong> - IPsec オフロード バージョン 2 が無効になっています。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_AH_ENABLED</strong> - IPsec オフロード バージョン 2 の認証ヘッダー (AH) 機能は、送信を有効にして、受信します。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_ESP_ENABLED</strong> - IPsec オフロード バージョン 2 のカプセル化セキュリティ ペイロード (ESP) 機能は、送信を有効にして、受信します。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_AH_AND_ESP_ENABLED</strong> - IPsec オフロード バージョン 2 の AH と ESP の機能は、送信を有効になっているし、受信します。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>タスク オフロードのパケットをカプセル化されます。 プロトコル ドライバーでは、次の値のいずれかにこのフィールドを設定します。
<p></p>
<ul>
<li><strong>NDIS_OFFLOAD_SET_NO_CHANGE</strong> (0) - NVGRE タスク オフロードの状態は変更されません。</li>
<li><strong>NDIS_OFFLOAD_SET_ON</strong> (1) - により、NVGRE タスク オフロードです。</li>
<li><strong>NDIS_OFFLOAD_SET_OFF</strong> (2) - を無効に NVGRE タスク オフロードです。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>型のカプセル化します。 このフィールドは、カプセル化パケット タスク オフロードに設定されている場合にのみ、有効な<strong>NDIS_OFFLOAD_SET_ON</strong>します。 カプセル化パケット タスク オフロード メンバーに設定されていないかどうかは<strong>NDIS_OFFLOAD_SET_ON</strong>、このメンバーは 0 になります。 プロトコル ドライバーは、または、必要なカプセル化の種類に対応するフラグのビットごとにカプセル化の種類を設定する必要があります。 これは、次のフラグから選択できます。
<p></p>
<ul>
<li><strong>NDIS_ENCAPSULATION_TYPE_GRE_MAC</strong> (0x00000001) - 指定 GRE MAC encapsulation (NVGRE)。</li>
</ul></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>必要条件
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
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_オフロード\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload_parameters)

[OID\_WDI\_設定\_TCP\_オフロード\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-tcp-offload-parameters)

 

 




