---
title: LoginToTarget
description: LoginToTarget
ms.assetid: 9ad66387-ca77-46e7-aa91-5c909251c2ce
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 483566fd2e5a7310b6147bfa3899c928aeaf8d02
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580764"
---
# <a name="logintotarget"></a>LoginToTarget


**LoginToTarget**メソッドがターゲット ポータルにログオンする HBA イニシエーターを管理するミニポート ドライバーに指示します。

実装するミニポート ドライバー、 [MSiSCSI\_操作 WMI クラス](msiscsi-operations-wmi-class.md)このメソッドをサポートする必要があります。

ミニポート ドライバーで作成したセッションに関する情報を公開する必要があります、 [MSiSCSI\_InitiatorSessionInfo WMI クラス](msiscsi-initiatorsessioninfo-wmi-class.md)します。

次の表では、イニシエーターが確立できるログオン セッションの種類について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ログイン セッション</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>情報表示</p></td>
<td align="left"><p>検出セッションは、専用に使用<strong>SendTargets</strong>操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>情報</p></td>
<td align="left"><p>情報のセッションにより、イニシエーターが、クエリについては、ターゲットがイニシエーターでは、プラグ アンド プレイ (PnP) マネージャー; ターゲットの論理ユニット番号 (Lun) を報告しません記憶域ポート ドライバーの Lun を列挙またはローカル デバイスとして公開することはできません。 管理アプリケーションは、情報のセッションを確立して、ユーザー モードの iSCSI ライブラリのルーチンをなど呼び出し、これらのリモートの Lun を照会できます<strong>SendScsiInquiry</strong>、 <strong>SendScsiReportLuns</strong>、および<strong>SendScsiReadCapacity</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>データ</p></td>
<td align="left"><p>データは全機能装備のセッションです。 ミニポート ドライバー、セッションを開始する必要があります、Lun ターゲット上に報告ポート ドライバー、ポート ドライバーはそれらを列挙し、適切なドライバーが読み込まれるように。 ソフトウェアは、ローカル デバイスと同様、これらのリモート デバイスをアクセスできます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Boot</p></td>
<td align="left"><p>ブートは iSCSI LUN がブート デバイスとして使用されているフル装備のセッションです。</p></td>
</tr>
</tbody>
</table>

 

識別子 (ID) を**LoginToTarget**メソッド割り当てます、セッションには、セッションの有効期間にわたって定数である必要があります。 同じセッション ID を使用する場合でも、非同期のログオフまたはネットワーク イベント、ターゲットへの接続を切断し、強制的に再接続するミニポート ドライバー、ミニポート ドライバーを続行する必要があります。

データとセッションの情報を再確立するときに、ミニポート ドライバーでは、次のガイドラインを使用する必要があります。

<span id="Periodic_reconnection_attempts"></span><span id="periodic_reconnection_attempts"></span><span id="PERIODIC_RECONNECTION_ATTEMPTS"></span>定期的な再接続の試行  
ミニポート ドライバーは、定期的に再接続を試行する必要があります (5 秒間隔は推奨)、ログオンに成功するか、ミニポート ドライバーはログオフ要求を受け取るまでです。

<span id="Device_removal_latency"></span><span id="device_removal_latency"></span><span id="DEVICE_REMOVAL_LATENCY"></span>デバイス削除の待機時間  
ミニポート ドライバーでは、ターゲットの論理ユニットはすぐには、ローカルのオペレーティング システムのデバイス スタックから削除しないでください。 代わりに、ミニポート ドライバーでは、ローカルにキャッシュされたデータを照会し、レポートの LUN の要求を処理およびミニポート ドライバーが処理するため、リモート ターゲットに送る必要がある要求をキューを使用する必要があります。

ミニポート ドライバーが約 60 秒後に、ターゲットとのセッションを再確立できない場合は、そのターゲットの論理ユニットは、ローカル デバイス スタックから削除する必要があります。 デバイス スタックからデバイスの削除に 60 秒の待機時間を導入することで、ミニポート ドライバーが、不必要にリモート ターゲットでのデータにアクセスするアプリケーションをローカルの作業を中断することを回避できます。 しかし、60 秒以上の待機時間は、要求の数が多いをキューに入れ、ミニポート ドライバーを必要があります、これらの要求が、許容できない量のシステム リソースを消費して可能性があります。 待機時間の正確な時間を設定できるようにします。

**LoginToTarget** WMI メソッドが属する、 [MSiSCSI\_操作 WMI クラス](msiscsi-operations-wmi-class.md)します。

ログを確立するために iSCSI ユーザー モードのライブラリを使用するアルゴリズムの詳細については、**LoginIScsiTarget**を参照してください。

 

 





