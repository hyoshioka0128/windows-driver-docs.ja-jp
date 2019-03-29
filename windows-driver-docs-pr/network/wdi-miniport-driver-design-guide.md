---
title: WDI ミニポート ドライバー設計ガイド
description: WLAN デバイス ドライバー インターフェイス (WDI) は、デスクトップのエディション (Home、Pro、Enterprise、および教育機関向け) の場合は、どちらも Windows 10 および Windows 10 Mobile の新しい WLAN のユニバーサル Windows ドライバー モデルです。
ms.assetid: E1666D5E-1932-4378-B4F6-61F28716183E
keywords:
- wi-fi ドライバー、wi-fi ドライバーを Windows 10、ワイヤレス ドライバー、ワイヤレス ドライバーの windows 10、wlan ドライバー、windows 10 の wlan ドライバー、wlan ドライバー インターフェイス、WDI ドライバー、WDI ネットワーク ドライバー、WDI Windows 10
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23aff4fa1d8ac998f021aa9d284deffbc36365f7
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464198"
---
# <a name="wdi-miniport-driver-design-guide"></a>WDI ミニポート ドライバー設計ガイド


WLAN デバイス ドライバー インターフェイス (WDI) は、デスクトップのエディション (Home、Pro、Enterprise、および教育機関向け) の場合は、どちらも Windows 10 および Windows 10 Mobile 用の Wi-fi ドライバーの新しいユニバーサル Windows ドライバー モデルです。 WLAN のデバイスの製造元は、Windows 10 OS 実装 WDI ミニポート ドライバーを書き込みます。 WDI は、以前のネイティブ WLAN ドライバー モデルよりも少ないコードを記述するデバイスの製造元を使用できます。 Windows 10 で導入されるすべての新しい WLAN 機能には WDI ベースのドライバーが必要です。

ベンダーから提供されるネイティブ WLAN ドライバーは Windows 10 で引き続き動作しますが、開発時に対象とした Windows バージョンの機能に限定されます。

この設計ガイドでは、WDI 要件とインターフェイスの仕様が記載されています。 新しいモデルの重要な目標は次のとおりです。

-   品質および Windows WLAN ドライバーの信頼性を向上します。
-   これにより、IHV ドライバーの複雑さが軽減され IHV ドライバーの開発の全体的なコストを削減現在ドライバー モデルの複雑さを軽減します。

このドキュメントの対象では、Windows および IHV ドライバー コンポーネントの間での Wi-fi 操作の動作とフローを指定します。 これは、ソフトウェア インターフェイス署名 (たとえば、デバイス ドライバー インターフェイス モデル) と Windows での IHV コンポーネントの読み込み方法の詳細には含まれません。

## <a name="design-principles"></a>設計原則


次の原則は、全体的なモデルとこのプロトコルの設計ガイド付き。

1.  ホスト コンポーネントと IHV コンポーネント/デバイス間のトラフィックの頻繁な通信を最小限に抑えます。 これは本質的に頻度の高い SDIO などのバス実装のため特に重要です。
2.  Wi-fi 機能 (特に低待機時間で実行する必要があります機能) は、デバイスによって処理されると想定されます。
3.  規制上のすべての関連機能では、IHV コンポーネントに存在し、IHV によって制御されます。
4.  Windows エクスペリエンスは、ホストのコンポーネントと Windows オペレーティング システムによって制御されます。
5.  Windows では、ハングしたデバイスを再生する機能があります。 IHV コンポーネントを再設定して、10 秒以内に回復するための十分な状態があります。
6.  多くのシステム メモリまたは高速なプロセッサを必要とし、ベンダー固有でない操作は、ホストによって処理されます。

