---
title: Device Fundamental のテスト
description: デバイスの基本的なテストの説明です。
ms.assetid: 1963B6BD-158C-4946-8FBA-55DE0C98BE44
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd6a987dcb3ccfccb29e7792a04ef4a6c6a0dbef
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355148"
---
# <a name="device-fundamentals-tests"></a>Device Fundamental のテスト


## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="chaos-tests--device-fundamentals-.md" data-raw-source="[CHAOS Tests (Device Fundamentals)](chaos-tests--device-fundamentals-.md)">CHAOS テスト (Device Fundamental)</a></p></td>
<td align="left"><p>(同時実行ハードウェアおよびオペレーティング システム) の混乱のテストがテスト PnP ドライバーさまざまなデバイス ドライバーのファジー テストを実行し、システムの電源が同時にテストします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="coverage-tests--device-fundamentals-.md" data-raw-source="[Coverage Tests (Device Fundamentals)](coverage-tests--device-fundamentals-.md)">カバレッジ テスト (Device Fundamental)</a></p></td>
<td align="left"><p>デバイスの基本的なカバレッジは、監視して、さまざまな I/O 要求パケット (Irp) を入力するか、指定したデバイスのドライバー スタックのままにするレポートをテストします。 カバレッジのテストからのデータは、ドライバーのテストおよび検証中にカバレッジの弱点を識別できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="cpustress-tests--device-fundamentals-.md" data-raw-source="[CPUStress Tests (Device Fundamentals)](cpustress-tests--device-fundamentals-.md)">CPUStress テスト (Device Fundamental)</a></p></td>
<td align="left"><p>CpuStress テストでは、別のプロセッサ使用率のレベルを持つデバイス I/O のテストを実行します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="driverinstall-tests--device-fundamentals-.md" data-raw-source="[DriverInstall Tests (Device Fundamentals)](driverinstall-tests--device-fundamentals-.md)">DriverInstall テスト (デバイスの基本)</a></p></td>
<td align="left"><p>機能をインストールするドライバーのインストール テスト カテゴリには、テストするテスト アンインストールしてドライバーを何度も再インストールにはが含まれています。 テストでは、I/O が各を再インストールした後、ドライバーとデバイスに対してテストを開始します。 テストは、インストールし、デバイス ドライバーまたはデバイスを再インストールする必要があるエンドユーザーの全体的なエクスペリエンスを向上させるために設計されています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="i-o-tests--device-fundamentals-.md" data-raw-source="[I/O Tests (Device Fundamentals)](i-o-tests--device-fundamentals-.md)">I/O テスト (Device Fundamental)</a></p></td>
<td align="left"><p>デバイスの基本 I/O テストでは、指定したデバイスの基本的な I/O テストを実行します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="penetration-tests--device-fundamentals-.md" data-raw-source="[Penetration Tests (Device Fundamentals)](penetration-tests--device-fundamentals-.md)">侵入テスト (Device Fundamental)</a></p></td>
<td align="left"><p>デバイスの基礎の侵入テストは、セキュリティのテストの重要なコンポーネントである入力による攻撃のさまざまなフォームを実行します。 攻撃および侵入テストは、ソフトウェア インターフェイスでの脆弱性を識別に役立つことができます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="pnp-tests--device-fundamentals-.md" data-raw-source="[PnP Tests (Device Fundamentals)](pnp-tests--device-fundamentals-.md)">PnP テスト (デバイスの基本)</a></p></td>
<td align="left"><p>デバイスの基礎 PnP テスト PnP Irp; のほぼすべてを処理するためのドライバーを強制します。ただし、具体的には負荷がかかっている 3 つの領域がある: 削除、再調整、および突然の削除。 PnP テストは、これらのそれぞれを個別に、テスト、またはすべて同時にテストするメカニズムを提供します (これは、ストレス テストとして)。 PnP このテストは、ユーザー モード API の呼び出し (のテスト アプリケーションの概要) と (上位フィルター ドライバー) を通じてカーネル モードの API 呼び出しの組み合わせを使用して行われます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="reboot-tests--device-fundamentals-.md" data-raw-source="[Reboot Tests (Device Fundamentals)](reboot-tests--device-fundamentals-.md)">再起動テスト (Device Fundamental)</a></p></td>
<td align="left"><p>デバイスの基礎の再起動のテストは前に、と後に、またはシステムの再起動中に、指定したデバイスの I/O を実行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="sleep-tests--device-fundamentals-.md" data-raw-source="[Sleep Tests (Device Fundamentals)](sleep-tests--device-fundamentals-.md)">スリープ テスト (Device Fundamental)</a></p></td>
<td align="left"><p>デバイス基礎スリープ テスト実行 I/O と、指定したデバイス、PnP 操作前に、と後に、またはシステムのスリープ中に状態遷移します。 スリープのテストでは、テスト対象のデバイスがすべてのサポートされるスリープ状態を循環できるシステムにできることを確認します。 さらに、単純な I/O ストレス テストを使用してこれらの状態変更した後、デバイスがまだ機能があるようになります。</p></td>
</tr>
</tbody>
</table>

 

 

 





