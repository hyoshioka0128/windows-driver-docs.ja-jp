---
Description: このセクションのトピックでは、USB パイプ、i/o 要求の URBs、およびクライアントドライバーがデバイスドライバーインターフェイス (DDIs) を使用して USB デバイスとの間でデータを転送する方法について説明します。
title: USB クライアント ドライバーでの USB データ転送送信の概要
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: e9795e2af0697f98990f116c2079c30bdd6504be
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844825"
---
# <a name="overview-of-sending-usb-data-transfers-in-usb-client-drivers"></a>USB クライアント ドライバーでの USB データ転送送信の概要


このセクションのトピックでは、USB パイプと i/o 要求の URBs に関する情報を提供し、クライアントドライバーがデバイスドライバーインターフェイス (DDIs) を使用して USB デバイスとの間でデータを転送する方法について説明します。




転送は、ホストコントローラーと USB デバイス間でデータが移動されるたびに行われます。 一般に、USB 転送は制御転送とデータ転送に幅広く分類できます。 すべての USB デバイスは制御転送をサポートする必要があり、データ転送のエンドポイントをサポートできます。 各種類の転送は、 *USB エンドポイント*の種類 (デバイスのバッファー) に関連付けられています。 制御転送は既定のエンドポイントに関連付けられ、データ転送は一方向のエンドポイントを使用します。 データ転送の種類では、割り込み、一括、およびアイソクロナスエンドポイントが使用されます。 USB ドライバースタックは、デバイスでサポートされている各エンドポイントの*パイプ*と呼ばれる通信チャネルを作成します。 パイプの一方の端はデバイスのエンドポイントです。 パイプのもう一方の端は、常にホストコントローラーです。

クライアントドライバーは、デバイスに i/o 要求を送信する前に、構成、インターフェイス、エンドポイント、ベンダー、およびクラス固有の記述子に関する情報を USB デバイスから取得する必要があります。 さらに、ドライバーでもデバイスを構成する必要があります。 デバイス構成には、構成の選択や、各インターフェイス内での代替設定などのタスクが含まれます。 それぞれの代替設定で、データ転送に使用できる1つ以上の USB エンドポイントを指定できます。

デバイス構成の詳細については、「 [Usb デバイスの構成を選択する方法](how-to-select-a-configuration-for-a-usb-device.md)」および「 [usb インターフェイスで別の設定を選択する方法](select-a-usb-alternate-setting.md)」を参照してください。

クライアントドライバーによってデバイスが構成されると、ドライバーは、現在選択されている別の設定の各エンドポイントについて、USB ドライバースタックによって作成されたパイプハンドルにアクセスできるようになります。 エンドポイントにデータを転送するために、クライアントドライバーは、要求の種類に固有の URB をフォーマットすることによって要求を作成します。

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
<td><p>このトピックでは、制御転送の構造と、クライアントドライバーがデバイスにコントロール要求を送信する方法について説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-get-usb-pipe-handles.md" data-raw-source="[How to enumerate USB pipes](how-to-get-usb-pipe-handles.md)">USB パイプを列挙する方法</a></p></td>
<td><p>このトピックでは、usb パイプの概要について説明し、usb ドライバースタックからパイプハンドルを取得するために USB クライアントドライバーが必要とする手順について説明します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-use-the-continous-reader-for-getting-data-from-a-usb-endpoint--umdf-.md" data-raw-source="[How to use the continuous reader for reading data from a USB pipe](how-to-use-the-continous-reader-for-getting-data-from-a-usb-endpoint--umdf-.md)">連続リーダーを使用して USB パイプからデータを読み取る方法</a></p></td>
<td><p>このトピックでは、WDF に用意されている連続リーダーオブジェクトについて説明します。 このトピックの手順では、オブジェクトを構成し、それを使用して USB パイプからデータを読み取る方法について、手順を追って説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="usb-bulk-and-interrupt-transfer.md" data-raw-source="[How to send USB bulk transfer requests](usb-bulk-and-interrupt-transfer.md)">USB 一括転送要求を送信する方法</a></p></td>
<td><p>このトピックでは、USB 一括転送の概要について説明します。 また、クライアントドライバーがデバイスから一括データを送受信する方法について、手順を追って説明します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-open-streams-in-a-usb-endpoint.md" data-raw-source="[How to open and close static streams in a USB bulk endpoint](how-to-open-streams-in-a-usb-endpoint.md)">USB 一括エンドポイントで静的ストリームを開いて閉じる方法</a></p></td>
<td><p>このトピックでは、静的ストリームの機能について説明します。また、usb クライアントドライバーが USB 3.0 デバイスの一括エンドポイントでストリームを開いたり閉じたりする方法について説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="transfer-data-to-isochronous-endpoints.md" data-raw-source="[How to transfer data to USB isochronous endpoints](transfer-data-to-isochronous-endpoints.md)">USB アイソクロナスエンドポイントにデータを転送する方法</a></p></td>
<td><p>このトピックでは、USB デバイスでアイソクロナスエンドポイントとの間でデータを転送するために、クライアントドライバーで USB 要求ブロック (URB) を作成する方法について説明します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-send-chained-mdls.md" data-raw-source="[How to send chained MDLs](how-to-send-chained-mdls.md)">チェーン MDLs を送信する方法</a></p></td>
<td><p>このトピックでは、USB ドライバースタックのチェーン MDLs 機能について、およびクライアントドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_mdl" data-raw-source="[&lt;strong&gt;MDL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_mdl)"><strong>MDL</strong></a>構造体のチェーンとして転送バッファーを送信する方法について説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-recover-from-usb-pipe-errors.md" data-raw-source="[How to recover from USB pipe errors](how-to-recover-from-usb-pipe-errors.md)">USB パイプエラーから回復する方法</a></p></td>
<td><p>このトピックでは、USB パイプへのデータ転送が失敗した場合に試すことができる手順について説明します。 このトピックで説明するメカニズムでは、一括、割り込み、およびアイソクロナスパイプでのポート操作の中止、リセット、およびサイクルについて説明します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="usb-bandwidth-allocation.md" data-raw-source="[USB Bandwidth Allocation](usb-bandwidth-allocation.md)">USB 帯域幅の割り当て</a></p></td>
<td><p>このセクションでは、USB 帯域幅の慎重な管理に関するガイダンスを提供します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[USB ドライバー開発ガイド](usb-driver-development-guide.md)  



