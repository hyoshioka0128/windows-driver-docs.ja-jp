---
title: WDI ミニポート ドライバー設計ガイド
description: WLAN Device Driver Interface (WDI) は、Windows 10 for desktop エディション (Home、Pro、Enterprise、および教育) と Windows 10 Mobile の両方に対応した新しい WLAN ユニバーサル Windows ドライバーモデルです。
ms.assetid: E1666D5E-1932-4378-B4F6-61F28716183E
keywords:
- wi-fi ドライバー、wi-fi ドライバー Windows 10、ワイヤレスドライバー、ワイヤレスドライバー windows 10、wlan ドライバー、wlan ドライバー windows 10、wlan driver interface、WDI drivers、WDI network drivers、WDI Windows 10
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 789cfeb9ab90e94f817bd7f846e6277573ecb135
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842920"
---
# <a name="wdi-miniport-driver-design-guide"></a>WDI ミニポート ドライバー設計ガイド


WLAN Device Driver Interface (WDI) は、Windows 10 for desktop エディション (Home、Pro、Enterprise、および教育) と Windows 10 Mobile の両方について、Wi-fi ドライバー用の新しいユニバーサル Windows ドライバーモデルです。 WLAN デバイスの製造元は、Windows 10 OS 実装と連携するように、WDI ミニポートドライバーを記述します。 WDI を使用すると、デバイスの製造元は以前のネイティブ WLAN ドライバーモデルよりも少ないコードを作成できます。 Windows 10 で導入されるすべての新しい WLAN 機能には WDI ベースのドライバーが必要です。

ベンダーから提供されるネイティブ WLAN ドライバーは Windows 10 で引き続き動作しますが、開発時に対象とした Windows バージョンの機能に限定されます。

WDI の要件とインターフェイスの仕様については、この設計ガイドで説明されています。 新しいモデルの主な目標は次のとおりです。

-   Windows WLAN ドライバーの品質と信頼性を向上させます。
-   現在のドライバーモデルの複雑さを軽減します。これにより、IHV ドライバーの複雑さが軽減され、IHV ドライバーを開発するための全体的なコストが削減されます。

このドキュメントでは、Windows と IHV ドライバーコンポーネント間での Wi-fi 操作のフローと動作を指定することに重点を置いています。 ソフトウェアインターフェイスの署名 (デバイスドライバーのインターフェイスモデルなど) や、IHV コンポーネントが Windows に読み込まれる方法の詳細については説明しません。

## <a name="design-principles"></a>設計原則


次の原則は、このプロトコルのモデルと設計全体を示しています。

1.  ホストコンポーネントと IHV コンポーネント/デバイスとの間のトラフィックの頻繁な通信を最小限に抑えます。 これは、SDIO などのバスでの実装 (本質的に高い) の場合に特に重要です。
2.  Wi-fi 機能 (特に、低待機時間で実行する必要がある機能) は、デバイスによって処理されることが想定されています。
3.  すべての規制に関連する機能は、IHV コンポーネントに存在し、IHV によって制御されます。
4.  Windows エクスペリエンスは、ホストコンポーネントと Windows オペレーティングシステムによって制御されます。
5.  Windows には、ハングしたデバイスをやり直すする機能があります。 IHV コンポーネントを再度プログラミングし、10秒以内に復旧するのに十分な状態があります。
6.  大量のシステムメモリや高速プロセッサを必要とし、ベンダー固有ではない操作は、ホストによって処理されます。

