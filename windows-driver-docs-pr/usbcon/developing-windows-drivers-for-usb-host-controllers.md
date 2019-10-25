---
Description: USB ホスト コントローラー用 Windows ドライバーの開発
title: USB ホスト コントローラー用 Windows ドライバー開発の概要
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f93df2d3edf2cfa439d68679f270bc2d00d874e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842390"
---
# <a name="overview-of-developing-windows-drivers-for-usb-host-controllers"></a>USB ホスト コントローラー用 Windows ドライバー開発の概要


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>目的</strong></p>
<p>このセクションでは、Microsoft 提供の USB ホストコントローラー拡張機能 (UCX) と通信するユニバーサルシリアルバス (USB) ホストコントローラードライバーを開発するための、Windows オペレーティングシステムでののサポートについて説明します。</p>
<p>仕様に準拠しない xHCI ホスト コントローラーを開発している場合、またはカスタムの非 xHCI ハードウェア (仮想ホスト コントローラーなど) を開発している場合、UCX と通信するホスト コントローラー ドライバーを記述できます。 たとえば、USB デバイスをサポートする無線ドックを検討してください。 PC は、トランスポートとして TCP 経由の USB を使用することで、無線ドック経由で USB デバイスと通信します。</p>
<p><strong>USB ホストコントローラー拡張機能 (UCX)</strong></p>
<p>USB ホストコントローラー拡張機能は、システムによって提供されるドライバー (Ucx01000) です。 このドライバーは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/" data-raw-source="[Windows Driver Framework](https://docs.microsoft.com/windows-hardware/drivers/wdf/)">Windows Driver framework</a>プログラミングインターフェイスを使用して、フレームワーククラス拡張として実装されます。 ホストコントローラードライバーは、そのクラス拡張に対するクライアントドライバーとして機能します。 ホストコントローラードライバーは、ハードウェアの操作とイベント、電源管理、および PnP イベントを処理しますが、UCX は、ホストコントローラードライバーへの要求をキューに入れ、他のタスクを実行する抽象化されたインターフェイスとして機能します。</p>
<p>UCX は、 <a href="usb-3-0-driver-stack-architecture.md" data-raw-source="[USB host-side drivers in Windows](usb-3-0-driver-stack-architecture.md)">Windows の USB ホスト側ドライバー</a>の1つです。 これは、ホストコントローラーのデバイススタックに FDO として読み込まれます。</p>
<p><strong>USB ホストコントローラードライバー</strong></p>
<p>UCX は拡張可能で、さまざまなホストコントローラードライバーをサポートするように設計されています。 Windows には、USB xHCI ホストコントローラーを対象とする xHCI ドライバー (Usbxhci) が用意されています。</p>
<p>ホストコントローラードライバーは UCX のクライアントであり、<a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-debugging" data-raw-source="[Kernel-Mode Driver Framework](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-debugging)">カーネルモードドライバーフレームワーク</a>(kmdf) ドライバーとして記述されています。</p>
<p><strong>Microsoft 提供のバイナリ</strong></p>
<p>ホストコントローラードライバーを作成するには、UCX (Ucx01000) とスタブライブラリ (Ucx01000) が必要です。 スタブライブラリは、Windows Driver Kit (WDK) に含まれています。 このライブラリは、2つの主な機能を実行します。</p>
<ul>
<li>ホストコントローラードライバーによって行われた呼び出しを変換し、UCX に渡します。</li>
<li>バージョン管理のサポートを提供します。 ホストコントローラードライバーは UCX で動作します。 UCX のメジャーバージョン番号がホストコントローラードライバーと同じであるか、ホストコントローラードライバーと同じかそれ以上のマイナーバージョン番号である場合に限られます。</li>
</ul>
<p><strong>開発ツール</strong></p>
<p>WDK には、ヘッダー、ライブラリ、ツール、サンプルなど、ドライバーの開発に必要なリソースが含まれています。</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=617155" data-raw-source="[Download kits and tools for Windows](https://go.microsoft.com/fwlink/p/?linkid=617155)">Windows 用のキットとツールのダウンロード</a></p></td>
<td><p><strong>作業の開始...</strong></p>
<p>アーキテクチャのさまざまなコンポーネント (デバイス、ホストコントローラー、およびハブ) の予想される動作について説明した公式仕様をお読みください。</p>
<a href="https://go.microsoft.com/fwlink/p/?linkid=618273" data-raw-source="[xHCI for Universal Serial Bus: Specification]( https://go.microsoft.com/fwlink/p/?linkid=618273)">xHCI For Universal Serial bus: Specification</a>
<a href="https://go.microsoft.com/fwlink/p/?linkid=224892" data-raw-source="[Official Universal Serial Bus Documents]( https://go.microsoft.com/fwlink/p/?linkid=224892)">オフィシャルユニバーサルシリアルバスドキュメント</a>
<p><strong>UCX のアーキテクチャについて</strong></p>
<p>Microsoft 提供の USB ドライバースタックについて理解を深めてください。</p>
<a href="usb-3-0-driver-stack-architecture.md" data-raw-source="[USB host-side drivers in Windows](usb-3-0-driver-stack-architecture.md)">Windows アーキテクチャにおける usb ホスト側ドライバー</a>
<a href="get-started-with-host-controller-driver-development.md" data-raw-source="[Architecture: USB host controller extension (UCX)](get-started-with-host-controller-driver-development.md)">: usb ホストコントローラー拡張機能 (ucx)</a>
<p><strong>UCX オブジェクトとハンドルについて理解する</strong></p>
<p>UCX は、WDF オブジェクト機能を拡張して、独自の USB 固有の UCX オブジェクトを定義します。 WDF オブジェクトの詳細については、「<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/introduction-to-framework-objects" data-raw-source="[Introduction to Framework Objects](https://docs.microsoft.com/windows-hardware/drivers/wdf/introduction-to-framework-objects)">フレームワークオブジェクトの概要</a>」を参照してください。</p>
<p>基になるホストコントローラードライバーへの要求をキューに置いている場合、UCX はこれらのオブジェクトを使用します。 詳細については、「 <a href="ucx-objects-and-handles-used-by-host-controller-driver.md" data-raw-source="[UCX objects and handles used by a host controller driver](ucx-objects-and-handles-used-by-host-controller-driver.md)">Ucx オブジェクトとホストコントローラードライバーによって使用されるハンドル</a>」を参照してください。</p>
<p></p>
<dl>
<dt>ホストコントローラーオブジェクト (UCXCONTROLLER)</dt>
<dd><p>ホストコントローラードライバーによって作成されたホストコントローラーを表します。 ドライバーは、ホストコントローラーインスタンスごとに1つのホストコントローラーオブジェクトのみを作成する必要があります。 通常、 <a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188033(v=vs.85)" data-raw-source="[&lt;strong&gt;UcxControllerCreate&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188033(v=vs.85))"><strong>UcxEVT_WDF_DRIVER_DEVICE_ADD create</strong></a>メソッドを呼び出すことによって、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add" data-raw-source="[**EVT_WDF_DRIVER_DEVICE_ADD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)"></a>コールバック内で作成されます。</p>
</dd>
<dt>ルートハブオブジェクト (UCXROOTHUB)</dt>
<dd><p>ホストコントローラーのルートポートの状態を取得および制御します。 通常、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add" data-raw-source="[**EVT_WDF_DRIVER_DEVICE_ADD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)"><strong>EVT_WDF_DRIVER_DEVICE_ADD</strong></a>コールバック内で、 <a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188048(v=vs.85)" data-raw-source="[&lt;strong&gt;UcxRootHubCreate&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188048(v=vs.85))"><strong>UcxRootHubCreate</strong></a>メソッドを呼び出すことによって作成されます。</p>
</dd>
<dt>USB デバイスオブジェクト (UCXUSBDEVICE)</dt>
<dd><p>バスに接続されている物理 USB デバイスを表します。 通常、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_usbdevice_add" data-raw-source="[&lt;em&gt;EVT_UCX_CONTROLLER_USBDEVICE_ADD&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_usbdevice_add)"><em>EVT_UCX_CONTROLLER_USBDEVICE_ADD</em></a>コールバック内で、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nf-ucxusbdevice-ucxusbdevicecreate" data-raw-source="[&lt;strong&gt;UcxUsbDeviceCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nf-ucxusbdevice-ucxusbdevicecreate)"><strong>UcxUsbDeviceCreate</strong></a>メソッドを呼び出すことによって作成されます。</p>
</dd>
<dt>エンドポイントオブジェクト (UCXENDPOINT)</dt>
<dd><p>USB デバイスオブジェクトのエンドポイントを表します。 通常、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_default_endpoint_add" data-raw-source="[&lt;em&gt;EVT_UCX_USBDEVICE_DEFAULT_ENDPOINT_ADD&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_default_endpoint_add)"><em>EVT_UCX_USBDEVICE_DEFAULT_ENDPOINT_ADD</em></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_endpoint_add" data-raw-source="[&lt;em&gt;EVT_UCX_USBDEVICE_ENDPOINT_ADD&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_endpoint_add)"><em>EVT_UCX_USBDEVICE_ENDPOINT_ADD</em></a>コールバック内で、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nf-ucxendpoint-ucxendpointcreate" data-raw-source="[&lt;strong&gt;UcxEndpointCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nf-ucxendpoint-ucxendpointcreate)"><strong>ucxendpointcreate</strong></a>メソッドを呼び出すことによって作成されます。</p>
</dd>
<dt>Stream オブジェクト (UCXSTREAMS)</dt>
<dd><p>1つの一括エンドポイントにわたるデバイスへのパイプの数を表します。 通常、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_static_streams_add" data-raw-source="[&lt;em&gt;EVT_UCX_ENDPOINT_STATIC_STREAMS_ADD&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_static_streams_add)"><em>EVT_UCX_ENDPOINT_STATIC_STREAMS_ADD</em></a>コールバック内で、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxsstreams/nf-ucxsstreams-ucxstaticstreamscreate" data-raw-source="[&lt;strong&gt;UcxStaticStreamsCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxsstreams/nf-ucxsstreams-ucxstaticstreamscreate)"><strong>UcxStaticStreamsCreate</strong></a>メソッドを呼び出すことによって作成されます。</p>
</dd>
</dl>
<p><strong>ドキュメントのセクション</strong></p>
<a href="manage-the-root-hub-in-a-host-controller-driver.md" data-raw-source="[Root hub callback functions of a host controller driver](manage-the-root-hub-in-a-host-controller-driver.md)">ホストコントローラードライバーのルートハブコールバック関数</a>
<p>UCX は、ルートハブに関連するほとんどの操作を処理します。 これにより、USB ハブドライバーは通常のハブと通信するのと同じ方法でルートハブと対話できます。 ホストコントローラードライバーは、コールバック関数を登録できます。</p>
<a href="handling-i-o-requests-in-a-host-controller-driver.md" data-raw-source="[Handle I/O requests in a USB host controller driver](handling-i-o-requests-in-a-host-controller-driver.md)">USB ホストコントローラードライバーで i/o 要求を処理する</a>
<p>インバウンド USB 要求ブロック (URBs) を UCX、正しいエンドポイントキューに転送します。</p>
<a href="configuring-usb-endpoints-in-a-host-controller-driver.md" data-raw-source="[Configure USB endpoints in a host controller driver](configuring-usb-endpoints-in-a-host-controller-driver.md)">ホストコントローラードライバーで USB エンドポイントを構成</a>する
<p>ホストコントローラードライバーは、そのエンドポイントに関連付けられているキューの UCX 管理と、コントローラーハードウェアへのエンドポイントのプログラミングの役割を果たします。</p>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#host-controller-driver-reference" data-raw-source="[USB host controller extension (UCX) reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#host-controller-driver-reference)">USB ホストコントローラー拡張機能 (UCX) のリファレンス</a>
<p>クライアントドライバーによって使用される i/o 要求、サポートルーチン、構造体、およびインターフェイスの仕様を提供します。 これらのルーチンと関連するデータ構造は、WDK ヘッダーで定義されています。</p>
<p>UCX は、<em>フレームワーククラス拡張</em>と呼ばれます。</p>
<p>ホストコントローラーのドライバーは、<em>クライアントドライバー</em>と呼ばれます。</p></td>

</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[ユニバーサル シリアル バス (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  



