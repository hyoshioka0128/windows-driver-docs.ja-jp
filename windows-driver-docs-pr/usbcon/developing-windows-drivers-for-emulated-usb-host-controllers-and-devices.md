---
Description: 列挙された USB デバイス (UDE) 用 Windows ドライバー開発の概要
title: 列挙された USB デバイス (UDE) 用 Windows ドライバー開発の概要
ms.date: 10/23/2019
ms.localizationpriority: medium
ms.openlocfilehash: bd0282520841ea4273fd54940bf5bcb1ce858a1b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842394"
---
# <a name="overview-of-developing-windows-drivers-for-emulated-usb-devices-ude"></a>列挙された USB デバイス (UDE) 用 Windows ドライバー開発の概要


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>目的</strong></p>
<p>このセクションでは、エミュレートされた Universal Serial Bus (USB) ホストコントローラードライバーと接続された仮想 USB デバイスを開発するための、Windows オペレーティングシステムでの USB エミュレートデバイス (UDE) のサポートについて説明します。 いずれのコンポーネントも、Microsoft 提供の USB デバイス エミュレーション クラス拡張 (UdeCx) と通信する 1 つの KMDF ドライバーに統合されます。</p>
<p><strong>開発ツールと Microsoft 提供のバイナリ</strong></p>
<p>Windows Driver Kit (WDK) には、ドライバーの開発に必要なリソース (ヘッダー、ライブラリ、ツール、サンプルなど) が含まれています。</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=617155" data-raw-source="[Download kits and tools for Windows](https://go.microsoft.com/fwlink/p/?linkid=617155)">Windows 用のキットとツールのダウンロード</a></p>
<p>関数コントローラードライバーを作成するには、次のものが必要です。</p>
<ul>
<li>UdeCx: (udecx .sys) 関数ドライバーによって使用される WDF 拡張機能。 この拡張機能は、Windows に含まれています。</li>
<li>スタブライブラリ (Udecxstub .lib) にリンクします。 スタブライブラリは、WDK にあります。</li>
<li>WDK に用意されている Udecx を含めます。</li>
</ul>
<p><strong>バージョン履歴</strong></p>
<p></p>
<dl>
<dt> <a href=""> </a>Windows 10</dt>
<dd><p>UDE バージョン1.0。</p>
<p>KMDF バージョン1.15。</p>
<p>UMDF はサポートされていません。</p>
</dd>
</dl></td>
<td><p><strong>UDE のアーキテクチャ</strong></p>
<a href="usb-emulated-device--ude--architecture.md" data-raw-source="[Architecture: USB Device Emulation (UDE)](usb-emulated-device--ude--architecture.md)">アーキテクチャ: Windows における Usb デバイスエミュレーション (UDE)</a>
<a href="usb-3-0-driver-stack-architecture.md" data-raw-source="[USB host-side drivers](usb-3-0-driver-stack-architecture.md)">usb ホスト側ドライバー</a>
<p><strong>エミュレートされたホストコントローラーとデバイス用のドライバーの作成</strong></p>
<p>UDE のオブジェクトとハンドルについて理解を深めます。 WDF オブジェクトの詳細については、「<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/introduction-to-framework-objects" data-raw-source="[Introduction to Framework Objects](https://docs.microsoft.com/windows-hardware/drivers/wdf/introduction-to-framework-objects)">フレームワークオブジェクトの概要</a>」を参照してください。</p>
<p>UDE の動作、クライアントドライバーとどのようにやり取りするか、およびクライアントドライバーが実装することが期待される機能について理解します。</p>
<p><a href="writing-a-ude-client-driver.md" data-raw-source="[Write a UDE client driver](writing-a-ude-client-driver.md)">UDE クライアントドライバーを作成する</a></p>
<p><strong>プログラミングリファレンスセクション</strong></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#emulated-host-controller-driver-reference" data-raw-source="[Emulated USB host controller driver programming reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#emulated-host-controller-driver-reference)">エミュレートされた USB ホスト コントローラー ドライバーのプログラミング参照</a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_wdf/" data-raw-source="[WDF Reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/_wdf/)">WDF リファレンス</a></p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[ユニバーサル シリアル バス (USB)](https://docs.microsoft.com/windows-hardware/drivers/usbcon)  



