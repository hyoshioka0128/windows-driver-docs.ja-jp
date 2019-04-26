---
Description: 考えられる原因と解決策をユーザーが Windows を実行している USB 型-C# のシステムで発生可能性のある Windows 10 でのメッセージのトラブルシューティングします。
title: USB タイプ C Windows システムのメッセージをトラブルシューティングします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 060ecddcb41ae474d0845afc0b9f11216525c407
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355468"
---
# <a name="troubleshoot-messages-for-a-usb-type-c-windows-system"></a>USB タイプ C Windows システムのメッセージをトラブルシューティングします。


考えられる原因と解決策をユーザーが Windows を実行している USB 型-C# のシステムで発生可能性のある Windows 10 でのメッセージのトラブルシューティングします。

USB 型-c コネクタの対称的、および元に戻すことのデザインでは、任意の型から C の USB デバイスを接続し、強化された課金と代替モードなどの新機能を使用して Windows を実行しているシステムを接続することができます。 ただし、ハードウェアやソフトウェアの制限事項の特定の組み合わせを妨げる可能性これらの機能の一部正常に機能します。 Windows 10 では、これらの問題をトラブルシューティングするのに役立ちます USB 型-C# の通知のセットを提供します。

このトピックでは、C-USB 型システムはデスクトップ エディション (Home、Pro、Enterprise、および教育機関向け) または Windows 10 Mobile を実行しているモバイル デバイスの Windows 10 を実行している PC を示します。

**システムの種類 C の USB コネクタに関連するメッセージのトラブルシューティング**

