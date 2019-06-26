---
Description: このセクションでは、USB ハードウェアまたはソフトウェアのテスト、操作とその他のシステム イベントのトレースをキャプチャして、USB ドライバー スタックをクライアント ドライバーまたはアプリケーションによって送信された要求に応答する方法を確認に使用できるツールについて説明します。
title: Windows での USB ハードウェア、ドライバー、アプリのテスト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 221a69c4b62df5f07a72be8c4577d8b5e734b9f0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356613"
---
# <a name="testing-usb-hardware-drivers-and-apps-in-windows"></a>Windows での USB ハードウェア、ドライバー、アプリのテスト


このセクションでは、USB ハードウェアまたはソフトウェアのテスト、操作とその他のシステム イベントのトレースをキャプチャして、USB ドライバー スタックをクライアント ドライバーまたはアプリケーションによって送信された要求に応答する方法を確認に使用できるツールについて説明します。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>トピック</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="microsoft-usb-test-tool--mutt--devices.md" data-raw-source="[Microsoft USB Test Tool (MUTT) devices](microsoft-usb-test-tool--mutt--devices.md)">Microsoft USB Test Tool (MUTT) デバイス</a></p></td>
<td><p>Microsoft USB Test Tool (MUTT) には、USB のハードウェアは Microsoft USB ドライバー スタックとの相互運用性をテストするためのデバイスのコレクションです。 このセクションでは、MUTT デバイス、テスト、デバイスを使用して実行でき、コント ローラー、ハブ、デバイス、トポロジの提案し、BIOS および UEFI テストのさまざまな種類の概要を提供します。</p>
<p>MUTT デバイスと通信、MUTT ソフトウェア パッケージが必要です。 このパッケージには、いくつかのテスト ツールとハードウェア テスト エンジニア テスト、USB コント ローラーや Microsoft USB ドライバー スタックとハブの相互運用性のためのドライバーが含まれています。 テスト ツールは、USB ホスト コント ローラーのソフトウェア、ハードウェア (ファームウェアを含む) およびホスト コント ローラーとデバイスの間にインストールされているいずれかの USB ハブを検証します。</p></td>
</tr>
<tr class="even">
<td><p><a href="usb-test-tools.md" data-raw-source="[USB test tools](usb-test-tools.md)">USB テスト ツール</a></p></td>
<td><p>USB デバイスとドライバーをテストに使用できるさまざまなツールについて説明します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="test-usb-type-c-systems-with-mutt-connex-c.md" data-raw-source="[Test USB Type-C systems with USB Type-C ConnEx](test-usb-type-c-systems-with-mutt-connex-c.md)">USB タイプ C ConnEx で USB 型-c システムをテストします。</a></p></td>
<td><p>USB タイプ C 接続 Exerciser (USB 型 C ConnEx) ハードウェア ボードでは、Arduino ボード用カスタム シールドです。 シールドは、USB 型-C# のシナリオの相互運用性のテストを自動化するための 4 対一スイッチを提供します。</p></td>
</tr>
<tr class="even">
<td><p><a href="type.md" data-raw-source="[USB Type-C manual interoperability test procedures](type.md)">USB タイプ-C 手動の相互運用性のテスト手順</a></p></td>
<td><p>このトピックでは、有効になっている C USB の型システムと Windows の相互運用性をテストする方法について説明します。 さまざまな機能を実行するデバイスとシステムの製造元とストレス テスト システムと USB 型-C# のコネクタを公開しているデバイスでのガイドラインを示します。 リーダーが公式 USB 仕様と xHCI の相互運用性テスト手順、USB.ORG からダウンロードできます。 これに精通するいると想定しています。</p></td>
</tr>
<tr class="odd">
<td><p><a href="mutt-testing-options.md" data-raw-source="[How to prepare the test system to run MUTT test tools](mutt-testing-options.md)">MUTT テスト ツールを実行するテスト システムを準備する方法</a></p></td>
<td><p>MUTT デバイスを使用する前に、テスト システムを準備する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-run-stress-and-transfer-and-super-mutt-performance-tests-for-mutt-devices.md" data-raw-source="[How to run stress and transfer performance tests for MUTT devices](how-to-run-stress-and-transfer-and-super-mutt-performance-tests-for-mutt-devices.md)">MUTT デバイス用のテストをストレスを実行し、パフォーマンスを転送する方法</a></p></td>
<td><p>ストレスおよび転送 SuperMUTT パフォーマンス テストを実行する方法を確認します。</p>
<p>ストレスおよび転送テストは、bus プロトコルとホスト コント ローラーのソフトウェアの飽和に特化しました。 これらのテストでは、いくつかの同時転送の I/O と MUTT デバイスに取り消しを実行します。 MUTT ファームウェアは、これらのテストの転送が失敗するプログラミングされます。 このようなエラーがエラーをエミュレートする条件をコント ローラーまたは USB ドライバー スタックに USB のストレス条件下で公開されます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-run-device-fundamental-tests-in-visual-studio-for-connected-mutt-devices.md" data-raw-source="[How to run system power devfund tests in Visual Studio for MUTT devices](how-to-run-device-fundamental-tests-in-visual-studio-for-connected-mutt-devices.md)">MUTT デバイスの Visual Studio でのシステム電源 devfund テストを実行する方法</a></p></td>
<td><p>MUTT デバイスで利用できるポートに関連付けられている実行が必要なデバイスの基本的なテストについて説明しますストレスおよび転送テストおよびシステム電源のテストを実行します。</p>
<p>これらのテストは、システム電源イベントを実行すると同時に、シンプルなデバイスの転送を実行します。 Devfund テストは Windows 8 でのみ実行できますに注意してください。 ことはできません<a href="how-to-run-stress-and-transfer-and-super-mutt-performance-tests-for-mutt-devices.md" data-raw-source="[run stress and transfer tests](how-to-run-stress-and-transfer-and-super-mutt-performance-tests-for-mutt-devices.md)">ストレスを実行し、テストに転送</a>およびシステムの電源が同時にテストします。 別のシステムには、これらのテストを実行します。 ただし、ストレスの転送とシステム間で切り替えることができますの電源をテストします。 これを行うに最初の一連のテストの完了や、コンピューターを再起動し、次のテストの指示に従います。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-run-bios-uefi-testing-with-the-mutt-device.md" data-raw-source="[BIOS/UEFI testing with the MUTT devices](how-to-run-bios-uefi-testing-with-the-mutt-device.md)">BIOS および UEFI の MUTT デバイスでのテスト</a></p></td>
<td><p>BIOS および UEFI テストには、USB ブートとオペレーティング システムのコント ローラーのハンドオフが検証します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-run-hub-testing-with-the-mutt-device.md" data-raw-source="[Test USB hubs with MUTT devices](how-to-run-hub-testing-with-the-mutt-device.md)">MUTT デバイスと USB ハブをテストします。</a></p></td>
<td><p>ハブのテストの目的では、デバイスからのトラフィック パターンの完全なセットを生成します。 テストすることができます、アップ ストリームの SuperMUTT パックを追加することでシナリオを切断します。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-run-controller-and-device-testing-with-the-mutt-device.md" data-raw-source="[Test USB host controllers with MUTT devices](how-to-run-controller-and-device-testing-with-the-mutt-device.md)">MUTT デバイスで USB ホスト コント ローラーをテストします。</a></p></td>
<td><p>コント ローラーのテストの目的では、ハブとデバイスからのトラフィック パターンの完全なセットを生成します。 これにより、コント ローラーと完全にテストするには、そのファームウェアの内部状態ができます。 MUTT デバイスが自動的に可能なプロトコルのさまざまなシナリオを生成する方法を提供することで、テストできます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="tools-in-the-package.md" data-raw-source="[Test USB devices with MUTT devices](tools-in-the-package.md)">MUTT デバイスで USB デバイスをテストします。</a></p></td>
<td><p>デバイスのテストの目標は、さまざまなハブ シナリオに対してもデバイスの使用状況をテストして、システムの電源の状態。 MUTT パックおよび SuperMUTT パック デバイスは、別のハブ間でのシナリオとシステムの電源状態のシナリオの接続/切断するデバイスを公開する方法を提供できます。 それぞれに USB 2.0 と 3.0 のハブ MUTT パックおよび SuperMUTT パックのデバイスにアタッチされている場合は、デバイスをテストします。</p></td>
</tr>
<tr class="even">
<td><p><a href="windows-hardware-certification-kit-tests-for-usb.md" data-raw-source="[Windows Hardware Lab Kit Tests for USB](windows-hardware-certification-kit-tests-for-usb.md)">USB の Windows ハードウェア ラボ キット テスト</a></p></td>
<td><p>Windows ハードウェア ラボ キット (HLK) テストは、システム、USB ホスト コント ローラー、ハブ、およびデバイスの追加テストに使用できます。 これらのテストは、基本的なデバイス機能、信頼性、および Windows との互換性について説明します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[ユニバーサル シリアル バス (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  



