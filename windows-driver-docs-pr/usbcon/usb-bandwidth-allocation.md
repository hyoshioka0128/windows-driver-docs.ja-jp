---
Description: このセクションでは、USB 帯域幅の慎重な管理に関するガイダンスを提供します。
title: USB 帯域幅割り当て
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ff231a0d5cb904b0e409d2aa3d2276a609071f0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844333"
---
# <a name="usb-bandwidth-allocation"></a>USB 帯域幅割り当て


このセクションでは、USB 帯域幅の慎重な管理に関するガイダンスを提供します。

使用される USB 帯域幅を最小限に抑えるために、すべての USB クライアントドライバーの役割を担い、未使用の帯域幅をできるだけ迅速に解放します。

ここでは、次のトピックについて説明します。

## <a name="why-is-my-usb-driver-getting-out-of-bandwidth-errors"></a>USB ドライバーの帯域幅のエラーが発生するのはなぜですか。


USB バスの帯域幅の競合は、ハードウェアとソフトウェアの両方のソースから取得されるため、USB クライアントドライバーで使用できる帯域幅の量を正確に予測することは困難です。 USB ホストコントローラーの操作には一定量の帯域幅が必要ですが、必要な量は、コントローラーの速度が高いかどうかによって異なります。システムによって異なります。 高速で動作する USB ハブでは、高速なアップストリームポートと低速デバイスの間でトランザクションを変換することが必要になることがあります。この変換プロセスでは、帯域幅が消費されます。 ただし、トランザクションの変換に帯域幅が必要になるかどうかは、接続されているデバイスの種類と、デバイスツリーのトポロジによって異なります。

帯域幅リソースの最も重大な負担は、通常、帯域幅を独占する USB クライアントドライバーからのものです。 システムによって、最初に提供された帯域幅が割り当てられます。 最初の USB ドライバーが、使用可能なすべての帯域幅を要求した場合、後で読み込まれる USB ドライバーは、デバイスの帯域幅をまったく取得しません。 この問題が発生すると、システムはデバイスを構成できず、デバイスの列挙に失敗します。 通常、列挙が失敗した理由は明らかではないため、ユーザーエクスペリエンスが悪い可能性があります。

場合によっては、クライアントドライバーが高速割り込み転送によって使用可能な帯域幅を消費することがあります。 しかし、最も一般的なのは、クライアントドライバーがアイソクロナス転送の帯域幅を過剰に割り当てているということです。その後、帯域幅を適時に解放できません。 システムは、要求されたドライバーがエンドポイントを閉じる (別のエンドポイントを開く) か、帯域幅が割り当てられたデバイスが削除されるまで、割り当てられた帯域幅を予約します。 システムは一括転送に対して保証された帯域幅を割り当てないため、一括転送は列挙エラーの原因にはなりません。 ただし、一括転送デバイスのパフォーマンスは、定期的 (アイソクロナスおよび割り込み) 転送を行うデバイスに割り当てられる帯域幅によって異なります。

USB 2.0 仕様では、既定のインターフェイス設定で、アイソクロナスデバイスの帯域幅がゼロに設定されている必要があります。 これにより、関数ドライバーが既定以外のインターフェイスを開くまで、デバイス用に帯域幅が予約されないようにすることができます。これにより、デバイスの構成中に、過剰な帯域幅の要求によって発生する列挙エラーを防ぐことができます。 ただし、デバイスを構成した後にクライアントドライバーが過剰な帯域幅を割り当てないようにして、他のデバイスが正常に機能しなくなるのを防ぐことはできません。

帯域幅を適切に管理するには、アイソクロナス転送を行うシステム内のすべての USB デバイスが、アイソクロナスエンドポイントを含むインターフェイスごとに複数の代替 (Alt) 設定を提供する必要があります。また、クライアントドライバーは、これらのAlt の設定。 クライアントドライバーは、最大の帯域幅でインターフェイスの設定を要求することから開始する必要があります。 要求が失敗した場合、クライアントドライバーは、要求が成功するまで、小さい帯域幅と小さい帯域幅でインターフェイス設定を要求する必要があります。

たとえば、web カメラのデバイスに次のようなインターフェイスがあるとします。

