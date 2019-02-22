---
Description: The topics in this section provides an USB pipes, URBs for I/O requests, and describes how a client driver can use the device driver interfaces (DDIs) to transfer data to and from a USB device.
title: USB クライアント ドライバーでの USB データ転送の送信
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: dd92cf4ac5eb08d2123c28fa604672ab74df39aa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557539"
---
# <a name="sending-usb-data-transfers-in-usb-client-drivers"></a>USB クライアント ドライバーでの USB データ転送の送信


このセクションのトピックでは、I/O 要求の USB パイプと翻訳の詳細についての情報を提供し、クライアント ドライバーがデバイス ドライバー インターフェイス (Ddi) を使用して、USB デバイスとの間のデータを転送する方法について説明します。




ホスト コント ローラーと USB デバイス間でデータを移動するたびに、転送が行われます。 一般に、USB 転送大別できますコントロールに転送およびデータ転送。 すべての USB デバイスは、コントロールの転送をサポートする必要があり、データ転送のエンドポイントをサポートすることができます。 転送の種類ごとの種類に関連付けられて*USB エンドポイント*(デバイスでバッファー)。 コントロールの転送に既定のエンドポイントに関連付けられてし、データ転送は、一方向のエンドポイントを使用します。 データ転送の種類は、割り込み、一括でおよびアイソクロナス エンドポイントを使用します。 USB ドライバー スタックと呼ばれる通信チャネルを作成する、*パイプ*デバイスでサポートされている各エンドポイント。 パイプの一方の end は、デバイスのエンドポイントです。 パイプのもう一方の端は、ホスト コント ローラーでは常にします。

デバイスの I/O 要求を送信する前に、クライアント ドライバーは、USB デバイスから構成、インターフェイス、エンドポイント、仕入先、およびクラスに固有の記述子に関する情報を取得する必要があります。 さらに、ドライバーは、デバイスも構成する必要があります。 デバイスの構成には、構成、および各インターフェイス内の別の設定を選択するなどのタスクが含まれます。 各代替の設定は、データ転送の使用可能な 1 つまたは複数の USB エンドポイントを指定できます。

デバイスの構成については、次を参照してください。 [USB デバイスの構成の選択方法](how-to-select-a-configuration-for-a-usb-device.md)と[USB インターフェイスで代替の設定を選択する方法](select-a-usb-alternate-setting.md)します。

クライアント ドライバーがデバイスを構成した後、ドライバーは現在選択されている別の設定では、各エンドポイントの USB ドライバー スタックによって作成されたパイプ ハンドルへのアクセスを持ちます。 エンドポイントにデータを転送するには、クライアント ドライバーは、URB 要求の種類に固有の書式を設定して要求を作成します。

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
<td><p><a href="usb-control-transfer.md" data-raw-source="[How to send a USB control transfer](usb-control-transfer.md)">USB 制御転送を送信する方法</a></p></td>
<td><p>このトピックでは、コントロールの転送とクライアント ドライバーがデバイスを制御要求を送信する必要がある方法の構造について説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-get-usb-pipe-handles.md" data-raw-source="[How to enumerate USB pipes](how-to-get-usb-pipe-handles.md)">USB パイプを列挙する方法</a></p></td>
<td><p>このトピックでは、USB パイプの概要を説明し、USB クライアント ドライバーで USB ドライバー スタックからパイプ ハンドルを取得するために必要な手順について説明します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-use-the-continous-reader-for-getting-data-from-a-usb-endpoint--umdf-.md" data-raw-source="[How to use the continuous reader for reading data from a USB pipe](how-to-use-the-continous-reader-for-getting-data-from-a-usb-endpoint--umdf-.md)">USB パイプからデータを読み取るための継続的なリーダーを使用する方法</a></p></td>
<td><p>このトピックでは、WDF の継続的なリーダー オブジェクトについて説明します。 このトピックの手順では、オブジェクトを構成し、USB パイプからデータの読み取りに使用する方法についての詳細な手順を説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="usb-bulk-and-interrupt-transfer.md" data-raw-source="[How to send USB bulk transfer requests](usb-bulk-and-interrupt-transfer.md)">USB 一括転送要求を送信する方法</a></p></td>
<td><p>このトピックでは、USB 一括転送について、簡単な概要を説明します。 クライアント ドライバーが送信して、デバイスから大量のデータを受信する方法についての詳細な手順についても提供します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-open-streams-in-a-usb-endpoint.md" data-raw-source="[How to open and close static streams in a USB bulk endpoint](how-to-open-streams-in-a-usb-endpoint.md)">USB 一括エンドポイントで静的なストリームを開閉する方法</a></p></td>
<td><p>このトピックでは、静的なストリームの機能について説明し、USB クライアント ドライバーが開くし、USB 3.0 デバイスの一括エンドポイントでのストリームを閉じる方法について説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="transfer-data-to-isochronous-endpoints.md" data-raw-source="[How to transfer data to USB isochronous endpoints](transfer-data-to-isochronous-endpoints.md)">USB アイソクロナス エンドポイントにデータを転送する方法</a></p></td>
<td><p>このトピックでは、クライアント ドライバーが、USB 要求ブロック (URB) USB デバイス アイソクロナス エンドポイントとの間のデータ転送を作成する方法について説明します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-send-chained-mdls.md" data-raw-source="[How to send chained MDLs](how-to-send-chained-mdls.md)">チェーンされた MDLs を送信する方法</a></p></td>
<td><p>このトピックでは、USB ドライバー スタック、およびクライアント ドライバーがのチェーンとして転送バッファーを送信する方法では、チェーンの MDLs 機能について学習<a href="https://msdn.microsoft.com/library/windows/hardware/ff554414" data-raw-source="[&lt;strong&gt;MDL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554414)"> <strong>MDL</strong> </a>構造体。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-recover-from-usb-pipe-errors.md" data-raw-source="[How to recover from USB pipe errors](how-to-recover-from-usb-pipe-errors.md)">USB パイプ エラーから回復する方法</a></p></td>
<td><p>このトピックでは、ときに、USB パイプへのデータ転送を試みることができますの手順については失敗します。 このトピックでカバーで説明されているメカニズムは、中止、リセットして、一括、割り込み、アイソクロナス パイプでポート operations のサイクルします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="usb-bandwidth-allocation.md" data-raw-source="[USB Bandwidth Allocation](usb-bandwidth-allocation.md)">USB の帯域幅の割り当て</a></p></td>
<td><p>このセクションでは、慎重に USB の帯域幅の管理に関するガイダンスを提供します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[USB ドライバー開発ガイド](usb-driver-development-guide.md)  



