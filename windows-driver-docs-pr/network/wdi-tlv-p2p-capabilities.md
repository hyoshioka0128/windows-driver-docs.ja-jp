---
title: WDI_TLV_P2P_CAPABILITIES
description: WDI_TLV_P2P_CAPABILITIES では、Wi-Fi Direct 機能を含む TLV です。
ms.assetid: 3BE13A87-ECA2-4204-87F1-2BE393F33D4C
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_CAPABILITIES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 7673589acdb9a97e4aef4d6a072645bef62e6af8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558674"
---
# <a name="wditlvp2pcapabilities"></a>WDI\_TLV\_P2P\_機能


WDI\_TLV\_P2P\_機能は、Wi-Fi Direct 機能を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x17

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
<td>UINT8</td>
<td>グループの所有者の同時実行の数を指定します。</td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>同時実行クライアントの数を指定します。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>サポートされている WPS バージョンを指定します。</td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>サービスの検出がサポートされているかどうかを指定します。
<p>有効な値は 0 (サポートされていません) および 1 (サポートです)。</p></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>Wi-Fi Direct サービスの名前検索のサポート。 かどうか、サービス名のハッシュの一覧を指定する場合、アダプターできますのハッシュにサービスをプローブし、到着すると、応答を示すを指定します。
<p>有効な値は 0 (サポートされていません) および 1 (サポートです)。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>Wi-Fi Direct サービス情報の検出のサポート。 かどうか、サービス名のハッシュの一覧を指定する場合、アダプターできますプローブとクエリを実行 ANQP 完全なサービス情報を取得するを指定します。
<p>有効な値は 0 (サポートされていません) および 1 (サポートです)。</p></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>(ビーコンおよびプローブ応答で送信される) をサービス名の提供情報のバイトの最大許容数を指定します。 これは、提供されるサービスの数のハード制限を設定します。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>サポートされている最大ガス プロトコルを使用して、アダプターが応答できるサービス情報の提供情報のバイト数を指定します。 これは、有効なは、サービスの提供情報のクエリに応答して、デバイスがサポートしている場合だけです。 この値は、ファームウェアがすべてのクエリに応答するホストを解除されないように、ファームウェアの最適化は。 オペレーティング システムでは、ファームウェア、オペレーティング システムでのフォールバックがあるため、制限がある場合、サービスの提供情報の数は制限されません。 ファームウェアが ANQP クエリの応答を処理できない場合は、要求を渡すかし、オペレーティング システムを処理します。</td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>Wi-Fi Direct デバイスとサービスのバック グラウンドの検出。 アダプターは定期的にクエリ Wi-Fi Direct デバイスを実行し、サービス名のため、新しいデバイスに表示の表示になることを 5 分以内かどうかを指定します。
<p>有効な値は 0 (サポートされていません) および 1 (サポートです)。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>クライアントの探索可能性はサポートされているかどうかを指定します。
<p>有効な値は 0 (サポートされていません) および 1 (サポートです)。</p></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>インフラストラクチャの管理がサポートされているかどうかを指定します。
<p>有効な値は 0 (サポートされていません) および 1 (サポートです)。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>セカンダリのアダプターの種類の一覧の最大サイズ。</td>
</tr>
<tr class="odd">
<td>UINT8[6]</td>
<td>ネットワークのバイト順で、デバイスのアドレス。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>探索フィルター リストのサイズ。</td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>GO クライアント テーブルのサイズ。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>最大サイズ (バイト単位) のベンダー固有拡張 IEs WFD 管理フレームに追加できます。</td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>アダプターが OID_WDI_P2P_LISTEN_STATE_PASSIVE_AVAILABILITY をサポートするかどうかを指定します。
<p>有効な値は 0 (サポートされていません) および 1 (サポートです)。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>アダプターが GO オペレーティング チャンネルへのかを示すの更新をサポートするかどうかを指定します。
<p>有効な値は 0 (サポートされていません) および 1 (サポートです)。</p></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>Windows 10 バージョン 1511、WDI バージョン 1.0.10 に追加されます。
<p>アダプターが 5 GHz 帯域の移動の操作をサポートするかどうかを指定します。</p>
<p>有効な値は 0 (サポートされていません) および 1 (サポートです)。</p></td>
</tr>
<tr class="even">
<td><p>UINT8</p></td>
<td><p>Windows 10 version 1607 では、バージョン 1.0.21 WDI に追加されます。</p>
ASP2 サービス名のインスタンスの一覧が提供された場合、アダプターがのハッシュにサービスをプローブし、到着すると、応答を示すかどうかを指定します。 有効な値は 0 (サポートされていません) および 1 (サポートです)。</td>
</tr>
<tr class="odd">
<td><p>UINT8</p></td>
<td><p>Windows 10 version 1607 では、バージョン 1.0.21 WDI に追加されます。</p>
プローブと ANQP クエリ サービスの完全な情報を取得するかどうか、アダプターは、特定のサービス名のインスタンスのセットを実行できますを指定します。 有効な値は 0 (サポートされていません) および 1 (サポートです)。</td>
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

 

 