インターフェイス 0 (既定のインターフェイス設定: 既定の設定では、0以外のアイソクロナス帯域幅を持つエンドポイントは存在しません)

アイソクロナスエンドポイント 1: 最大パケットサイズ = 0 バイト

アイソクロナスエンドポイント 2: 最大パケットサイズ = 0 バイト

インターフェイス 0 Alt 設定1

アイソクロナスエンドポイント 1: 最大パケットサイズ = 256 バイト

アイソクロナスエンドポイント 2: 最大パケットサイズ = 256 バイト

インターフェイス 0 Alt 設定2

アイソクロナスエンドポイント 1: 最大パケットサイズ = 512 バイト

アイソクロナスエンドポイント 2: 最大パケットサイズ = 512 バイト

Web カメラのドライバーによって、既定のインターフェイス設定を初期化するときに使用するように web カメラが構成されます。 既定の設定では、アイソクロナス帯域幅がないため、初期化中に既定の設定を使用すると、アイソクロナス帯域幅の要求に失敗したために、web カメラが列挙に失敗する危険性が回避されます。

クライアントドライバーがアイソクロナス転送を実行する準備ができたら、alt 設定2を使用します。これは、Alt 設定2のパケットサイズが最大になるためです。 要求が失敗した場合、ドライバーは Alt 設定1を使用して2回目の試行を行うことができます。 Alt 設定1の方が必要な帯域幅が少なくなるため、最初の要求が失敗した場合でも、この要求は成功する可能性があります。 複数の Alt 設定を使用すると、ドライバーは何回も試行することができます。

Web カメラがアイドル状態になると、既定の設定を再度選択することで、割り当てられた帯域幅を空き帯域幅プールに戻すことができます。

Windows Vista 以降では、デバイスマネージャーでコントローラーのプロパティを確認することによって、USB コントローラーが割り当てた帯域幅の量を確認できます。 コントローラーのプロパティを選択し、[詳細設定] タブを確認します。この読み取りは、USB ハブがトランザクションの変換に割り当てた帯域幅の量を示すものではありません。

USB コントローラーの帯域幅の使用量を報告するデバイスマネージャー機能は、Windows XP では正しく機能しません。

 
## <a name="usb-transfer-and-packet-sizes"></a>USB 転送とパケットサイズ


このトピックでは、さまざまなバージョンの Windows オペレーティングシステムで許可される USB 転送サイズについて説明します。

