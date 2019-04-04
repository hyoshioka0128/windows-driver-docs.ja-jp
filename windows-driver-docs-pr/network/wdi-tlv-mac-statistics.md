---
title: WDI_TLV_MAC_STATISTICS
description: WDI_TLV_MAC_STATISTICS は、OID_WDI_GET_STATISTICS のツー ピアの MAC の統計情報を含む TLV です。
ms.assetid: 47ABF170-76D7-4F17-BA92-56E1FEFF729D
ms.date: 07/18/2017
keywords:
- WDI_TLV_MAC_STATISTICS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 0513d4da6a4f8f1735b1768ab32d1124bf47d535
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580171"
---
# <a name="wditlvmacstatistics"></a>WDI\_TLV\_MAC\_統計情報


WDI\_TLV\_MAC\_統計情報が、ピア用の MAC 統計情報を含む TLV [OID\_WDI\_取得\_統計](https://msdn.microsoft.com/library/windows/hardware/dn925850)します。

## <a name="tlv-type"></a>TLV 型


0xA6

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
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn926071" data-raw-source="[&lt;strong&gt;WDI_MAC_ADDRESS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn926071)"><strong>WDI_MAC_ADDRESS</strong></a></td>
<td>これらのカウントが設定されているピアの MAC アドレス。 マルチキャストおよびブロードキャスト パケットの場合は、この値は FF-FF-FF-FF-FF-FF-FF に設定されます。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>MSDU パケットと 802.11 ステーションの IEEE mac が正常に送信される MMPDU フレームの数。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>MSDU パケットと 802.11 ステーションの IEEE mac が正常に受信された MMPDU フレームの数。 このメンバーを暗号解読または MIC 検証に失敗した受信パケットのインクリメントしない必要があります。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>Mac の破棄、IEEE 802.11 dot11ExcludeUnencrypted 管理情報ベース (MIB) オブジェクトが有効にすると、暗号化されていない受信 MPDU フレームの数。
<p>この MIB オブジェクトに関する詳細については、<a href="https://msdn.microsoft.com/library/windows/hardware/ff569365" data-raw-source="[OID_DOT11_EXCLUDE_UNENCRYPTED](https://msdn.microsoft.com/library/windows/hardware/ff569365)">OID_DOT11_EXCLUDE_UNENCRYPTED</a>を参照してください。 MPDU フレームでは、IEEE 802.11 MAC ヘッダー内のフレーム コントロール フィールドの保護されているフレームのサブフィールドが 0 に設定されているときに暗号化されていないと見なされます。</p></td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>MIC の失敗したため、802.11 ステーションが破棄された受信 MSDU パケットの数。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>[Tkip] 再生の保護手順したため、802.11 ステーションが破棄された受信 MPDU フレームの数。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>802.11 ステーションが TKIP ICV エラーのための暗号化を解除に失敗した暗号化の MPDU フレームの数。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>無効な AES CCMP 形式したため、802.11 が破棄された受信 MPDU フレームの数。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>AES CCMP 再生の保護手順したため、802.11 ステーションが破棄された受信 MPDU フレームの数。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>AES CCMP の復号化アルゴリズムにより検出されたエラーのため、802.11 ステーションが破棄された受信 MPDU フレームの数。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>MPDU フレームを暗号化された受信を WEP 復号化キーが使用可能な 802.11 ステーションの数。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>802.11 ステーションが WEP ICV エラーのための暗号化を解除に失敗した暗号化の MPDU フレームの数。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>802.11 ステーションが正常に復号化する受信の暗号化されたパケットの数。
<p>WEP および TKIP 暗号化アルゴリズムをポートが正常に復号化された各受信暗号化の MPDU のこのカウンターをインクリメントする必要があります。 AES CCMP の暗号アルゴリズムのポートは、各受信暗号化 MSDU パケットが正常に復号化するには、このカウンターを増やす必要があります。</p></td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>802.11 ステーションが復号化に失敗した暗号化されたパケットの数。
<p>WEP および TKIP 暗号化アルゴリズムをポートは正常に解読されませんを受信した各暗号化 MPDU のこのカウンターをインクリメントする必要があります。 AES CCMP の暗号アルゴリズムのポートは、このにカウンターを受信した暗号化された MSDU される各パケットは正常に解読されませんを増やす必要があります。 ポートには、このカウンターは正常に復号化が、他の理由が破棄されたパケットを増加できませんする必要があります。 たとえば、ポート TKIP MIC のエラーのため破棄されたパケットの場合は、このカウンターをインクリメントいない必要があります。 または TKIP/CCMP 再生します。</p></td>
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

 

 




