---
Description: Windows を実行している USB タイプ C システムでユーザーが取得する可能性のある、Windows 10 のメッセージのトラブルシューティングに関する考えられる原因と解決策。
title: USB タイプのメッセージのトラブルシューティング-C Windows システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 060ecddcb41ae474d0845afc0b9f11216525c407
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242927"
---
# <a name="troubleshoot-messages-for-a-usb-type-c-windows-system"></a>USB タイプのメッセージのトラブルシューティング-C Windows システム


Windows を実行している USB タイプ C システムでユーザーが取得する可能性のある、Windows 10 のメッセージのトラブルシューティングに関する考えられる原因と解決策。

USB タイプ C コネクタの対称および元に戻すことができる設計により、ユーザーは Windows を実行しているシステムに接続し、任意の USB タイプ C デバイスに接続し、拡張充電や代替モードなどの新機能を使用することができます。 ただし、ハードウェアやソフトウェアの制限の特定の組み合わせによって、これらの機能の一部が正常に機能しなくなる場合があります。 Windows 10 は、ユーザーがこれらの問題のトラブルシューティングを行うのに役立つ、一連の USB タイプ C 通知を提供します。

このトピックでは、USB タイプ C システムは、デスクトップエディション (Home、Pro、Enterprise、および教育) 用の Windows 10 を実行している PC、または Windows 10 Mobile を実行しているモバイルデバイスを指します。

**システムの USB タイプ C コネクタに関連するメッセージのトラブルシューティング**

