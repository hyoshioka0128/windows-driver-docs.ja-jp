---
title: WDI_TLV_PHY_STATISTICS
description: WDI_TLV_PHY_STATISTICS は、OID_WDI_GET_STATISTICS の PHY ごとの統計情報を含む TLV です。
ms.assetid: 2F27FF4E-54AC-4518-AEB0-3518FBC8BE0F
ms.date: 07/18/2017
keywords:
- WDI_TLV_PHY_STATISTICS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 71fe7efbc022fef9047a97f7bb2bd7bc54a6d089
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561058"
---
# <a name="wditlvphystatistics"></a>WDI\_TLV\_PHY\_統計情報


WDI\_TLV\_PHY\_統計情報がの PHY ごとの統計情報を含む TLV [OID\_WDI\_取得\_統計](https://msdn.microsoft.com/library/windows/hardware/dn925850)します。

## <a name="tlv-type"></a>TLV 型


0xA7

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
<th>種類</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn926105" data-raw-source="[&lt;strong&gt;WDI_PHY_TYPE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn926105)"><strong>WDI_PHY_TYPE</strong></a></td>
<td>この PHY の型。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>MSDU パケットと 802.11 ステーションの IEEE PHY 層が正常に送信される MMPDU フレームの数。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>マルチキャストまたはブロードキャストの MSDU パケットと 802.11 ステーションの IEEE PHY 層が正常に送信される MMPDU フレームの数。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>MSDU パケットと 802.11 ステーションが 802.11 IEEE dot11ShortRetryLimit または dot11LongRetryLimit MIB カウンターで定義された再試行回数の制限を超えた送信に失敗した MMPDU フレームの数。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>802.11 ステーションは、1 つまたは複数の試行後に正常に送信 MSDU パケットと MMPDU フレームの数。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>802.11 ステーションは、1 つの再転送試行より後に正常に送信 MSDU パケットと MMPDU フレームの数。
<p>MSDU パケットの場合、ポートがその MPDU のために必要なフラグメントの再送信の 1 つ以上の後に正常に送信されたパケットごとに、このカウンターを増やす必要があります。</p></td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>MSDU パケットと 802.11 ステーションは、IEEE 802.11 dot11MaxTransmitMSDULifetime MIB オブジェクトで定義されているタイムアウトのため送信に失敗した MMPDU フレームの数。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>802.11 ステーションの送信および受信した ACK 802.11 フレームを確認する MPDU フレームの数。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>802.11 ステーションが要求を送信 (RTS) フレームへの応答で明確に送信する (CTS) フレームを受け取った回数。 これは、ポートごとに保持できません、チャネルあたり保持できます。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>802.11 ステーションが、RTS フレームへの応答で CTS フレームを受信しなかったこと回数。 これは、ポートごとに保持できません、チャネルあたり保持できます。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>時間数、802.11 ステーションが予想し、受信確認 (ACK) フレームを受信しませんでした。 これは、ポートごとに保持できません、チャネルあたり保持できます。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>MSDU パケットと 802.11 ステーションが正常に受信 MMPDU フレームの数。
<p>MSDU パケットの場合、ポートが持つ MPDU フラグメント受信され、フレーム チェック シーケンス (FCS) の検証と再生検出を渡された各パケットに対するこのカウンターを増やす必要があります。 ポートは受信 MSDU パケットまたは MPDU の失敗を分割するかどうかに関係なく、このメンバーを増やす必要があります - mac 暗号復号化します。</p></td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>マルチキャストまたはブロードキャストの MSDU パケットと 802.11 ステーションが正常に受信 MMPDU フレームの数。
<p>MSDU パケットの場合、ポートを持つ MPDU フラグメント受信され、FCS 検証し、再生検出を渡された各パケットに対するこのカウンターを増やす必要があります。 ポートは受信 MSDU パケットまたは MPDU の失敗を分割するかどうかに関係なく、このメンバーを増やす必要があります - mac 暗号復号化します。</p></td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>MSDU パケットまたは無作為検出パケット フィルターが有効な場合は、802.11 ステーションが受信した MMPDU フレームの数。 これは、ポートごとに保持できません、チャネルあたり保持できます。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>IEEE 802.11 dot11MaxReceiveLifetime で定義されているタイムアウトしたため破棄された 802.11 ステーションが、MIB オブジェクトを使用する場合は MSDU パケットと MMPDU フレームを数。 これは、ポートごとに保持できません、チャネルあたり保持できます。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>802.11 ステーションを受信した重複の MPDU フレームの数。 802.11 ステーションでは、802.11 MAC ヘッダーのシーケンス コントロール フィールドの重複するフレームを決定します。 これは、ポートごとに保持できません、チャネルあたり保持できます。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>MSDU パケットまたは MMPDU フレームの 802.11 ステーションが受信した MPDU フレームの数。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>802.11 ステーションで MSDU パケットまたは MMPDU フレームの無作為検出パケット フィルターが有効になっているときに受信した MPDU フレームの数。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>802.11 ステーションが FCS エラーのある受信 MPDU フレームの数。 これは、ポートごとに保持できません、チャネルあたり保持できます。</td>
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
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




