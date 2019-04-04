---
Description: この表は、使用の場合は、Windows 10 でサポートされて、作業にこれらのユース ケースの Oem 追加のタスクを実行する必要があります。
title: USB Type-C システムの OEM タスク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c82a8d7a88289e19d547fa006ea07accabd08ee7
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57463897"
---
# <a name="oem-tasks-for-usb-type-c-systems"></a>USB Type-C システムの OEM タスク


\[いくつかの情報は、リリース版の発売までに著しく変更される可能性がありますが、リリース前の製品に関連します。 Microsoft では、一切の保証、明示または黙示にかかわらず、ここで提供される情報はありません。\]

この表は、使用の場合は、Windows 10 でサポートされて、作業にこれらのユース ケースの Oem 追加のタスクを実行する必要があります。




<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>ユース ケース</th>
<th>Windows のサポート</th>
<th>OEM タスク</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>電源の配信</strong></p>
<p>従来の充電器を使用して C-USB 型システムを課金のサポート (&lt;7.5W)、USB 型-C# の充電器 (&lt;15W)、充電器を電源配信 (台の 100 w +)</p></td>
<td><p>Windows 10 Mobile のシステムでは、</p>
<ul>
<li>により処理されます。 充電器を従来から充電中、 <a href="usb-device-side-drivers-in-windows.md" data-raw-source="[USB device-side drivers in Windows](usb-device-side-drivers-in-windows.md)">Windows での USB デバイス側ドライバー</a>します。</li>
<li>USB 型-C# の充電器 (電源の配信を実装するものを含む) からの課金は、コネクタ マネージャーの USB ドライバーによって処理されます。USB コネクタ マネージャー クラスの拡張機能 (UcmCx) とコネクタのクライアント ドライバー。 クライアント ドライバーでは、充電のポリシーを決定するためのハードウェアと通信し、その UcmCx では、さらに、充電調停ドライバー (CAD) に送信を転送します。 CAD は、課金に使用するソースを選択します。</li>
</ul>
<p>Windows 10 デスクトップ エディション (Home、Pro、Enterprise、および Education) システムでは、</p>
<ul>
<li>強力なデスクトップ パソコンの充電が解除されると、従来の充電器から充電はお勧めしません。</li>
<li>USB タイプ-c 充電器の課金は、USB コネクタ マネージャー クラスの拡張機能 (UcmCx) とコネクタのクライアント ドライバーによって処理されます。 システムは現在、どの電源を使用して消費電力量は指定しません。</li>
</ul>
<p></p>
<div class="alert">
<strong>注</strong>  低速の充電器が検出されたときに、ユーザーに通知します。
</div>
<div>
 