## <a name="definitions"></a>定義


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">項目</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>デバイス</p></td>
<td align="left"><p>バスに接続するハードウェアのすべての要素。 デバイスでは、(特に、Wi-fi と Bluetooth など) が複数の無線ことができます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Wi-fi アダプター</p></td>
<td align="left"><p>この仕様での説明に従って、Wi-fi 機能を実装するデバイスの特定の部分。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ポート</p></td>
<td align="left"><p>MAC と PHY の状態は、特定の接続を表すオブジェクト。</p></td>
</tr>
<tr class="even">
<td align="left"><p>IHV コンポーネント</p></td>
<td align="left"><p>ホストに Wi-fi アダプター/デバイスを表す IHV が開発したソフトウェア コンポーネント。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Host</p></td>
<td align="left"><p>ホスト側または Microsoft オペレーティング システム ソフトウェアこの仕様で説明されているインターフェイスを使用して、IHV コンポーネントと連携します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>上端ドライバー (UE)</p></td>
<td align="left"><p>UE は、このドキュメントで WDI と呼ばれる、WdiWiFi ドライバーを参照します。 UE と低い Edge (LE) IHV ドライバーは、完全な NDIS ミニポート ドライバーに結合します。 UE は、コア Wi-fi ロジックを実装します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>下位の Edge ドライバー (LE)</p></td>
<td align="left"><p>LE は下辺 IHV ドライバーを表します。 LE および UE は、完全な NDIS ミニポート ドライバーに結合します。 LE バスとハードウェアの特定の機能を実装します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>機能レベルのリセット (FLR)</p></td>
<td align="left"><p>機能レベルをリセット、PCIe 仕様のようにします。 この用語は、複合関数があります。 完全なデバイスのリセットではなく、関数のリセットを指します。 このようなスコープのリセットに、同じデバイス上の他の機能が損なわれるされません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>プラットフォーム レベルのリセット (する)</p></td>
<td align="left"><p>プラットフォーム レベルのリセット。 これは、デバイス上のすべての関数をメソッドへの影響にリセットします。 コストとフット プリントを削減するデバイスで複数の関数を作成することがよくなります。 たとえば、チップの Bluetooth が通常 Wi-fi で構築します。 ただし、このような reset メソッドは、デバイス上のすべての関数単位をリセットします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>回復 (RR) をリセットします。</p></td>
<td align="left"><p>RR はリセットおよび回復のイベント シーケンスを表します。</p>
<p>FLR が含まれます。</p>
<ul>
<li>NDIS で、バスに Wi-fi 機能をリセットする要求を転送する要求です。</li>
<li>ドライバー、ファームウェアのコンテキストの回復。</li>
<li>リセットする前に接続されていた場合は、アクセス ポイントに再接続します。</li>
</ul>
<p>含まれます。</p>
<ul>
<li>NDIS で、バスに要求を転送する要求です。 PnP とバスの操作驚き、デバイスを削除します。</li>
<li>デバイスの再列挙体。</li>
<li>デバイス スタックを再確立します。</li>
<li>Wi-fi が再起動し、再接続します。</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p>WDI コマンド</p></td>
<td align="left"><p>UE は WDI Oid を送信し、LE コールバックを呼び出します。 これらはすべて WDI コマンドと呼ばれます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MAC アドレスのランダム化</p></td>
<td align="left"><p>構成されている Windows 10 のユーザーのプライバシー保護を強化するために、Wi-fi MAC アドレスはなどで使用されて状況によっては、特定の Wi-fi ネットワーク、または特定の条件でスキャンを開始するときに接続する前にします。 これは、ステーションのポートにのみ適用されます。 システムはにより重要な接続のシナリオが切断されていないためそのランダム化を適切に使用されます。 システムでは、アドレスの変更を管理を発行して<a href="https://msdn.microsoft.com/library/windows/hardware/dn925952" data-raw-source="[OID_WDI_TASK_DOT11_RESET](https://msdn.microsoft.com/library/windows/hardware/dn925952)">OID_WDI_TASK_DOT11_RESET</a>スキャンを発行する前にコマンドやコマンドを接続します。 リセット コマンド パラメーターには、省略可能な MAC アドレス引数が含まれます。 引数が存在する場合は、MAC アドレスが指定した値にリセットされます。 存在しない場合は、MAC アドレスは現在の値のまま。 ランダム化された MAC アドレスを構成するときに、オペレーティング システムは IEEE802 アドレスに対して定義されている「ローカルで管理」の形式を使用します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ECSA</p></td>
<td align="left"><p>拡張チャネル スイッチのお知らせします。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック


[WDI ミニポート ドライバー リファレンス](https://msdn.microsoft.com/library/windows/hardware/dn926075)

 

 






