---
Description: USB 機能コントローラー用 Windows ドライバーの開発
title: USB 機能コントローラー用 Windows ドライバーの開発
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4b59d338829ef2a1d1f2984ea7d05872b25756f
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394029"
---
# <a name="developing-windows-drivers-for-usb-function-controllers"></a>USB 機能コントローラー用 Windows ドライバーの開発


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>目的</strong></p>
<p>このセクションでは、Windows オペレーティング システムの Microsoft 提供の USB 関数コント ローラー拡張機能 (UFX) と通信するユニバーサル シリアル バス (USB) 関数のコント ローラー ドライバーを開発するためのサポートについて説明します。</p>
<p><strong>開発ツールと Microsoft から提供されたバイナリ</strong></p>
<p>Windows Driver Kit (WDK) には、ヘッダー、ライブラリ、ツール、およびサンプルなど、ドライバーの開発に必要なリソースが含まれています。</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=617155" data-raw-source="[Download kits and tools for Windows](https://go.microsoft.com/fwlink/p/?linkid=617155)">Windows 用のキットとツールのダウンロード</a></p>
<p>関数のコント ローラーのドライバーを作成するには、次の必要があります。</p>
<ul>
<li>UFX (Ufx01000.sys) は、FDO として読み込まれます。 このドライバーは、Windows に含まれます。</li>
<li>スタブ ライブラリ (Ufx01000.lib) にリンクします。 スタブ ライブラリでは、WDK に含まれています。 ライブラリは、関数のコント ローラー ドライバーによって行われた呼び出しを変換し、UFX までに渡します。</li>
<li>WDK で提供される Ufxclient.h が含まれます。</li>
</ul>
<p>ユーザー モードから要求を送信する必要があります。</p>
<ul>
<li>関数の USB クラス ドライバーとして GenericUSBFn.sys が読み込まれます。 このドライバーは、Windows に含まれます。</li>
<li>WDK で提供される Genericusbfnioctl.h が含まれます。</li>
</ul>
<p>USB クラス ドライバーからの要求を送信するには、次の操作をする必要があります。</p>
<ul>
<li>UFX (Ufx01000.sys) は、FDO として読み込まれます。 このドライバーは、Windows に含まれます。</li>
<li>WDK で提供される Usbfnioctl.h が含まれます。</li>
</ul>
独自の充電器を充電を処理するフィルター ドライバーを作成するには、次の必要があります。
<ul>
<li>UfxChipidea.sys または Ufxsynopsys.sys のいずれかが、クライアント ドライバー UFX として読み込まれます。</li>
<li>WDK で提供される Ufxproprietarycharger.h が含まれます。</li>
</ul></td>
<td><p><strong>UFX のアーキテクチャ</strong></p>
<p>Microsoft 提供の USB ドライバー スタックを理解します。</p>
<a href="usb-device-side-drivers-in-windows.md" data-raw-source="[USB device-side drivers in Windows](usb-device-side-drivers-in-windows.md)">Windows の USB デバイス側ドライバー</a>
<p><strong>UFX オブジェクトおよびハンドルと理解します。</strong></p>
<p>UFX では、独自の特定の USB UCX オブジェクトを定義する WDF オブジェクトの機能を拡張します。 WDF のオブジェクトの詳細については、次を参照してください。 <a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/introduction-to-framework-objects" data-raw-source="[Introduction to Framework Objects](https://docs.microsoft.com/windows-hardware/drivers/wdf/introduction-to-framework-objects)">Framework オブジェクトの概要</a>します。</p>
<p>要求をキュー、UFX USB に固有のオブジェクトを使用します。 詳細については、 <a href="ufx-objects-and-handles-used-by-a-usb-function-controller.md" data-raw-source="[UFX objects and handles used by a USB function client driver](ufx-objects-and-handles-used-by-a-usb-function-controller.md)">UFX オブジェクトし、処理関数の USB クライアント ドライバーによって使用</a>します。</p>
<p><strong>関数のコント ローラーのクライアント ドライバーの作成</strong></p>
<p>動作を理解、UFX のクライアント ドライバーと、クライアント ドライバーである機能との対話方法を実装する必要があります。</p>
<p><a href="function-client-driver.md" data-raw-source="[Tasks for a function controller client driver](function-client-driver.md)">関数のコント ローラーのクライアント ドライバーのタスク</a></p>
<p><strong>プログラミング リファレンスのセクション</strong></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#function-class-driver-reference" data-raw-source="[USB function class driver to UFX programming reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#function-class-driver-reference)">USB クラス ドライバーを関数 UFX プログラミング リファレンスを</a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#usb-function-controller-client-driver-reference" data-raw-source="[USB function controller client driver programming reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#usb-function-controller-client-driver-reference)">USB 関数コント ローラー クライアント ドライバーのプログラミング リファレンス</a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#filter-driver-for-supporting-usb-chargers" data-raw-source="[USB filter driver for supporting proprietary chargers](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#filter-driver-for-supporting-usb-chargers)">独自の充電器をサポートするための USB フィルター ドライバー</a></p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[ユニバーサル シリアル バス (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  



