---
Description: このセクションでは、慎重に USB の帯域幅の管理に関するガイダンスを提供します。
title: USB 帯域幅割り当て
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e431ce8e26de70c6f7f338c9a7ad93d0c7cf5ad
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369532"
---
# <a name="usb-bandwidth-allocation"></a>USB 帯域幅割り当て


このセクションでは、慎重に USB の帯域幅の管理に関するガイダンスを提供します。

すべての USB クライアント ドライバーを使用して、USB の帯域幅を最小限に抑え、未使用の帯域幅をできるだけ早く空き帯域幅プールに戻すの役目です。

ここでは、次のトピックについて説明します。

## <a name="why-is-my-usb-driver-getting-out-of-bandwidth-errors"></a>不足エラーの帯域幅には、USB ドライバーが取得するはなぜでしょうか。


USB バスで帯域幅の競合は、帯域幅の量が、USB クライアント ドライバーできるようになります正確に予測することは困難であるために、ハードウェアとソフトウェアの両方の複数のソースから取得されます。 USB ホスト コント ローラーでは、その操作では、一定量の帯域幅が必要ですが、必要な量のシステム値が異なるため、コント ローラーが高速かどうか、異なります。 高速で動作する USB ハブは高速のアップ ストリームのポートと低速デバイス、下流の間のトランザクションを変換する必要がある場合がありますし、この翻訳プロセスは、帯域幅を消費します。 接続されているデバイスの種類と、デバイス ツリーのトポロジによっては帯域幅がトランザクションの変換に必要かどうか。

帯域幅リソースの最も重大な負担は、通常は、帯域幅を独占する USB クライアント ドライバーから取得されます。 システムでは、1 つ目は、先着ごとに帯域幅を割り当てます。 最初に読み込まれた USB ドライバーは、すべての利用可能な帯域幅を要求している場合は後で読み込まれる USB ドライバーはそのデバイスのすべてのすべての帯域幅を取得できません。 これが発生したし、システム デバイスを構成することはできません、列挙するために失敗します。 通常はないため明らかな列挙が失敗した理由、これは不適切なユーザー エクスペリエンスにつながります。

場合によっては、クライアント ドライバーでは、割り込みを高速転送で使用できる帯域幅は使い果たしてしまいます。 クライアントのドライバーを isochronous 転送では、多くの帯域幅を割り当てるしが失敗する適切なタイミングで帯域幅を解放するに間違いは最も一般的です。 システムは、それを要求したドライバーでは、そのエンドポイントを閉じる (を別のエンドポイントを開いて)、または帯域幅が割り当てられているデバイスが削除されるまでに割り当てられた帯域幅を予約します。 一括転送は、列挙体のエラーの原因であることはありませんので、システムは、一括転送に保証された帯域幅を割り当てられません。 ただし、一括転送デバイスのパフォーマンスは、定期的に実行するデバイスに割り当てられる帯域幅の量に依存 (アイソクロナスと割り込み) 転送します。

USB 2.0 仕様では、その既定のインターフェイスの設定に 0-帯域幅のエンドポイントに isochronous デバイスが必要です。 これにより、帯域幅は予約されていません、デバイスの機能ドライバーが、既定ではないインターフェイスをさらに、デバイスの構成中に、帯域幅の過剰な要求によって発生した列挙体のエラーを防止するを開くを待ちます。 ただし、これもクライアント ドライバーから正常に機能してから、その他のデバイスを防ぐ、そのデバイスを構成した後の帯域幅の割り当ています。

適切な帯域幅を管理するキーは isochronous 転送システム内のすべての USB デバイスが、アイソクロナス エンドポイントを格納している各インターフェイスに対して複数の代替 (Alt) 設定を提供する必要があります。、クライアント ドライバーは、これらを賢く利用を行う必要があります。Alt 設定します。 クライアント ドライバーは、最大帯域幅のインターフェイス設定を要求することで開始する必要があります。 要求が失敗した場合、クライアント ドライバーは、要求が成功するまで小さなの帯域幅とインターフェイスの設定を要求する必要があります。

たとえば、web カメラ デバイスに、次のインターフェイスがあるとします。

インターフェイス 0 (既定のインターフェイスの設定。既定の設定でアイソクロナス帯域幅が 0 以外のエンドポイントがありません)

