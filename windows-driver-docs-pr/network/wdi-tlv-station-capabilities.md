---
title: WDI_TLV_STATION_CAPABILITIES
description: WDI_TLV_STATION_CAPABILITIES では、ステーションの機能を含む TLV です。
ms.assetid: 567445F1-EEDC-4302-B709-ED76D044A971
ms.date: 02/08/2019
keywords:
- WDI_TLV_STATION_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 70b35e7549410cf9d7e1cf8dc2cc623865d23b26
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903258"
---
# <a name="wditlvstationcapabilities"></a>WDI\_TLV\_ステーション\_機能


WDI\_TLV\_ステーション\_機能は、ステーションの機能を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x11

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
<td>UINT32</td>
<td>スキャン SSID リストのサイズ。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>必要な BSSID 一覧のサイズ。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>必要な SSID リストのサイズ。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>プライバシーの除外リストのサイズ。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>キー マップ テーブルのサイズ。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>既定のテーブルのキー サイズ。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>WEP キー値の最大長。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>STA の既定のキー テーブルあたりの最大数。</td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>QoS のフラグがサポートされています。 デバイスで WMM をサポートするかどうかを指定します。
<p>有効な値は 0 (サポートされていません) および 1 (サポートです)。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>ホスト FIPS モードが実装されているかどうかを指定します。
<p>その他のビット セットで DOT11_EXTSTA_ATTRIBUTES_SAFEMODE_OID_SUPPORTED にフィールドを設定すると、ドライバーは操作の 802.11 のセーフ モードを実装します。</p>
<p>NIC が、National Institute of Standards と Technology (NIST) 連邦情報処理規格 (FIPS) Publication 140-2 では、下から検証証明書を受信したフィールドが DOT11_EXTSTA_ATTRIBUTES_SAFEMODE_CERTIFIED に設定されている場合暗号化モジュールのセキュリティ要件です。 このモードでは、ハードウェアが FIPS 標準に準拠したことを保証します。</p>
<p>FIPS モードは、NIC が実装されていません、フィールドは、ゼロ (0) に設定されている場合</p></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>指定するかどうか 802.11w MFP 機能がサポートされています。
<p>有効な値は 0 (サポートされていません) および 1 (サポートです)。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>省電力自動がサポートされているかどうかを指定します。
<p>有効な値は 0 (サポートされていません) および 1 (サポートです)。</p></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>アダプターは、ステーション BSS リスト キャッシュを保持するかどうかを指定します。
<p>有効な値は 0 (オフ) および 1 (yes です)。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>アダプターがステーションの中に優先 BSSID リストで指定されていない BSSID への関連付けを試みることがあるかどうかを指定します。 接続します。
<p>有効な値は 0 (オフ) および 1 (yes です)。</p></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>最大値には、ネットワーク オフロード リストのサイズがサポートされています。</td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>アダプターが HESSIDs Ssid と指定の SSID + HESSID に一致するこれらのアクセス ポイントにのみ接続/ローミングに関連付けられているを追跡できるかどうかを指定します。
<p>有効な値は 0 (サポートされていません) および 1 (サポートです)。</p></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>アダプターが特定 HESSIDs に属しているネットワークへの接続をオフロードできるかどうかを指定します。</td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>切断されたスタンバイはサポートされているかどうかを指定します。
<p>有効な値は 0 (サポートされていません) および 1 (サポートです)。</p></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>ドライバーが開始側として正常時間測定 (FTM) プロトコルをサポートするかどうかを指定します。
<p>有効な値は 0 (サポートされていません) および 1 (サポートです)。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>FTM 要求タスクごとにクエリ可能なターゲットの Sta の最大数。</td>
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

 

 