## <a name="definitions"></a>定義


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">用語</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>デバイス</p></td>
<td align="left"><p>バスに接続するハードウェアの全体。 1つのデバイスに複数のラジオ (特に Wi-fi と Bluetooth) を搭載できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Wi-fi アダプター</p></td>
<td align="left"><p>この仕様で説明されているように Wi-fi 機能を実装するデバイスの特定の部分。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ポート</p></td>
<td align="left"><p>特定の接続の MAC と PHY の状態を表すオブジェクト。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IHV コンポーネント</p></td>
<td align="left"><p>ホストに Wi-fi アダプターまたはデバイスを表す、IHV が開発したソフトウェアコンポーネント。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Host</p></td>
<td align="left"><p>この仕様で説明されているインターフェイスを使用して IHV コンポーネントと対話するホスト側の Microsoft/オペレーティングシステムソフトウェア。</p></td>
</tr>
<tr class="even">
<td align="left"><p>上端ドライバー (UE-V)</p></td>
<td align="left"><p>UE-V は、このドキュメントの WDI と呼ばれる WdiWiFi ドライバーを参照します。 UE-V (LE) IHV ドライバーは、完全な NDIS ミニポートドライバーに結合されます。 UE-V は、コア Wi-fi ロジックを実装します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>下端のドライバー (LE)</p></td>
<td align="left"><p>LE は、下部にある IHV ドライバーを参照します。 LE と UE-V は、完全な NDIS ミニポートドライバーに結合されます。 LE は、バスおよびハードウェア固有の機能を実装します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>機能レベルのリセット (FLR)</p></td>
<td align="left"><p>機能レベルのリセット (PCIe 仕様の場合)。 この用語は、複合関数を持つ可能性がある完全なデバイスのリセットと比較して、関数のリセットを指します。 このようなスコープをリセットしても、同じデバイス上の他の関数は損なわれません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>プラットフォームレベルのリセット (PLR)</p></td>
<td align="left"><p>プラットフォームレベルのリセット。 この reset メソッドは、デバイス上のすべての関数に影響します。 コストとフットプリントを削減するために、デバイスで複数の関数を構築することは非常に一般的です。 たとえば、Bluetooth は通常、Wi-fi を使用してチップに組み込まれています。 ただし、このような reset メソッドは、デバイス上のすべての関数ユニットをリセットします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>復旧のリセット (RR)</p></td>
<td align="left"><p>RR は、リセットと復旧のイベントシーケンスを参照します。</p>
<p>FLR の場合、これには次のものが含まれます。</p>
<ul>
<li>NDIS への要求。この要求をバスに転送して Wi-fi 機能をリセットします。</li>
<li>ドライバーによるファームウェアコンテキストの回復。</li>
<li>リセットの前に接続されていた場合、アクセスポイントに再接続します。</li>
</ul>
<p>PLR の場合、これには次のものが含まれます。</p>
<ul>
<li>要求をバスに転送する NDIS への要求。 バスは PnP とやり取りして、デバイスを突然削除します。</li>
<li>デバイスを再列挙します。</li>
<li>デバイススタックを再確立します。</li>
<li>Wi-fi を再起動して再接続します。</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p>WDI コマンド</p></td>
<td align="left"><p>UE-V は WDI Oid を送信し、LE コールバックを呼び出します。 これらはすべて WDI コマンドと呼ばれます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MAC アドレスのランダム化</p></td>
<td align="left"><p>Windows 10 ユーザーのプライバシーを向上させるために、特定の Wi-fi ネットワークに接続する前や特定の条件でスキャンを開始する前など、一部の状況では Wi-fi MAC アドレスが使用されます。 これは、ステーションのポートにのみ適用されます。 システムは、ランダム化が適切に使用されていることを確認します。これにより、重要な接続シナリオが壊れることはありません。 システムは、スキャンまたは接続コマンドを発行する前に<a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-dot11-reset" data-raw-source="[OID_WDI_TASK_DOT11_RESET](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-dot11-reset)">OID_WDI_TASK_DOT11_RESET</a>コマンドを発行することによって、アドレスの変更を管理します。 Reset コマンドのパラメーターには、オプションの MAC アドレス引数が含まれています。 引数が存在する場合は、MAC アドレスが指定された値にリセットされます。 存在しない場合は、MAC アドレスが現在の値のままになります。 ランダム化された MAC アドレスを構成する場合、オペレーティングシステムでは、IEEE802 アドレスに対して定義されている "ローカルで管理" 形式が使用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ECSA</p></td>
<td align="left"><p>拡張チャネルスイッチのアナウンス。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック


[WDI ミニポートドライバーリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

 

 