アイソクロナス エンドポイント 1: 最大パケット サイズ 0 バイトを =

アイソクロナス エンドポイント 2: 最大パケット サイズ 0 バイトを =

Setting 1 0 インターフェイスの Alt

アイソクロナス エンドポイント 1: 最大パケット サイズ = 256 バイト

アイソクロナス エンドポイント 2: 最大パケット サイズ = 256 バイト

0 インターフェイスの alt キーを 2 に設定

アイソクロナス エンドポイント 1: 最大パケット サイズ 512 バイトを =

アイソクロナス エンドポイント 2: 最大パケット サイズ 512 バイトを =

Web カメラのドライバーの初期化時に既定のインターフェイス設定を使用する web カメラを構成します。 既定の設定がアイソクロナス帯域幅、アイソクロナス帯域幅の失敗した要求のため、列挙するために、web カメラの障害が発生する危険性の初期化中に既定の設定を使用して回避できます。

クライアント ドライバーのアイソクロナスの転送を行う準備が最大パケット サイズが 2 の設定に alt キーを押し、alt キーを押し、2 の設定を使用するようにします。 要求が失敗すると、ドライバーは、alt キーを 1 に設定を使用して、2 回目の試行をことができます。 Alt キーを 1 に設定より少ない帯域幅を必要とするためこの要求が成功したと場合でも、最初の要求が失敗しました。 複数の Alt 設定では、ドライバーを断念する前に、いくつかの試行を許可します。

Web カメラがアイドル状態になった後、既定の設定をもう一度選択して割り当てられた帯域幅、帯域幅の空きプールに返すできます。

Windows Vista 以降、ユーザーはデバイス マネージャーで、コント ローラーのプロパティをチェックして USB コント ローラーが割り当てられている帯域幅の量を確認できます。 コント ローラーのプロパティ を選択し、詳細設定 タブを確認します。この読み取りは、トランザクションの翻訳の帯域幅の USB ハブが割り当てられている量を示していません。

Windows XP では、USB コント ローラーの帯域幅の使用状況を報告するデバイス マネージャーの機能が正しく動作しないしません。

 
## <a name="usb-transfer-and-packet-sizes"></a>USB 転送およびパケットのサイズ


このトピックでは、さまざまなバージョンの Windows オペレーティング システムで許可されている USB 転送サイズについて説明します。

