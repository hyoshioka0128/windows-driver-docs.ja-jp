---
Description: Developing Windows drivers for emulated USB devices (UDE)
title: 列挙された USB デバイス (UDE) 用 Windows ドライバーの開発
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b36a2057ea3a8ab84023ef2bfa96e830d28f5d7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581277"
---
# <a name="developing-windows-drivers-for-emulated-usb-devices-ude"></a>列挙された USB デバイス (UDE) 用 Windows ドライバーの開発


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>目的</strong></p>
<p>このセクションでは、エミュレートされたユニバーサル シリアル バス (USB) ホスト コント ローラー ドライバーと、接続された仮想の USB デバイスを開発するため、Windows オペレーティング システムでエミュレートされた USB デバイス (UDE) のサポートについて説明します。 いずれのコンポーネントも、Microsoft 提供の USB デバイス エミュレーション クラス拡張 (UdeCx) と通信する 1 つの KMDF ドライバーに統合されます。</p>
<p><strong>開発ツールと Microsoft から提供されたバイナリ</strong></p>
<p>Windows Driver Kit (WDK) には、ヘッダー、ライブラリ、ツール、およびサンプルなど、ドライバーの開発に必要なリソースが含まれています。</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=617155" data-raw-source="[Download kits and tools for Windows](https://go.microsoft.com/fwlink/p/?linkid=617155)">Windows 用のキットとツールのダウンロード</a></p>
<p>関数のコント ローラーのドライバーを作成するには、次の必要があります。</p>
<ul>
<li>UdeCx: 関数のドライバーによって使用される、WDF の拡張機能が (udecx.sys)。 この拡張機能は、Windows に含まれます。</li>
<li>スタブ ライブラリ (Udecxstub.lib) にリンクします。 スタブ ライブラリでは、WDK に含まれています。</li>
<li>WDK で提供される Udecx.h が含まれます。</li>
</ul>
<p><strong>バージョン履歴</strong></p>
<p></p>
<dl>
<dt><a href=""></a>Windows 10</dt>
<dd><p>UDE バージョン 1.0。</p>
<p>KMDF バージョン 1.15 します。</p>
<p>UMDF がサポートされていません。</p>
</dd>
</dl></td>
<td><p><strong>UDE のアーキテクチャ</strong></p>
<a href="usb-emulated-device--ude--architecture.md" data-raw-source="[Architecture: USB Device Emulation (UDE)](usb-emulated-device--ude--architecture.md)">アーキテクチャ:USB デバイスのエミュレーション (UDE)</a>
<a href="usb-3-0-driver-stack-architecture.md" data-raw-source="[USB host-side drivers](usb-3-0-driver-stack-architecture.md)">ホスト側の USB ドライバー</a> Windows で
<p><strong>エミュレートされたホスト コント ローラーとデバイスのドライバーの記述</strong></p>
<p>UDE オブジェクトとハンドルの把握します。 詳細については、WDF オブジェクトは、次を参照してください。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff544249" data-raw-source="[Introduction to Framework Objects](https://msdn.microsoft.com/library/windows/hardware/ff544249)">Framework オブジェクトの概要</a>します。</p>
<p>動作を理解、UDE のクライアント ドライバーと、クライアント ドライバーである機能との対話方法を実装する必要があります。</p>
<p><a href="writing-a-ude-client-driver.md" data-raw-source="[Write a UDE client driver](writing-a-ude-client-driver.md)">UDE クライアント ドライバーを作成します。</a></p>
<p><strong>プログラミング リファレンスのセクション</strong></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#emulated-host-controller-driver-reference" data-raw-source="[Emulated USB host controller driver programming reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#emulated-host-controller-driver-reference)">エミュレートされた USB ホスト コントローラー ドライバーのプログラミング参照</a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/dn265590" data-raw-source="[WDF Reference](https://msdn.microsoft.com/library/windows/hardware/dn265590)">WDF の参照</a></p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[ユニバーサル シリアル バス (USB)](https://msdn.microsoft.com/library/windows/hardware/ff538930)  