-   [USB デバイスを修正できる場合があります。](#-1)
-   [デバイスが充電緩やかに変化](#-2)
-   [USB デバイスが動作しない可能性があります。](#-3)
-   [USB 接続の改善を再試行してください。](#-4)
-   [接続の表示は制限されています](#-5)
-   [これら 2 つの Pc (モバイル デバイス) とは通信できません。](#-6)

## <a href="" id="-1"></a>USB デバイスを修正できる場合があります。


* *、USB デバイスがある問題に直面します。 これを修正しようとするこれらの手順に従います。 (エラー コード\_ \_ \_ \_) * *

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>考えられる原因</th>
<th>推奨される解決方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>デバイスのハードウェアが問題を報告またはデバイス ドライバーに障害が発生します。</p></td>
<td><ol>
<li>エラー コードに注意してください。
<ul>
<li>Windows 10 デスクトップ エディションのシステムで、デバイス マネージャーを開き、デバイスを探します。 これは、黄色の感嘆符でマークされます。 開いているデバイス プロパティ、ノードで右クリックします。 下のエラー コードは<strong>デバイス ステータス</strong>します。</li>
<li>Windows 10 Mobile のシステムでは、通知は、エラー コードを示します。</li>
</ul></li>
<li>説明されているトラブルシューティングの手順に従います<a href="https://go.microsoft.com/fwlink/p/?LinkId=526896" data-raw-source="[this article](https://go.microsoft.com/fwlink/p/?LinkId=526896)">今回</a>します。</li>
</ol>
<div class="alert">
<strong>注</strong>コード 28 を除くデバイス マネージャーに表示されるすべてのエラー コードに適用されます。
</div>
<div>

</div></td>
</tr>
</tbody>
</table>



## <a href="" id="-2"></a>デバイスが充電緩やかに変化


**課金の速度、充電器とデバイスに付属しているケーブルを使用します。**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>考えられる原因</th>
<th>推奨される解決方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li>充電器は、システムと互換性がありません。
<div class="alert">
<strong>注</strong>USB 以外の型から C の充電器が USB バッテリの充電 1.2 の仕様をサポートします。 これらの充電器の一部は、独自の充電機構を使用します。 システムが、これらすべての充電器をサポートしていません。
</div>
<div>

</div></li>
<li>充電器は、強力な課金システムではありません。</li>
<li>充電器は、システムの充電中のポートに接続されていません。</li>
<li>課金のケーブルが充電器またはシステムの電源の要件を満たしていません。</li>
</ul>
<div class="alert">
<strong>注:</strong><br/><p>USB タイプ-c コネクタを持つシステムが電源上限の引き上げ、5 v、3A、15W までをサポートできます。 コネクタがサポートしている場合<a href="https://go.microsoft.com/fwlink/p/?LinkID=623310" data-raw-source="[USB Power Delivery](https://go.microsoft.com/fwlink/p/?LinkID=623310)">USB 電力配信</a>(industry standard)、その料金を課金できます高速 power のより高いレベルでします。</p>
<p>高速の課金のメリットを活用するためには、システム、充電器、およびケーブルは、業界標準をサポートする必要があります。 さらに、充電器とケーブルは、最適な状態で、課金、システムで必要な電力レベルをサポートする必要があります。 たとえば、システム充電中の 5 v の 12 v と 3A が必要な場合 3A 充電器ことはできません課金システム最適。</p>
</div>
<div>

</div></td>
<td><ul>
<li>充電器とデバイスに付属しているケーブルを使用します。</li>
<li>充電器、システムに充電型-C# の USB ポートに接続していることを確認します。</li>
</ul></td>
</tr>
</tbody>
</table>



## <a href="" id="-3"></a>USB デバイスが動作しない可能性があります。


**PC に接続してみてください。**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>考えられる原因</th>
<th>推奨される解決方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>接続されたデバイスのドライバーは、システムで実行されている Windows のバージョンでサポートされていません。 サポートされているデバイスについては、次を参照してください。 <a href="supported-usb-classes.md" data-raw-source="[USB device class drivers included in Windows](supported-usb-classes.md)">USB デバイス クラス ドライバーが Windows に含まれる</a>します。</p>
<div class="alert">
<strong>注</strong>モバイル システムが他の USB 周辺機器を接続する機能。 ただし、PC に接続するすべてのデバイスは、モバイル システムに接続できます。 サポートされているデバイスには、上記の一覧を確認します。
</div>
<div>

</div></td>
<td><ul>
<li>最新のドライバー パッケージがあるように、Windows の最新バージョンが実行していることを確認します。 詳しくは、次を参照してください。 <a href="https://go.microsoft.com/fwlink/p/?LinkID=698739" data-raw-source="[Windows 10 Updates](https://go.microsoft.com/fwlink/p/?LinkID=698739 )">Windows 10 更新プログラム</a>します。</li>
<li>最新バージョンを既に実行している場合は、代わりに、デバイスを PC に接続してみてください。</li>
</ul></td>
</tr>
</tbody>
</table>



## <a href="" id="-4"></a>USB 接続の改善を再試行してください。


**接続しているデバイスがサポートされており、適切なケーブルを使用していることを確認してください。**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>考えられる原因</th>
<th>推奨される解決方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li>新しいデバイスを接続した USB 型-C# 機能しているシステムでサポートされていません。</li>
<li>デバイスは、ケーブルでサポートされていない新しい USB 型-C# の機能を使用して接続されています。</li>
</ul>
<p>USB タイプ-C では、型-C# の USB ケーブルで実行するための USB 以外のプロトコルを使用する別のモードと呼ばれる新しい機能について説明します。 たとえば、dock 代替モードを使用するには、USB 経由でビデオ信号を送信する権限を持ちます。</p>
<p>動作する別のモードは、ハードウェアとソフトウェア PC/電話とデバイス、またはアダプターでは、代替のモードをサポートする必要があります。 さらに、特定の代替モードでは、特定の型から C の USB ケーブルを必要があります。</p></td>
<td><ul>
<li>システムが接続されているデバイスの機能をサポートすることを確認します。</li>
<li>ケーブルが接続されているデバイスの機能をサポートすることを確認します。</li>
</ul></td>
</tr>
</tbody>
</table>



## <a href="" id="-5"></a>接続の表示は制限されています


**ディスプレイ ポート等/MHL 接続が機能しない可能性があります。別のケーブルを使用してください。**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>考えられる原因</th>
<th>推奨される解決方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li>システムでサポートされていない新しい USB 型-C# の機能を使用してデバイスを接続されています。</li>
<li>デバイスは、ケーブルでサポートされていない新しい USB 型-C# の機能を使用して接続されています。</li>
</ul>
<p>USB タイプ-C では、別のモードと呼ばれる新しい機能について説明します。 機能は、同時に USB 2.0 の維持および機能の充電中に、型-C# の USB ケーブルで実行するための USB 以外のプロトコルを使用できます。 代替の表示モードを次に示します。</p>
<ul>
<li><p><strong>DisplayPort</strong> /<strong>DockPort</strong></p>
<p>この代替モードは、USB コネクタ経由で外部ディスプレイ ポート等を表示するには、オーディオ/ビデオをプロジェクトにできます。</p></li>
<li><p><strong>MHL</strong></p>
<p>MHL 代替モードはにより、ユーザーが外部プロジェクトのビデオ/オーディオ MHL をサポートするを表示します。</p></li>
</ul>
<p>ハードウェアとソフトウェア システム、デバイスまたはアダプター、またはケーブルにはサポートしていません、<strong>ディスプレイ ポート等</strong> /<strong>DockPort</strong>または<strong>MHL</strong>別のモード。</p></td>
<td><ul>
<li>確認システム、デバイス、およびケーブル サポート<strong>ディスプレイ ポート等</strong> /<strong>DockPort</strong>または<strong>MHL</strong>別のモード。</li>
</ul></td>
</tr>
</tbody>
</table>



## <a href="" id="-6"></a>これら 2 つの Pc (モバイル デバイス) とは通信できません。


**モバイル デバイス (PC) の目標を達成するために 1 つ接続してみます。**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>考えられる原因</th>
<th>推奨される解決方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li>デスクトップ エディションの Windows 10 を実行している 2 つの Pc に接続することはできません。</li>
<li>Windows 10 Mobile を実行している 2 つのモバイル デバイスを接続することはできません。</li>
</ul></td>
<td>この接続のシナリオがサポートされていません。</td>
</tr>
</tbody>
</table>