-   [最大転送サイズ](#maximum-transfer-size)
-   [最大パケットサイズ](#maximum-packet-size)
-   [読み取り転送バッファーの最大パケットサイズ制限](#maximum-packet-size-restriction-on-read-transfer-buffers)
-   [短いパケットでの書き込み転送の区切り](#delimiting-write-transfers-with-short-packets)

### <a name="maximum-transfer-size"></a>最大転送サイズ


*最大転送サイズ*は、USB ドライバースタックのハードコーディングされた制限を指定します。 システムリソースの制限により、これらの制限を下回る転送サイズが失敗する可能性があります。 この種のエラーを回避し、すべてのバージョンの Windows で互換性を確保するには、USB 転送に大きな転送サイズを使用しないでください。

> **注:**  
>
> Windows XP、Windows Server 2003、およびそれ以降のバージョンでは、 [**USBD\_PIPE\_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_pipe_information)構造体の**MaximumTransferSize**メンバーは廃止されています。 USB ドライバースタックは、複合デバイスと非複合デバイスの両方の**MaximumTransferSize**の値を無視します。
>
> Windows 2000 では、USB ドライバースタックは**MaximumTransferSize**を\_USBD に初期化し、既定\_最大\_転送\_サイズに初期化します。 クライアントドライバーは、デバイスの構成中により小さい値を設定できます。 複合デバイスの場合、各関数のクライアントドライバーは、既定以外のインターフェイス設定のパイプの**MaximumTransferSize**のみを変更できます。

USB 転送のサイズには、次の制限があります。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>パイプの転送</th>
<th>Windows 8.1、Windows 8</th>
<th>Windows 7、Windows Vista</th>
<th>Windows XP、Windows Server 2003</th>
<th>Windows 2000</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>コントロール</td>
<td><p>SuperSpeed と高速 (xHCI) の場合は64K</p>
<p>フルおよび低速度の 4K (xHCI、EHCI、UHCI、OHCI)</p>
<p>UHCI の場合、既定のエンドポイントでは4K です。既定以外のコントロールパイプの64K</p></td>
<td><p>高速 (EHCI) の場合は64K</p>
<p>フルおよび低速度の 4K (EHCI、UHCI、OHCI)</p>
<p>UHCI の場合、既定のエンドポイントでは4K です。既定以外のコントロールパイプの 64K (UHCI)</p></td>
<td><p>高速 (EHCI) の場合は64K</p>
<p>フルおよび低速度の 4K (EHCI、UHCI、OHCI)</p>
<p>UHCI の場合、既定のエンドポイントでは4K です。既定以外のコントロールパイプの 64K (UHCI)</p></td>
<td><p>既定のエンドポイントでは4K既定以外のコントロールパイプ (OHCI) で64K</p></td>
</tr>
<tr class="even">
<td>妨害</td>
<td><p>4 MB、SuperSpeed、高、フル、低速度 (xHCI、EHCI、UHCI、OHCI)</p></td>
<td><p>4 MB (高、最大、低速度) (EHCI、UHCI、OHCI)</p></td>
<td>[無制限]</td>
<td><p>未確定 (OHCI)</p></td>
</tr>
<tr class="odd">
<td>一括</td>
<td><p>SuperSpeed の場合は 32MB (xHCI)</p>
<p>4MB と最高速度 (xHCI)</p>
<p>最大速度と最高速度 (EHCI と UHCI) の 4 MB</p>
<p>256K の全速度 (OHCI)</p></td>
<td><p>最大速度と最高速度 (EHCI、UHCI) の 4 MB</p>
<p>フルスピードの 256K (OHCI)</p></td>
<td><p>3 MB と最高速度 (EHCI) の場合</p>
<p>未確定 (UHCI)</p>
<p>フルスピードの 256K (OHCI)</p></td>
<td><p>未確定 (OHCI)</p></td>
</tr>
<tr class="even">
<td>アイソクロナス</td>
<td><p>1024<em><strong>Wbytesperinterval</strong> (SUPERSPEED を参照) (xHCI) については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_superspeed_endpoint_companion_descriptor" data-raw-source="[&lt;strong&gt;USB_SUPERSPEED_ENDPOINT_COMPANION_DESCRIPTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_superspeed_endpoint_companion_descriptor)"><strong>USB_SUPERSPEED_ENDPOINT_COMPANION_DESCRIPTOR</strong></a>」を参照してください。</p>
<p>1024</em> <strong>MaximumPacketSize</strong> (XHCI, EHCI)</p>
<p>256 * <strong>MaximumPacketSize</strong>の全速度 (XHCI、EHCI)</p>
<p>64K (全速度) (UHCI、OHCI)</p></td>
<td><p>1024 * 高速 (EHCI) の<strong>MaximumPacketSize</strong></p>
<p>256 * <strong>MaximumPacketSize</strong> (EHCI)</p>
<p>64K (全速度) (UHCI、OHCI)</p></td>
<td><p>1024 * 高速 (EHCI) の<strong>MaximumPacketSize</strong></p>
<p>256 * <strong>MaximumPacketSize</strong>の全速度 (EHCI)</p>
<p>64K (全速度) (UHCI、OHCI)</p></td>
<td><p>全速度で 64K (OHCI)</p></td>
</tr>
</tbody>
</table>

 

**MaximumTransferSize**を使用して転送サイズを制限しても、デバイスが消費する帯域幅の量に直接影響はありません。 クライアントドライバーは、インターフェイスの設定を変更するか、 [**USBD\_パイプ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_pipe_information)の**MaximumPacketSize**メンバーで設定された最大パケットサイズを制限する必要があります\_情報。

### <a name="maximum-packet-size"></a>最大パケットサイズ


*最大パケットサイズ*は、エンドポイント記述子の**wMaxPacketSize**フィールドによって定義されます。 クライアントドライバーは、デバイスに対する選択インターフェイス要求で USB パケットサイズを制御できます。 この値を変更しても、デバイスの**wMaxPacketSize**は変更されません。

要求の[**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)は、パイプの[**USBD\_パイプ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_pipe_information)構造体です。 この構造体では、

-   [**USBD\_パイプ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_pipe_information)構造体の**MaximumPacketSize**メンバーを変更します。 現在のインターフェイス設定のデバイスファームウェアで定義されている**wMaxPacketSize**の値以下の値に設定します。
-   USBD\_PF\_CHANGE\_MAX\_PACKET フラグを設定します。これには、 **PipeFlags**メンバー [**USBD\_パイプ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_pipe_information)構造体が含まれます。

インターフェイス設定の選択の詳細については、「 [USB デバイスの構成を選択する方法](how-to-select-a-configuration-for-a-usb-device.md)」を参照してください。

### <a name="maximum-packet-size-restriction-on-read-transfer-buffers"></a>読み取り転送バッファーの最大パケットサイズ制限


クライアントドライバーが読み取り要求を行う場合、転送バッファーは最大パケットサイズの倍数である必要があります。 ドライバーが最大パケットサイズよりも小さいデータを必要とする場合でも、パケット全体を要求する必要があります。 デバイスが最大サイズ (短いパケット) 未満のパケットを送信すると、転送が完了したことが示されます。

**注:**  

古いコントローラーでは、クライアントドライバーは動作をオーバーライドできます。 データ転送の[**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)の**transferflags**メンバーでは、クライアントドライバーは、USBD\_SHORT\_transfer\_OK フラグを設定する必要があります。 このフラグは、デバイスが**wMaxPacketSize**より小さいパケットを送信することを許可します。

XHCI ホストコントローラーでは、一括エンドポイントと割り込みエンドポイントでは、USBD\_SHORT\_TRANSFER\_OK は無視されます。 EHCI コントローラーでの短いパケットの転送では、エラー状態は発生しません。

EHCI ホストコントローラーでは、一括エンドポイントと割り込みエンドポイントでは、USBD\_SHORT\_TRANSFER\_OK は無視されます。

UHCI および OHCI ホストコントローラーで、\_転送\_OK が一括または割り込み転送用に設定されていない\_場合、短いパケット転送によってエンドポイントが停止し、転送に対してエラーコードが返されます。

### <a name="delimiting-write-transfers-with-short-packets"></a>短いパケットでの書き込み転送の区切り


USB ドライバースタックドライバーは、デバイスへの書き込み時に、デバイスからの読み取り時に適用されるパケットサイズに対して同じ制限を課すことはありません。 一部のクライアントドライバーでは、デバイスを管理するために少量の制御データを頻繁に送信する必要があります。 このような場合には、データ転送を一様なサイズのパケットに制限するのは現実的ではありません。 したがって、ドライバースタックは、データの書き込み時にエンドポイントの最大サイズよりも小さいサイズのパケットに特別な意味を割り当てません。 これにより、クライアントドライバーは、デバイスへの大きな転送を、最大サイズ以下のサイズの複数の URBs に分割できます。

ドライバーは、最大サイズより小さいパケットによって転送を終了するか、長さが0のパケットを使って転送の終了を区切る必要があります。 ドライバーが*wMaxPacketSize*より小さいパケットを送信するまで、転送は完了しません。 転送サイズが最大値の倍数である場合、ドライバーは、転送を明示的に終了するために、長さが0の区切りパケットを送信する必要があります。

USB 仕様で必要とされるように、長さゼロのパケットでデータ転送を区切ることは、クライアントドライバーの役割です。 USB ドライバースタックは、これらのパケットを自動的に生成しません。

 
## <a name="delimiting-usb-data-transfers-with-packets-smaller-than-wmaxpacketsize"></a>WMaxPacketSize より小さいパケットでの USB データ転送の区切り


準拠している USB 2.0/1.1 ドライバーは、最大サイズ (*wMaxPacketSize*) のパケットを送信する必要があります。その後、最大サイズより小さいパケットで転送を終了するか、長さが0のパケットを使って転送の終了を区切ります。 ドライバーが*wMaxPacketSize*より小さいパケットを送信するまで、転送は完了しません。 転送サイズが最大値の倍数である場合、ドライバーは、転送を明示的に終了するために、長さが0の区切りパケットを送信する必要があります。

USB 仕様で必要とされるように、長さゼロのパケットでデータ転送を区切ることは、デバイスドライバーの役割です。 システムの USB スタックは、これらのパケットを自動的に生成しません。


 




