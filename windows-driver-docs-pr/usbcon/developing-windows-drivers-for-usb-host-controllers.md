---
Description: USB ホスト コントローラー用 Windows ドライバーの開発
title: USB ホスト コントローラー用 Windows ドライバーの開発
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5cee2cfac0dd75e730bf43ce1307ea73279dcaf3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377404"
---
# <a name="developing-windows-drivers-for-usb-host-controllers"></a>USB ホスト コントローラー用 Windows ドライバーの開発


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>目的</strong></p>
<p>このセクションでは、Windows オペレーティング システムの Microsoft 提供の USB ホスト コント ローラー拡張機能 (UCX) と通信するユニバーサル シリアル バス (USB) ホスト コント ローラーのドライバーを開発するためのサポートについて説明します。</p>
<p>仕様に準拠しない xHCI ホスト コントローラーを開発している場合、またはカスタムの非 xHCI ハードウェア (仮想ホスト コントローラーなど) を開発している場合、UCX と通信するホスト コントローラー ドライバーを記述できます。 たとえば、USB デバイスをサポートする無線ドックを検討してください。 PC は、トランスポートとして TCP 経由の USB を使用することで、無線ドック経由で USB デバイスと通信します。</p>
<p><strong>USB ホスト コント ローラーの拡張機能 (UCX)</strong></p>
<p>USB ホスト コント ローラー拡張機能は、システム指定のドライバー (Ucx01000.sys) です。 このドライバーを使用して、framework クラスの拡張機能として実装されている、 <a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/" data-raw-source="[Windows Driver Framework](https://docs.microsoft.com/windows-hardware/drivers/wdf/)">Windows Driver Framework</a>プログラミング インターフェイスです。 ホスト コント ローラーのドライバーは、そのクラスの拡張機能へのクライアント ドライバーとして機能します。 ホスト コント ローラーのドライバーでは、ハードウェアの操作とイベント、電源管理、および PnP イベントを処理するときに、UCX は、ホスト コント ローラー ドライバーへの要求をキューに配置し他のタスクを実行する抽象化されたインターフェイスとして機能します。</p>
<p>1 つ UCX です、 <a href="usb-3-0-driver-stack-architecture.md" data-raw-source="[USB host-side drivers in Windows](usb-3-0-driver-stack-architecture.md)">Windows での USB ホスト側ドライバー</a>します。 ホスト コント ローラー デバイス スタックの FDO として読み込まれます。</p>
<p><strong>USB ホスト コント ローラーのドライバー</strong></p>
<p>UCX は、拡張可能なは、さまざまなホスト コント ローラーのドライバーをサポートするために設計されています。 Windows では、(Usbxhci.sys) そのターゲット USB xHCI ホスト コント ローラー、xHCI ドライバーを提供します。</p>
<p>ホスト コント ローラーのドライバーとして書き込まれます UCX のクライアントは、<a href="https://msdn.microsoft.com/library/windows/hardware/ff551869" data-raw-source="[Kernel-Mode Driver Framework](https://msdn.microsoft.com/library/windows/hardware/ff551869)">カーネル モード ドライバー フレームワーク</a>(KMDF) ドライバー。</p>
<p><strong>Microsoft から提供されたバイナリ</strong></p>
<p>ホスト コント ローラー用ドライバーを作成するには、UCX (Ucx01000.sys) とスタブ ライブラリ (Ucx01000.lib) が必要です。 スタブ ライブラリは、Windows Driver Kit (WDK) にします。 ライブラリは、2 つの主な機能を実行します。</p>
<ul>
<li>ホスト コント ローラーのドライバーによって行われた呼び出しを変換し、UCX まで渡したりします。</li>
<li>バージョン管理のサポートを提供します。 ホスト コント ローラーのドライバーは、UCX、UCX が、ホスト コント ローラー ドライバーとして同じメジャー バージョン番号と同じかそれ以上のマイナー場合にのみ、ホスト コント ローラーのドライバーとバージョン番号。</li>
</ul>
<p><strong>開発ツール</strong></p>
<p>WDK には、ヘッダー、ライブラリ、ツール、およびサンプルなど、ドライバーの開発に必要なリソースが含まれています。</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=617155" data-raw-source="[Download kits and tools for Windows](https://go.microsoft.com/fwlink/p/?linkid=617155)">Windows 用のキットとツールのダウンロード</a></p></td>
<td><p><strong>開始してください.</strong></p>
<p>アーキテクチャのさまざまなコンポーネント (デバイス、ホスト コント ローラーとハブ) の予期される動作を説明する正式な仕様を参照してください。</p>
<a href="https://go.microsoft.com/fwlink/p/?linkid=618273" data-raw-source="[xHCI for Universal Serial Bus: Specification]( https://go.microsoft.com/fwlink/p/?linkid=618273)">ユニバーサル シリアル バスの xHCI:仕様</a>
<a href="https://go.microsoft.com/fwlink/p/?linkid=224892" data-raw-source="[Official Universal Serial Bus Documents]( https://go.microsoft.com/fwlink/p/?linkid=224892)">ユニバーサル シリアル バスを公式のドキュメント</a>
<p><strong>UCX のアーキテクチャを理解します。</strong></p>
<p>Microsoft 提供の USB ドライバー スタックを理解します。</p>
<a href="usb-3-0-driver-stack-architecture.md" data-raw-source="[USB host-side drivers in Windows](usb-3-0-driver-stack-architecture.md)">Windows での USB ホスト側ドライバー</a>
<a href="get-started-with-host-controller-driver-development.md" data-raw-source="[Architecture: USB host controller extension (UCX)](get-started-with-host-controller-driver-development.md)">アーキテクチャ。USB ホスト コント ローラーの拡張機能 (UCX)</a>
<p><strong>UCX オブジェクトおよびハンドルと理解します。</strong></p>
<p>UCX では、独自の特定の USB UCX オブジェクトを定義する WDF オブジェクトの機能を拡張します。 WDF のオブジェクトの詳細については、次を参照してください。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff544249" data-raw-source="[Introduction to Framework Objects](https://msdn.microsoft.com/library/windows/hardware/ff544249)">Framework オブジェクトの概要</a>します。</p>
<p>基になるホスト コント ローラー ドライバーにキュー要求の場合は、UCX は、これらのオブジェクトを使用します。 詳細については、次を参照してください。 <a href="ucx-objects-and-handles-used-by-host-controller-driver.md" data-raw-source="[UCX objects and handles used by a host controller driver](ucx-objects-and-handles-used-by-host-controller-driver.md)">UCX オブジェクトと、処理ホスト コント ローラーのドライバーによって使用される</a>します。</p>
<p></p>
<dl>
<dt>ホスト コント ローラーのオブジェクト (UCXCONTROLLER)</dt>
<dd><p>ホスト コント ローラーのドライバーによって作成されるホスト コント ローラーを表します。 ドライバーは、ホスト コント ローラーのインスタンスごとに 1 つだけのホスト コント ローラー オブジェクトを作成する必要があります。 内で作成された通常、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff541693" data-raw-source="[**EVT_WDF_DRIVER_DEVICE_ADD**](https://msdn.microsoft.com/library/windows/hardware/ff541693)"> <strong>EVT_WDF_DRIVER_DEVICE_ADD</strong></a>コールバックを呼び出すことによって、 <a href="https://msdn.microsoft.com/library/windows/hardware/mt188033" data-raw-source="[&lt;strong&gt;UcxControllerCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt188033)"> <strong>UcxControllerCreate</strong> </a>メソッド。</p>
</dd>
<dt>ルート ハブ オブジェクト (UCXROOTHUB)</dt>
<dd><p>取得し、ホスト コント ローラーのルートのポートの状態を制御します。 通常内のホスト コント ローラーのドライバーによって作成された、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff541693" data-raw-source="[**EVT_WDF_DRIVER_DEVICE_ADD**](https://msdn.microsoft.com/library/windows/hardware/ff541693)"> <strong>EVT_WDF_DRIVER_DEVICE_ADD</strong> </a>コールバックを呼び出すことによって、 <a href="https://msdn.microsoft.com/library/windows/hardware/mt188048" data-raw-source="[&lt;strong&gt;UcxRootHubCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt188048)"> <strong>UcxRootHubCreate</strong> </a>メソッド。</p>
</dd>
<dt>USB デバイス オブジェクト (UCXUSBDEVICE)</dt>
<dd><p>バスに接続されている物理的な USB デバイスを表します。 通常内のホスト コント ローラーのドライバーによって作成された、 <a href="https://msdn.microsoft.com/library/windows/hardware/mt187823" data-raw-source="[&lt;em&gt;EVT_UCX_CONTROLLER_USBDEVICE_ADD&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/mt187823)"> <em>EVT_UCX_CONTROLLER_USBDEVICE_ADD</em> </a>コールバックを呼び出すことによって、 <a href="https://msdn.microsoft.com/library/windows/hardware/mt188052" data-raw-source="[&lt;strong&gt;UcxUsbDeviceCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt188052)"> <strong>UcxUsbDeviceCreate</strong></a>メソッド。</p>
</dd>
<dt>Endpoint オブジェクト (UCXENDPOINT)</dt>
<dd><p>USB デバイス オブジェクトのエンドポイントを表します。 通常内のホスト コント ローラーのドライバーによって作成された、 <a href="https://msdn.microsoft.com/library/windows/hardware/mt187839" data-raw-source="[&lt;em&gt;EVT_UCX_USBDEVICE_DEFAULT_ENDPOINT_ADD&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/mt187839)"> <em>EVT_UCX_USBDEVICE_DEFAULT_ENDPOINT_ADD</em> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/mt187843" data-raw-source="[&lt;em&gt;EVT_UCX_USBDEVICE_ENDPOINT_ADD&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/mt187843)"> <em>EVT_UCX_USBDEVICE_ENDPOINT_ADD</em></a>コールバックを呼び出すことによって、 <a href="https://msdn.microsoft.com/library/windows/hardware/mt188039" data-raw-source="[&lt;strong&gt;UcxEndpointCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt188039)"> <strong>UcxEndpointCreate</strong> </a>メソッド。</p>
</dd>
<dt>Stream オブジェクト (UCXSTREAMS)</dt>
<dd><p>1 つの一括エンドポイント全体をデバイスにパイプの数を表します。 通常内のホスト コント ローラーのドライバーによって作成された、 <a href="https://msdn.microsoft.com/library/windows/hardware/mt187830" data-raw-source="[&lt;em&gt;EVT_UCX_ENDPOINT_STATIC_STREAMS_ADD&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/mt187830)"> <em>EVT_UCX_ENDPOINT_STATIC_STREAMS_ADD</em> </a>コールバックを呼び出すことによって、 <a href="https://msdn.microsoft.com/library/windows/hardware/mt188050" data-raw-source="[&lt;strong&gt;UcxStaticStreamsCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt188050)"> <strong>UcxStaticStreamsCreate</strong></a>メソッド。</p>
</dd>
</dl>
<p><strong>ドキュメントのセクション</strong></p>
<a href="manage-the-root-hub-in-a-host-controller-driver.md" data-raw-source="[Root hub callback functions of a host controller driver](manage-the-root-hub-in-a-host-controller-driver.md)">ホスト コント ローラーのドライバーのルート ハブのコールバック関数</a>
<p>UCX は、ルート ハブに関連するほとんどの操作を処理します。 これにより、通常のハブと対話するのと同じ方法でルート ハブと対話する USB ハブのドライバーができます。 ホスト コント ローラーのドライバーでは、そのコールバック関数を登録できます。</p>
<a href="handling-i-o-requests-in-a-host-controller-driver.md" data-raw-source="[Handle I/O requests in a USB host controller driver](handling-i-o-requests-in-a-host-controller-driver.md)">USB ホスト コント ローラー ドライバーでの I/O 要求を処理します。</a>
<p>UCX 優先受信 USB 要求は、(翻訳) をブロックし、適切なエンドポイントのキューに転送します。</p>
<a href="configuring-usb-endpoints-in-a-host-controller-driver.md" data-raw-source="[Configure USB endpoints in a host controller driver](configuring-usb-endpoints-in-a-host-controller-driver.md)">ホスト コント ローラーのドライバーで USB エンドポイントを構成します。</a>
<p>ホスト コント ローラーのドライバーは、そのエンドポイントに関連付けられているキューの UCX の管理やコント ローラーのハードウェアにエンドポイントのプログラミングの役割を果たします。</p>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#host-controller-driver-reference" data-raw-source="[USB host controller extension (UCX) reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#host-controller-driver-reference)">USB ホスト コント ローラーの拡張機能 (UCX) リファレンス</a>
<p>I/O 要求、サポート ルーチン、構造、およびクライアント ドライバーによって使用されるインターフェイスの仕様を示します。 これらのルーチンと関連のデータ構造は、WDK ヘッダーで定義されます。</p>
<p>UCX と呼びます、<em>フレームワーク クラス拡張</em>します。</p>
<p>ホスト コント ローラーのドライバーと呼びます、<em>クライアント ドライバー</em>します。</p></td>

</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[ユニバーサル シリアル バス (USB)](https://msdn.microsoft.com/library/windows/hardware/ff538930)  



