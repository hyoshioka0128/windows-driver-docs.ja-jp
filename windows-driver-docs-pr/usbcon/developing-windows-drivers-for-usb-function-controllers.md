---
Description: USB ファンクション コントローラー用 Windows ドライバー開発の概要
title: USB ファンクション コントローラー用 Windows ドライバー開発の概要
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fae4e4aacb28a1cb4ec4b665c0e4cd7c2d3b7e5a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842393"
---
# <a name="overview-of-developing-windows-drivers-for-usb-function-controllers"></a>USB ファンクション コントローラー用 Windows ドライバー開発の概要


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>目的</strong></p>
<p>このセクションでは、Windows オペレーティングシステムでのサポートについて説明します。これは、Microsoft が提供する USB 機能コントローラー拡張機能 (UFX) と通信する Universal Serial Bus (USB) 関数コントローラードライバーを開発するためのものです。</p>
<p><strong>開発ツールと Microsoft 提供のバイナリ</strong></p>
<p>Windows Driver Kit (WDK) には、ドライバーの開発に必要なリソース (ヘッダー、ライブラリ、ツール、サンプルなど) が含まれています。</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=617155" data-raw-source="[Download kits and tools for Windows](https://go.microsoft.com/fwlink/p/?linkid=617155)">Windows 用のキットとツールのダウンロード</a></p>
<p>関数コントローラードライバーを作成するには、次のものが必要です。</p>
<ul>
<li>UFX (Ufx01000) が FDO として読み込まれました。 このドライバーは Windows に含まれています。</li>
<li>スタブライブラリ (Ufx01000) にリンクします。 スタブライブラリは、WDK にあります。 ライブラリは、関数コントローラードライバーによって行われた呼び出しを変換し、UFX に渡します。</li>
<li>WDK に用意されている Ufxclient. h を含めます。</li>
</ul>
<p>ユーザーモードから要求を送信するには、次のものが必要です。</p>
<ul>
<li>USB 関数クラスドライバーとして読み込まれた GenericUSBFn。 このドライバーは Windows に含まれています。</li>
<li>WDK に用意されている Genericusbfをインクルードします。</li>
</ul>
<p>USB クラスドライバーから要求を送信するには、次のものが必要です。</p>
<ul>
<li>UFX (Ufx01000) が FDO として読み込まれました。 このドライバーは Windows に含まれています。</li>
<li>WDK に用意されている Usbfをインクルードします。</li>
</ul>
独自の充電器による課金を処理するフィルタードライバーを作成するには、次のものが必要です。
<ul>
<li>UfxChipidea または Ufxsynopsys がクライアントドライバーとして UFX に読み込まれました。</li>
<li>WDK に用意されている Ufxproprietarycharger を含めます。</li>
</ul></td>
<td><p><strong>UFX のアーキテクチャ</strong></p>
<p>Microsoft 提供の USB ドライバースタックについて理解を深めてください。</p>
<a href="usb-device-side-drivers-in-windows.md" data-raw-source="[USB device-side drivers in Windows](usb-device-side-drivers-in-windows.md)">Windows の USB デバイス側ドライバー</a>
<p><strong>UFX オブジェクトとハンドルについて理解する</strong></p>
<p>UFX は、WDF オブジェクト機能を拡張して、独自の USB 固有の UCX オブジェクトを定義します。 WDF オブジェクトの詳細については、「<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/introduction-to-framework-objects" data-raw-source="[Introduction to Framework Objects](https://docs.microsoft.com/windows-hardware/drivers/wdf/introduction-to-framework-objects)">フレームワークオブジェクトの概要</a>」を参照してください。</p>
<p>キュー要求の場合、UFX は USB 固有のオブジェクトを使用します。 詳細については、「」を参照し<a href="ufx-objects-and-handles-used-by-a-usb-function-controller.md" data-raw-source="[UFX objects and handles used by a USB function client driver](ufx-objects-and-handles-used-by-a-usb-function-controller.md)">て</a>ください。</p>
<p><strong>関数コントローラークライアントドライバーの記述</strong></p>
<p>UFX の動作、クライアントドライバーとの対話方法、およびクライアントドライバーが実装することが期待される機能について説明します。</p>
<p><a href="function-client-driver.md" data-raw-source="[Tasks for a function controller client driver](function-client-driver.md)">関数コントローラークライアントドライバーのタスク</a></p>
<p><strong>プログラミングリファレンスセクション</strong></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#function-class-driver-reference" data-raw-source="[USB function class driver to UFX programming reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#function-class-driver-reference)">USB 関数クラスドライバーから UFX プログラミングリファレンス</a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#usb-function-controller-client-driver-reference" data-raw-source="[USB function controller client driver programming reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#usb-function-controller-client-driver-reference)">USB 関数コントローラークライアントドライバーのプログラミングリファレンス</a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#filter-driver-for-supporting-usb-chargers" data-raw-source="[USB filter driver for supporting proprietary chargers](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#filter-driver-for-supporting-usb-chargers)">独自の充電器をサポートするための USB フィルタードライバー</a></p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[ユニバーサル シリアル バス (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  