-   [最大転送サイズ](#maximum-transfer-size)
-   [最大パケット サイズ](#maximum-packet-size)
-   [読み取り転送バッファーの最大パケット サイズの制限](#maximum-packet-size-restriction-on-read-transfer-buffers)
-   [書き込みを区切る短いパケットを転送します。](#delimiting-write-transfers-with-short-packets)

### <a name="maximum-transfer-size"></a>最大転送サイズ


*最大転送サイズ*USB ドライバー スタックでハード コーディングされた制限を指定します。 転送のサイズ以下のシステム リソースの制限によりこれらの制限が失敗する可能性があります。 これらの種類の障害を回避し、Windows のすべてのバージョン間で互換性を確保するには、USB 転送の大規模な転送サイズの使用を回避します。

> **注:**  
>
> Windows XP、Windows Server 2003、および以降のバージョンで**MaximumTransferSize**のメンバー、 [ **USBD\_パイプ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_usbd_pipe_information)構造体は廃止されています。 USB ドライバー スタックの値を無視します**MaximumTransferSize**複合および非複合デバイスです。
>
> Windows 2000 での USB ドライバー スタックの初期化**MaximumTransferSize** USBD に\_既定\_最大\_転送\_サイズ。 クライアント ドライバーでは、デバイスを構成するときより小さい値を設定できます。 複合デバイスは、関数ごとに、クライアント ドライバーを変更することができますのみ**MaximumTransferSize**パイプの既定以外のインターフェイスを設定します。

USB 転送サイズは、次の制限が適用されます。

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
<th>パイプを転送します。</th>
<th>Windows 8.1、Windows 8</th>
<th>Windows 7、Windows Vista</th>
<th>Windows XP、Windows Server 2003</th>
<th>Windows 2000</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>コントロール</td>
<td><p>SuperSpeed、高速 (xHCI) の 64 K</p>
<p>完全な低速度 (xHCI、EHCI、UHCI、OHCI) の 4 K</p>
<p>UHCI、既定のエンドポイントでは 4 K のコントロールの既定以外のパイプに 64 K</p></td>
<td><p>高速 (EHCI) の 64 K</p>
<p>完全な低速度 (EHCI、UHCI、OHCI) の 4 K</p>
<p>UHCI、既定のエンドポイントでは 4 K の既定ではないコントロール パイプ (UHCI) に 64 K</p></td>
<td><p>高速 (EHCI) の 64 K</p>
<p>完全な低速度 (EHCI、UHCI、OHCI) の 4 K</p>
<p>UHCI、既定のエンドポイントでは 4 K の既定ではないコントロール パイプ (UHCI) に 64 K</p></td>
<td><p>既定のエンドポイントでは 4 K既定ではないコントロール パイプ (OHCI) に 64 K</p></td>
</tr>
<tr class="even">
<td>割り込み</td>
<td><p>SuperSpeed、高、完全、および低速度 (xHCI、EHCI、UHCI、OHCI) の 4 MB</p></td>
<td><p>高、完全、および低速度 (EHCI、UHCI、OHCI) の 4 MB</p></td>
<td>無制限</td>
<td><p>Undetermined(OHCI)</p></td>
</tr>
<tr class="odd">
<td>一括</td>
<td><p>SuperSpeed (xHCI) は 32 MB</p>
<p>高速とフル_スピード (xHCI) の 4 MB</p>
<p>高速とフル_スピード (EHCI と UHCI) の 4 MB</p>
<p>256 K フル_スピード (OHCI)</p></td>
<td><p>高速とフル_スピード (EHCI、UHCI) の 4 MB</p>
<p>最大速度 (OHCI) は 256 K</p></td>
<td><p>高速とフル_スピード (EHCI) では 3 MB</p>
<p>不定 (UHCI)</p>
<p>最大速度 (OHCI) は 256 K</p></td>
<td><p>Undetermined(OHCI)</p></td>
</tr>
<tr class="even">
<td>アイソクロナス</td>
<td><p>1024<em><strong>wBytesPerInterval</strong> (を参照してください<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbspec/ns-usbspec-_usb_superspeed_endpoint_companion_descriptor" data-raw-source="[&lt;strong&gt;USB_SUPERSPEED_ENDPOINT_COMPANION_DESCRIPTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbspec/ns-usbspec-_usb_superspeed_endpoint_companion_descriptor)"> <strong>USB_SUPERSPEED_ENDPOINT_COMPANION_DESCRIPTOR</strong></a>) の SuperSpeed (xHCI)</p>
<p>1024</em> <strong>MaximumPacketSize</strong>の高速 (xHCI、EHCI)</p>
<p>256 * <strong>MaximumPacketSize</strong>フル_スピード (xHCI、EHCI) の</p>
<p>最大速度 (UHCI、OHCI) の 64 K</p></td>
<td><p>1024 * <strong>MaximumPacketSize</strong>の高速 (EHCI)</p>
<p>256 * <strong>MaximumPacketSize</strong>完全速度 (EHCI)</p>
<p>最大速度 (UHCI、OHCI) の 64 K</p></td>
<td><p>1024 * <strong>MaximumPacketSize</strong>の高速 (EHCI)</p>
<p>256 * <strong>MaximumPacketSize</strong>フル_スピード (EHCI) の</p>
<p>最大速度 (UHCI、OHCI) の 64 K</p></td>
<td><p>最大速度 (OHCI) の 64 K</p></td>
</tr>
</tbody>
</table>

 

転送サイズを制限する**MaximumTransferSize**デバイス、帯域幅の消費を直接影響しません。 クライアント ドライバーのインターフェイス設定を変更するかで設定した最大パケット サイズを制限する必要があります、 **MaximumPacketSize**のメンバー [ **USBD\_パイプ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_usbd_pipe_information).

### <a name="maximum-packet-size"></a>最大パケット サイズ


*最大パケット サイズ*によって定義されます、 **wMaxPacketSize**のエンドポイント記述子フィールド。 クライアント ドライバーでは、インターフェイスの要求をデバイスで USB のパケット サイズを制御できます。 この値を変更することは変わりません、 **wMaxPacketSize**デバイスにします。

[ **URB** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb)要求は、 [ **USBD\_パイプ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_usbd_pipe_information)パイプの構造体。 で、その構造

-   変更、 **MaximumPacketSize**のメンバー、 [ **USBD\_パイプ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_usbd_pipe_information)構造体。 値に設定する値の小さい**wMaxPacketSize**デバイス ファームウェアの現在のインターフェイスの設定で定義されています。
-   設定、USBD\_PF\_変更\_最大\_パケット フラグ、 **PipeFlags**メンバー [ **USBD\_パイプ\_情報** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_usbd_pipe_information)構造体。

インターフェイスの設定を選択する方法の詳細については、次を参照してください。 [USB デバイスの構成の選択方法](how-to-select-a-configuration-for-a-usb-device.md)します。

### <a name="maximum-packet-size-restriction-on-read-transfer-buffers"></a>読み取り転送バッファーの最大パケット サイズの制限


クライアント ドライバーが読み取り要求を行うと、転送バッファーはパケットの最大サイズの倍数である必要があります。 でもときにドライバーが必要ですが、パケットの最大サイズより小さいデータ、パケット全体をまだ要求にする必要があります。 デバイスは、最大サイズ (短いパケット) よりも小さいパケットを送信するときは、転送が完了したことを示します。

**注:**  

以前のコント ローラーで、クライアント ドライバーは、動作をオーバーライドできます。 **TransferFlags**メンバー データ転送の[ **URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb)、クライアント ドライバーは、USBD を設定する必要があります\_短い\_転送\_[Ok] のフラグ。 フラグによりより小さいパケットを送信するデバイス**wMaxPacketSize**します。

XHCI ホスト コント ローラー、USBD\_短い\_転送\_OK 一括および割り込みのエンドポイントは無視されます。 EHCI コント ローラーでは、短いパケットの転送は、エラー状態では発生しません。

EHCI ホスト コント ローラー、USBD\_短い\_転送\_一括および割り込みのエンドポイントは [ok] は無視されます。

UHCI と OHCI コント ローラーがホストに場合 USBD\_短い\_転送\_一括 [ok] が設定されていないまたは割り込み転送では、短いパケットの転送は、エンドポイントを停止し、転送エラー コードが返されます。

### <a name="delimiting-write-transfers-with-short-packets"></a>書き込みを区切る短いパケットを転送します。


USB ドライバー スタックのドライバーがデバイスから読み取るときに、デバイスに書き込むときに、同じパケットのサイズ制限を強制しません。 一部のクライアント ドライバーでは、自分のデバイスを管理するコントロールのデータの量が少ないの頻繁な転送を行う必要があります。 このような場合の均一のサイズのパケット データ転送を制限するのには実用的ではありません。 そのため、ドライバー スタックは何も特別な意味に割り当てませんエンドポイントの最大サイズよりも小さいサイズのパケット データの書き込み中にします。 これにより、任意のサイズの小さいよりまたは等しい最大値に複数の翻訳をデバイスに大規模な転送を中断するクライアント ドライバーができます。

ドライバーは、する必要がありますか、未満の最大サイズのパケットを使用して送信を終了または長さ 0 のパケットを使用して、送信の終了を区切ります。 ドライバーがより小さいパケットを送信するまで、送信は完了しない*wMaxPacketSize*します。 転送のサイズが最大値の倍数である場合は、ドライバーが、転送を明示的に終了する長さ 0 の区切りパケットを送信する必要があります。

長さ 0 のパケット データ転送を区切るには、USB 仕様で必要とはクライアント ドライバーの責任です。 USB ドライバー スタックでは、これらのパケットを自動的に生成しません。

 
## <a name="delimiting-usb-data-transfers-with-packets-smaller-than-wmaxpacketsize"></a>USB データ転送とパケットより小さい wMaxPacketSize を区切る


USB 2.0/1.1 準拠のドライバーが最大サイズのパケットを送信する必要があります (*wMaxPacketSize*) し未満の最大サイズのパケットを使用して送信を終了するか、長さ 0 を使用して、送信の終了を区切るパケットです。 ドライバーがより小さいパケットを送信するまで、送信は完了しない*wMaxPacketSize*します。 転送のサイズが最大値の倍数である場合は、ドライバーが、転送を明示的に終了する長さ 0 の区切りパケットを送信する必要があります。

長さ 0 のパケット データ転送を区切るには、USB 仕様で必要とは、デバイス ドライバーの責任です。 これらのパケットは、システムの USB スタックによって自動的には生成されません。


 




