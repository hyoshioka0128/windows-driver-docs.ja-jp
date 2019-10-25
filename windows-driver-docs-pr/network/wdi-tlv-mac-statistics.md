---
title: WDI_TLV_MAC_STATISTICS
description: WDI_TLV_MAC_STATISTICS は、OID_WDI_GET_STATISTICS のピアごとの MAC 統計を含む TLV です。
ms.assetid: 47ABF170-76D7-4F17-BA92-56E1FEFF729D
ms.date: 07/18/2017
keywords:
- WDI_TLV_MAC_STATISTICS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 3b5e873d3fd909d9b1163ebc5eb28fb77f5455c7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826324"
---
# <a name="wdi_tlv_mac_statistics"></a>WDI\_TLV\_MAC\_統計


WDI\_TLV\_MAC\_STATISTICS は、 [OID\_WDI\_の統計情報の取得](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-statistics)に関するピアごとの mac 統計を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0xA6

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
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address" data-raw-source="[&lt;strong&gt;WDI_MAC_ADDRESS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)"><strong>WDI_MAC_ADDRESS</strong></a></td>
<td>これらのカウントが設定されるピアの MAC アドレス。 マルチキャストパケットとブロードキャストパケットの場合、この値は FF-ff-ff-ff-ff-ff に設定されます。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>802.11 ステーションの IEEE MAC レイヤーが正常に送信した MSDU パケットと MMPDU フレームの数。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>802.11 ステーションの IEEE MAC レイヤーが正常に受信した MSDU パケットと MMPDU フレームの数。 このメンバーは、暗号暗号化解除または MIC 検証に失敗した受信パケットに対して、増分しないでください。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>IEEE 802.11 dot11ExcludeUnencrypted 管理情報ベース (MIB) オブジェクトが有効になっている場合に MAC レイヤーによって破棄された、暗号化されていない受信済み MPDU フレームの数。
<p>この MIB オブジェクトの詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-exclude-unencrypted" data-raw-source="[OID_DOT11_EXCLUDE_UNENCRYPTED](https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-exclude-unencrypted)">OID_DOT11_EXCLUDE_UNENCRYPTED</a>」を参照してください。 IEEE 802.11 MAC ヘッダーの Frame コントロールフィールドの Protected Frame サブフィールドが0に設定されている場合、MPDU フレームは暗号化されていないと見なされます。</p></td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>MIC エラーのために802.11 ステーションが破棄した、受信した MSDU パケットの数。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>TKIP replay protection 手順により802.11 ステーションが破棄した、受信した MPDU フレームの数。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>802.11 ステーションが TKIP ICV エラーのために暗号化を解除できなかった、暗号化された MPDU フレームの数。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>AES-CCMP 形式が無効なために802.11 が破棄した、受信した MPDU フレームの数。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>AES CCMP replay 保護手順により802.11 ステーションが破棄した、受信した MPDU フレームの数。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>AES CCMP 暗号化アルゴリズムによって検出されたエラーが原因で802.11 ステーションが破棄した、受信した MPDU フレームの数。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>802.11 ステーションで WEP 復号化キーを使用できなかった、受信した暗号化された MPDU フレームの数。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>WEP ICV エラーが原因で802.11 ステーションが暗号化を解除できなかった、暗号化された MPDU フレームの数。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>802.11 ステーションが正常に暗号化解除した、受信した暗号化パケットの数。
<p>WEP および TKIP 暗号アルゴリズムの場合、ポートは、正常に暗号化解除された、受信した暗号化された MPDU ごとにこのカウンターを増やす必要があります。 AES CCMP 暗号アルゴリズムの場合、ポートは、正常に暗号化解除された、受信した暗号化された MSDU パケットごとにこのカウンターをインクリメントする必要があります。</p></td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>802.11 ステーションが復号化できなかった暗号化されたパケットの数。
<p>WEP および TKIP 暗号アルゴリズムの場合、ポートは、正常に暗号化解除されなかった、受信した暗号化された MPDU ごとにこのカウンターを増やす必要があります。 AES CCMP 暗号アルゴリズムの場合、ポートは、正常に暗号化解除されなかった、受信した暗号化された MSDU パケットごとにこのカウンターをインクリメントする必要があります。 ポートは、正常に暗号化解除されたパケットに対してこのカウンターを増やさないでください。その他の理由で破棄されます。 たとえば、ポートでは、TKIP MIC の故障または TKIP/CCMP 再生によって破棄されたパケットに対して、このカウンターを増やさないようにする必要があります。</p></td>
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

 

 




