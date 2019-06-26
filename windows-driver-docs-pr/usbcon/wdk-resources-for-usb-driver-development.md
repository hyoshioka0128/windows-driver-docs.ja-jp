---
Description: このトピックの「How to」のトピックでは、USB ドライバーのドキュメント セット。 各に関する「方法」のトピックでは、コード例を含む、一連の手順として一連タスクを示します。
title: USB クライアント ドライバーに関する一般的なタスク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ae8bf2cd77c58138cda95df8ef448e50f0ca2fb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356549"
---
# <a name="common-tasks-for-usb-client-drivers"></a>USB クライアント ドライバーに関する一般的なタスク


このトピックの「How to」のトピックでは、このドキュメント セット。 各に関する「方法」のトピックでは、コード例を含む、一連の手順として一連タスクを示します。

方法トピックでは、USB クライアント ドライバー タスクに関連するプロセスに関する詳細な手順について説明します。 一般に、トピックは、Microsoft Visual Studio 2012 に含まれている USB テンプレートで作成されたドライバーを拡張することを想定して書き込まれます。

この一覧には、USB クライアント ドライバーの操作方法に関するトピックへのリンクが含まれています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>タスク</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="tutorial--write-your-first-usb-client-driver--kmdf-.md" data-raw-source="[How to write your first USB client driver (KMDF)](tutorial--write-your-first-usb-client-driver--kmdf-.md)">最初、USB クライアント ドライバー (KMDF) を記述する方法</a></p></td>
<td><p>このトピックでは、単純なカーネル モード ドライバー フレームワーク (KMDF) を記述する Microsoft Visual Studio 11 の Professional Beta に付属する USB カーネル モード ドライバー テンプレートを使用します-ベースのクライアント ドライバー。 を構築してクライアント ドライバーをインストールしたら、デバイス マネージャーで、クライアント ドライバーを表示し、デバッガーでドライバーの出力を表示します。</p></td>
</tr>
<tr class="even">
<td><p><a href="implement-driver-entry-for-a-usb-driver--umdf-.md" data-raw-source="[How to write your first USB client driver (UMDF)](implement-driver-entry-for-a-usb-driver--umdf-.md)">最初、USB クライアント ドライバー (UMDF) を記述する方法</a></p></td>
<td><p>このトピックでは、ユーザー モード ドライバー フレームワーク (UMDF) を記述する Microsoft Visual Studio 11 Beta に付属する USB ユーザー モード ドライバー テンプレートを使用します-ベースのクライアント ドライバー。 を構築してクライアント ドライバーをインストールしたら、デバイス マネージャーで、クライアント ドライバーを表示し、デバッガーでドライバーの出力を表示します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="usb-configuration-descriptors.md" data-raw-source="[How to get the configuration descriptor](usb-configuration-descriptors.md)">構成記述子を取得する方法</a></p></td>
<td><p>このトピックでは、構成の重要なフィールドについて説明し、USB デバイスからの構成記述子を取得する方法についてステップ バイ ステップ ガイダンスが含まれます。</p></td>
</tr>
<tr class="even">
<td><p><a href="send-requests-to-the-usb-driver-stack.md" data-raw-source="[How to Submit an URB (WDM)](send-requests-to-the-usb-driver-stack.md)">URB (WDM) を送信する方法</a></p></td>
<td><p>このトピックでは、USB ドライバー スタックに特定の要求を処理するのに初期化された URB を送信するために必要な手順について説明します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-select-a-configuration-for-a-usb-device.md" data-raw-source="[How to select a configuration for a USB device](how-to-select-a-configuration-for-a-usb-device.md)">USB デバイスの構成を選択する方法</a></p></td>
<td><p>このトピックでは、ユニバーサル シリアル バス (USB) デバイスで、構成を選択する方法について学習します。 このトピックでは、URB を送信することで、選択構成要求を送信するプロセスについて説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="select-a-usb-alternate-setting.md" data-raw-source="[How to select an alternate setting in a USB interface](select-a-usb-alternate-setting.md)">USB インターフェイスで代替の設定を選択する方法</a></p></td>
<td><p>このトピックでは、選択インターフェイス USB インターフェイスでの代替設定をアクティブ化要求を発行する手順について説明します。 クライアント ドライバーでは、USB の設定を選択した後、この要求を発行する必要があります。 その構成内の各インターフェイスでの最初の代替設定をアクティブにも既定では、構成を選択します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-get-usb-pipe-handles.md" data-raw-source="[How to enumerate USB pipes](how-to-get-usb-pipe-handles.md)">USB パイプを列挙する方法</a></p></td>
<td><p>このトピックでは、USB パイプの概要を説明し、USB クライアント ドライバーで USB ドライバー スタックからパイプ ハンドルを取得するために必要な手順について説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-use-the-continous-reader-for-getting-data-from-a-usb-endpoint--umdf-.md" data-raw-source="[How to use the continuous reader for reading data from a USB pipe](how-to-use-the-continous-reader-for-getting-data-from-a-usb-endpoint--umdf-.md)">USB パイプからデータを読み取るための継続的なリーダーを使用する方法</a></p></td>
<td><p>このトピックでは、WDF の継続的なリーダー オブジェクトについて説明します。 このトピックの手順では、オブジェクトを構成し、USB パイプからデータの読み取りに使用する方法についてステップ バイ ステップの手順を提供します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="usb-control-transfer.md" data-raw-source="[How to send a USB control transfer](usb-control-transfer.md)">USB 制御転送を送信する方法</a></p></td>
<td><p>このトピックでは、コントロールの転送とクライアント ドライバーがデバイスを制御要求を送信する必要がある方法の構造について説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="usb-bulk-and-interrupt-transfer.md" data-raw-source="[How to transfer data to USB bulk endpoints](usb-bulk-and-interrupt-transfer.md)">USB 一括エンドポイントにデータを転送する方法</a></p></td>
<td><p>このトピックでは、USB 一括転送について、簡単な概要を説明します。 クライアント ドライバーが送信して、デバイスから大量のデータを受信する方法についての詳細な手順についても提供します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-open-streams-in-a-usb-endpoint.md" data-raw-source="[How to open and close static streams in a USB bulk endpoint](how-to-open-streams-in-a-usb-endpoint.md)">USB 一括エンドポイントで静的なストリームを開閉する方法</a></p></td>
<td><p>このトピックでは、静的なストリームの機能について説明し、USB クライアント ドライバーが開くし、USB 3.0 デバイスの一括エンドポイントでのストリームを閉じる方法について説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="transfer-data-to-isochronous-endpoints.md" data-raw-source="[How to transfer data to USB isochronous endpoints](transfer-data-to-isochronous-endpoints.md)">USB アイソクロナス エンドポイントにデータを転送する方法</a></p></td>
<td><p>このトピックでは、クライアント ドライバーが、USB 要求ブロック (URB) して、USB デバイスでサポートされているアイソクロナス エンドポイントからデータの転送を作成する方法について説明します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-recover-from-usb-pipe-errors.md" data-raw-source="[How to recover from USB pipe errors](how-to-recover-from-usb-pipe-errors.md)">USB パイプ エラーから回復する方法</a></p></td>
<td><p>このトピックでは、ときに、USB パイプへのデータ転送を試みることができますの手順については失敗します。 このトピックでカバーで説明されているメカニズムは、中止、リセットして、一括、割り込み、アイソクロナス パイプでポート operations のサイクルします。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-send-chained-mdls.md" data-raw-source="[How to send chained MDLs](how-to-send-chained-mdls.md)">チェーンされた MDLs を送信する方法</a></p></td>
<td><p>このトピックでは、チェーンの MDLs 機能、USB ドライバー スタックと、クライアント ドライバーが MDL 構造体のチェーンとして転送バッファーを送信する方法の詳細について学びます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="register-a-composite-driver.md" data-raw-source="[How to Register a Composite Device](register-a-composite-driver.md)">複合デバイスを登録する方法</a></p></td>
<td><p>このトピックでは、複合のドライバーと呼ばれる、USB 多機能デバイスのドライバーを登録および基になる USB ドライバー スタックと複合デバイスの登録を解除する方法について説明します。 Microsoft 提供のドライバーで、Usbccgp.sys は、Windows によって読み込まれる既定の複合ドライバーです。 このトピックの手順では、カスタム Windows Driver Model WDM ベース複合ドライバーで、Usbccgp.sys を置換するには適用されます。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to--implement-remote-and-function-wake-support.md" data-raw-source="[How to Implement Function Suspend in a Composite Driver](how-to--implement-remote-and-function-wake-support.md)">複合のドライバーで中断する関数を実装する方法</a></p></td>
<td><p>このトピックでは、関数の概要が中断し、関数リモート ウェイク アップ機能ユニバーサル シリアル バス (USB) の 3.0 の多機能デバイス (複合デバイス) を提供します。 このトピックでは、ドライバーでは複合デバイスを制御するこれらの機能を実装する方法について説明します。 置換で、Usbccgp.sys 複合のドライバーをトピックが適用されます。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[ユニバーサル シリアル バス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/)  