</div></td>
<td><p>充電中、ハードウェア、ファームウェア、およびクライアント ドライバーでポリシーを決定する必要があります。 ポリシーを主に課金が含まれます。</p>
<ul>
<li>電源 (プロバイダー) または電源シンク (コンシューマー)、システムは、ですか。</li>
<li>システムで電力量を使用する必要がありますか。</li>
<li>どの電源 (充電器) は、複数の電源が充電器) などに利用できない場合に使用するか</li>
</ul>
<p>電源配信準拠の充電器は、ハードウェアは、電源コントラクトには、電圧と現在をネゴシエートする必要があります。 ネゴシエートされた電源コントラクトは、USB コネクタ マネージャー クラス拡張 (UcmCx) または適切なアクションの USCI ドライバーにより、システムに転送する必要があります。</p>
<p>低速の充電器がシステムに接続されている場合、システムが UcmCx または UCSI を通じて通知する必要があります。</p>
<p>独自のレガシをサポートするために 高電圧または高現在メカニズム、充電中、追加のフィルター ドライバーを独自の充電器を検出し、レポートをインボックス ドライバーを Microsoft のインボックス USB 機能ドライバーの記述をする必要があります。</p>
<p><a href="bring-up-a-usb-type-c-connector-on-a-windows-system.md" data-raw-source="[Write a USB Type-C connector driver](bring-up-a-usb-type-c-connector-on-a-windows-system.md)">USB タイプ-c コネクタのドライバーを作成します。</a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/mt188012" data-raw-source="[USB filter driver for supporting proprietary chargers](https://msdn.microsoft.com/library/windows/hardware/mt188012)">独自の充電器をサポートするための USB フィルター ドライバー</a></p>
<div class="alert">
<strong>注</strong>  Windows はレガシ USB A と USB B USB microB コネクタの Power 配信をサポートしていません。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td><p><strong>USB デバイスと周辺機器を接続します。</strong></p>
<p>USB デバイス/周辺機器を接続する (デスクトップおよびモバイル) は、Windows システムの機能</p></td>
<td><p>Windows 10 デスクトップ エディションの場合は、ほとんどのデバイス クラスをサポートします。 デバイス ドライバーとそのインストール ファイルは、Windows に含まれる</p>
<p>Windows 10 Mobile を実行しているデバイスでは、接続でき、USB デバイス/周辺、一連のインボックス ドライバーと対話することができます。 オペレーティング システムでは、デバイス クラスのサブセットをサポートします。</p>
<p>参照してください、 <a href="supported-usb-classes.md" data-raw-source="[USB device class drivers included in Windows](supported-usb-classes.md)">USB デバイス クラス ドライバーが Windows に含まれる</a>します。</p></td>
<td><p>システムは、Windows がドライバーを含まないカスタム USB デバイスに接続する場合、汎用ドライバー (Winusb.sys) の読み込みまたはドライバーを作成することもできます。 ガイダンスについては、<a href="winusb-considerations.md" data-raw-source="[Choosing a driver model for developing a USB client driver](winusb-considerations.md)">USB クライアント ドライバーを開発するためのドライバー モデルを選択する</a>を参照してください。</p>
<p>Windows 10 デスクトップ エディションと Windows 10 Mobile を実行する 1 つのドライバーを記述することをお勧めします。 詳しくは、「<a href="https://msdn.microsoft.com/windows-drivers/develop/getting_started_with_universal_drivers" data-raw-source="[Getting Started with Universal Windows drivers](https://msdn.microsoft.com/windows-drivers/develop/getting_started_with_universal_drivers)">ユニバーサル Windows ドライバーの概要</a>」をご覧ください。</p>
<p>デバイスと通信するアプリケーションを作成するには、Windows ランタイム Api を使用します。 詳細については、<a href="talking-to-usb-devices-start-to-finish.md" data-raw-source="[Talking to USB devices, start to finish (UWP app)](talking-to-usb-devices-start-to-finish.md)">(UWP アプリ) を終了する開始の USB デバイスとの対話、</a>を参照してください。</p></td>
</tr>
<tr class="odd">
<td><strong>別のモード</strong>
<p>非 USB デバイスへの接続 (例: 監視) USB 型-C# のコネクタを使用します。</p>
 </td>
<td><p>Windows 10 では、ハードウェアは、これらの代替モードをサポートしている場合は、ディスプレイ ポート等/DockPort デバイスを検出することができます。</p>
<p>Windows 10 は、インボックス ドライバーは、ビルボードのデバイスおよびビルボード デバイスでは、エラーが発生したことを示している場合、ユーザーに通知します。</p></td>
<td><p>動作する別のモードは、システムとデバイスは、ハードウェアとファームウェアに代替のモードをサポートする必要があります。 別のモードと、モードをネゴシエートするために必要なタスクを実行します。 つまり、ネットワーク上の別のモードに USB 型-C# コネクタをマルチプレキシングで通常実行します。</p></td>
</tr>
<tr class="even">
<td><strong>ビルボード デバイス</strong>
<p>問題のトラブルシューティングを行うユーザーを支援するエラー状態に関する情報を表示します。</p></td>
<td><p>Windows 10 では、ビルボードのデバイスに、インボックス ドライバーを提供します。 および、ビルボード デバイスがエラーを示す場合、ユーザーに通知します。</p>
<p>場合、エラー通知を表示可能性があります。</p>
<ul>
<li>別のモードは、PC または Windows 10 を実行している電話でサポートされていません。</li>
<li>使用する場合、代替のモードは、ケーブルでサポートされていません。</li>
</ul>
最適な結果を PC または電話ケーブルで別のモードのデバイスまたはアダプターの要件を満たしていることを確認します。
<p></p></td>
<td><p>代替モード アダプターまたはデバイスを別のモードのネゴシエーションが成功したかどうかを示すビルボード デバイスを実装する必要があります。</p>
<p>別のモードのアダプターまたはデバイスは、その他の USB 機能を実装する場合、ビルボード記述子の内容を更新する必要がありますを切断および再接続機能を中断する可能性があること、デバイス (ファイル転送など場合、デバイスUSB 大容量記憶装置デバイスである)。 防ぐには、ビルボードの仕様では、お使いのデバイスで、統合されたハブを使用し、いずれかのポートは別の USB デバイスとして表示されるビルボード デバイスがあることをお勧めします。</p>
<p>詳細については、<a href="https://go.microsoft.com/fwlink/p/?linkid=620207" data-raw-source="[USB Device Class Definition for Billboard Devices specification](https://go.microsoft.com/fwlink/p/?linkid=620207)">ビルボード デバイス仕様の USB デバイス クラス定義</a>を参照してください。</p></td>
</tr>
<tr class="odd">
<td><strong>USB デュアル ロール</strong>
<p>2 つの Windows デバイスをつなぐ</p></td>
<td><p>2 つの Windows デバイスが相互に接続されたときに、システムには、適切なロールの各デバイスである必要があり、必要な場合は、ロールのスワップ操作を実行しますが決定します。</p>
<p>これをサポートするには、Windows 10 は、USB ロール スイッチ クラスの拡張機能フレームワークを使用してシステムの役割コント ローラーと通信できます。 このフレームワークの受信トレイ クライアント ドライバーは、Synopsys ロール デュアル コント ローラーも提供されます。</p>
<p>USB 型-C# のシステムでは、USB コネクタ マネージャは、最初にハードウェア ポート コント ローラーによって割り当てられたロールに関する情報を取得します。</p>
<p>USB の役割のスイッチのスタックと USB コネクタ マネージャー スタックを現在のロールを取得し、必要に応じて、システムのポートのロールを切り替えるハードウェアと通信します。</p>
<p></p>
<div class="alert">
<strong>注</strong>  USB 型-C# のピア ツー ピア接続など、PC が別の PC に接続されているか、別のモバイル デバイスにモバイル デバイスが接続されていることはできません。 このような接続では、ユーザーにエラーが表示されます。
</div>
<div>
 
</div></td>
<td><p>ロールのデュアル ポートは、適切なタイミングで適切なソフトウェア スタック (ホストまたは関数) が読み込まれるかどうかを確認するオペレーティング システムで動作する必要があります。</p>
<p>デュアル ロールの USB ポートが Windows ホストまたは関数のいずれかのモードに構成する必要があるように、システムを設計できます。 これらの設計は、USB ロール スイッチのスタックを使用する必要があります。 システムが Synopsys または ChipIdea のロールのデュアル コント ローラーを使用しない場合は、システムの役割のデュアル コント ローラー用の USB ロール切り替えのクライアント ドライバーを記述する必要があります。</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/mt628026" data-raw-source="[USB dual-role controller driver programming reference](https://msdn.microsoft.com/library/windows/hardware/mt628026)">USB デュアルロール コントローラー ドライバーのプログラミング参照</a></p>
<p>ファームウェアまたはドライバーの顧客が指定したポートに接続されているデバイスに応じて、ホストまたは関数のいずれかのポートとしてポートを構成するよう、システムを設計こともできます。 これらの設計では、必要があるか、このロジックで実装、ファームウェア、または USB コネクタ マネージャーのクライアント ドライバーで実装する必要があります。 これらのシステムで、Windows は、正しいソフトウェア スタックを自動的に読み込まれます。</p>
<p><a href="bring-up-a-usb-type-c-connector-on-a-windows-system.md" data-raw-source="[Write a USB Type-C connector driver](bring-up-a-usb-type-c-connector-on-a-windows-system.md)">USB タイプ-c コネクタのドライバーを作成します。</a></p></td>
</tr>
<tr class="even">
<td><strong>オーディオのアクセサリ</strong>
<p>USB タイプ-c コネクタは、オーディオ ジャックとして使用できます。</p></td>
<td>Windows 10 は、ハードウェアが、機能をサポートしている場合の 3.5 mm のオーディオ ジャックとして USB 型-C# のアナログ入力を検出することができます。
<p>USB 型-C# の仕様のコネクタでは、オーディオ アクセサリ モードを使用して、3.5"アナログのオーディオ ジャックのような使用する USB 型-c コネクタをできます。 Windows 10 には、通常 3.5"アナログ オーディオ デバイスとしてアクセサリを検出してオーディオ accessories の USB 型-C# のサポートを実装するシステムがサポートしています。</p></td>
<td>この機能を使用するには、ハードウェアまたはファームウェア検出オーディオ アクセサリが接続されている場合およびオーディオ型-C# の仕様どおりそのモードに切り替えます。 これは、USB 型-c コネクタのピンを 3.5"アナログ オーディオ コネクタのピンをマップすることによって行います。</td>
</tr>
</tbody>
</table>

 

USB 型-C# のコネクタは、システムの能力をシステムを他の周辺機器を接続します。 ドッキング ステーションに接続するためのワイヤード (有線) のドッキングを使用できます。 別の表示が検出された場合、システムは、表示するに射影できます。 ワイヤード (有線) のドッキングを有効にするには、電源配信、接続する USB デバイスと周辺機器、表示される OEM タスクが完了し、上記の表に代替のモードのユース ケースを確認します。

## <a name="related-topics"></a>関連トピック
[USB タイプ-c コネクタの Windows のサポート](oem-tasks-for-bringing-up-a-usb-typec.md)  