-   [USB デバイスを修正できる可能性があります](#-1)
-   [デバイスの充電速度が低下しています](#-2)
-   [USB デバイスが動作しない可能性がある](#-3)
-   [USB 接続を改善してみてください](#-4)
-   [表示接続が制限されている](#-5)
-   [これら2台の Pc (モバイルデバイス) は通信できません](#-6)

## <a href="" id="-1"></a>USB デバイスを修正できる可能性があります


\* * USB デバイスで問題が発生しました。 この問題を解決するには、次の手順を実行します。 (エラーコード \_\_\_\_) * *

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>考えられる原因</th>
<th>推奨される解像度</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>デバイスハードウェアから問題が報告されたか、デバイスドライバに問題があります。</p></td>
<td><ol>
<li>エラーコードを確認します。
<ul>
<li>Windows 10 for desktop エディションのシステムでは、デバイスマネージャーを開き、デバイスを検索します。 黄色い感嘆符でマークされています。 ノードを右クリックし、[デバイスのプロパティ] を開きます。 エラーコードは [<strong>デバイスの状態</strong>] の下にあります。</li>
<li>Windows 10 Mobile システムでは、通知にエラーコードが表示されます。</li>
</ul></li>
<li><a href="https://go.microsoft.com/fwlink/p/?LinkId=526896" data-raw-source="[this article](https://go.microsoft.com/fwlink/p/?LinkId=526896)">この記事</a>で説明されているトラブルシューティングの手順に従います。</li>
</ol>
<div class="alert">
<strong>メモ</strong> コード28以外のデバイスマネージャーに表示されるすべてのエラーコードに適用されます。
</div>
<div>

</div></td>
</tr>
</tbody>
</table>



## <a href="" id="-2"></a>デバイスの充電速度が低下しています


**課金速度を上げるには、デバイスに付属の充電器とケーブルを使用します。**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>考えられる原因</th>
<th>推奨される解像度</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li>チャージャーはシステムと互換性がありません。
<div class="alert">
<strong>メモ</strong> 非 USB タイプ-C 充電器は、USB バッテリ充電1.2 仕様をサポートしています。 これらの充電器の一部は、独自の課金メカニズムを使用しています。 システムがこれらの充電器をすべてサポートしていない可能性があります。
</div>
<div>

</div></li>
<li>チャージャーは、システムの充電に十分な能力がありません。</li>
<li>チャージャーがシステムの充電ポートに接続されていません。</li>
<li>充電ケーブルが充電器またはシステムの電力要件を満たしていません。</li>
</ul>
<div class="alert">
<strong>注:</strong><br/><p>USB タイプ C コネクタを使用するシステムでは、電力制限が高く、最大5V、3A、15W がサポートされています。 コネクタで<a href="https://go.microsoft.com/fwlink/p/?LinkID=623310" data-raw-source="[USB Power Delivery](https://go.microsoft.com/fwlink/p/?LinkID=623310)">USB 電力配信</a>(業界標準) がサポートされている場合は、高いパワーレベルでより高速に課金される可能性があります。</p>
<p>課金の速度を向上させるために、システム、チャージャー、ケーブルで業界標準をサポートする必要があります。 さらに、充電能力とケーブルは、システムが最適に充電するために必要な電力レベルをサポートしている必要があります。 たとえば、システムの充電に12V と3A が必要な場合、5V の3A チャージャーはシステムを最適に請求できません。</p>
</div>
<div>

</div></td>
<td><ul>
<li>デバイスに付属の充電器とケーブルを使用します。</li>
<li>システムの充電 USB タイプ C ポートにチャージャーを接続していることを確認します。</li>
</ul></td>
</tr>
</tbody>
</table>



## <a href="" id="-3"></a>USB デバイスが動作しない可能性がある


**PC に接続してみてください。**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>考えられる原因</th>
<th>推奨される解像度</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>接続されているデバイスのドライバーは、システムで実行されているバージョンの Windows ではサポートされていません。 サポートされているデバイスの詳細については、「 <a href="supported-usb-classes.md" data-raw-source="[USB device class drivers included in Windows](supported-usb-classes.md)">Windows に含まれる USB デバイスクラスドライバー</a>」を参照してください。</p>
<div class="alert">
<strong>メモ</strong> モバイルシステムには、他の USB 周辺機器と接続する機能があります。 ただし、PC に接続するデバイスによっては、モバイルシステムに接続できないものもあります。 上記の一覧で、サポートされているデバイスを確認します。
</div>
<div>

</div></td>
<td><ul>
<li>最新のドライバーパッケージがあることを確認して、最新バージョンの Windows を実行していることを確認します。 詳細については、「 <a href="https://go.microsoft.com/fwlink/p/?LinkID=698739" data-raw-source="[Windows 10 Updates](https://go.microsoft.com/fwlink/p/?LinkID=698739 )">Windows 10 の更新プログラム</a>」を参照してください。</li>
<li>最新バージョンを既に実行している場合は、代わりにデバイスを PC に接続してみてください。</li>
</ul></td>
</tr>
</tbody>
</table>



## <a href="" id="-4"></a>USB 接続を改善してみてください


**接続しているデバイスがサポートされていること、および適切なケーブルを使用していることを確認します。**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>考えられる原因</th>
<th>推奨される解像度</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li>お使いのシステムでサポートされていない新しい USB タイプ C 機能を使用してデバイスを接続しました。</li>
<li>ケーブルでサポートされていない新しい USB タイプ C 機能を使用してデバイスを接続しました。</li>
</ul>
<p>USB タイプ-C では、代替モードと呼ばれる新機能が導入されています。これにより、非 USB プロトコルで USB タイプ C ケーブルを使用できるようになります。 たとえば、代替モードを使用する dock には、USB 経由でビデオ信号を送信する機能があります。</p>
<p>代替モードを機能させるには、ハードウェアと、PC/電話およびデバイスまたはアダプターのソフトウェアが、代替モードをサポートしている必要があります。 また、特定の代替モードでは、特定の USB タイプ C ケーブルが必要になる場合があります。</p></td>
<td><ul>
<li>システムが接続されているデバイスの機能をサポートしていることを確認します。</li>
<li>ケーブルが接続されているデバイスの機能をサポートしていることを確認します。</li>
</ul></td>
</tr>
</tbody>
</table>



## <a href="" id="-5"></a>表示接続が制限されている


**DisplayPort/MHL 接続が機能しない可能性があります。別のケーブルを使用してみてください。**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>考えられる原因</th>
<th>推奨される解像度</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li>お使いのシステムでサポートされていない新しい USB タイプ C 機能を使用してデバイスを接続しました。</li>
<li>ケーブルでサポートされていない新しい USB タイプ C 機能を使用してデバイスを接続しました。</li>
</ul>
<p>USB タイプ-C では、代替モードと呼ばれる新機能が導入されています。 この機能を使用すると、usb タイプ C ケーブルを介して非 USB プロトコルを実行できます。同時に、usb 2.0 および充電機能が同時に維持されます。 次に、代替モードの表示を示します。</p>
<ul>
<li><p><strong>DisplayPort</strong> /<strong>DockPort</strong></p>
<p>この代替モードでは、ユーザーは、USB コネクタ経由で外部 DisplayPort を表示することができます。</p></li>
<li><p><strong>MHL</strong></p>
<p>MHL の代替モードでは、ユーザーは MHL をサポートする外部ディスプレイにビデオ/オーディオを投影できます。</p></li>
</ul>
<p>システム、デバイス、アダプター、またはケーブルのハードウェアとソフトウェアでは、 <strong>DisplayPort</strong> /<strong>DockPort</strong>または<strong>mhl</strong>の代替モードはサポートされていません。</p></td>
<td><ul>
<li>システム、デバイス、およびケーブルが、 <strong>DisplayPort</strong> /<strong>DockPort</strong>または<strong>mhl</strong>の代替モードをサポートしていることを確認します。</li>
</ul></td>
</tr>
</tbody>
</table>



## <a href="" id="-6"></a>これら2台の Pc (モバイルデバイス) は通信できません


**そのうちの1つをモバイルデバイス (PC) に接続して、目標を達成してみてください。**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>考えられる原因</th>
<th>推奨される解像度</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li>Windows 10 を実行する2台の Pc をデスクトップエディションとして接続することはできません。</li>
<li>Windows 10 Mobile を実行している2つのモバイルデバイスを接続することはできません。</li>
</ul></td>
<td>この接続シナリオはサポートされていません。</td>
</tr>
</tbody>
</table>










