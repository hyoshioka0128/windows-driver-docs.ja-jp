---
Description: トピックには、GitHub では、Windows ドライバーのサンプル リポジトリからダウンロード可能な USB サンプルに関する基本情報が含まれています。
title: USB ドライバーのサンプル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e8cecce9ec3e6ae3488f999674fdfb1095f664a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356601"
---
# <a name="usb-driver-samples"></a>USB ドライバーのサンプル


トピックにはからダウンロード可能な USB サンプルに関する基本情報が含まれています、 [Windows ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub リポジトリにあります。

## <a name="usb-samples"></a>USB のサンプル


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>サンプル名</th>
<th>サンプルの説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://go.microsoft.com/fwlink/p/?LinkId=618936" data-raw-source="[WDF Sample Driver Learning Lab for OSR USB-FX2](https://go.microsoft.com/fwlink/p/?LinkId=618936)">OSR usb-fx2 のラボをラーニング WDF サンプル ドライバー</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?LinkId=618002" data-raw-source="[Sample UMDF Function Driver for OSR USB-FX2](https://go.microsoft.com/fwlink/p/?LinkId=618002)">OSR usb-fx2 のサンプル UMDF 関数ドライバー</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?LinkId=618937" data-raw-source="[Sample KMDF Function Driver for OSR USB-FX2](https://go.microsoft.com/fwlink/p/?LinkId=618937)">OSR usb-fx2 のサンプル KMDF 関数ドライバー</a></p></td>
<td><p>OSRUSBFX2 サンプルでは、一括を実行し、Microsoft Windows Driver Frameworks (WDF) を使用して、ユニバーサル シリアル バス (USB) デバイスへのデータ転送を中断する方法を示します。 このサンプルは、OSR usb-fx2 Learning Kit に書き込まれます。 デバイスの仕様をご覧<a href="https://go.microsoft.com/fwlink/p/?linkid=64091" data-raw-source="[Using the OSR USB FX-2 Learning Kit V2.0](https://go.microsoft.com/fwlink/p/?linkid=64091)">OSR USB FX 2 ラーニング キット V2.0 を使用して</a>します。</p></td>
</tr>
<tr class="even">
<td><a href="https://go.microsoft.com/fwlink/p/?LinkId=618938" data-raw-source="[USBSAMP](https://go.microsoft.com/fwlink/p/?LinkId=618938)">USBSAMP</a></td>
<td><p>USBSAMP サンプルでは、Windows Driver Framework (WDF) を使用して一括と汎用の USB デバイスへの isochronous データ転送を実行する方法を示します。 このサンプルは、Intel 82930 USB テスト掲示板に書き込まれます。 一括とアイソクロナス転送を開始し、デバイスの I/O のエンドポイントに関する情報を取得するコンソール テスト アプリケーションが含まれています。 アプリケーションは GUID ベースのデバイス名とを使用して、オペレーティング システムによって生成されるパイプ名を使用する方法も示します、 <strong>SetupDiXXX</strong>ユーザー モード Api。</p></td>
</tr>
<tr class="odd">
<td><a href="https://go.microsoft.com/fwlink/p/?LinkId=618004" data-raw-source="[USBVIEW](https://go.microsoft.com/fwlink/p/?LinkId=618004)">USBVIEW</a></td>
<td><p>ユーザー モード アプリケーションの USB ホスト コント ローラー、USB ハブ、および接続されている USB デバイスを列挙できるし、デバイスを USB 要求と、レジストリからデバイスに関する情報をクエリできます USBVIEW サンプルを示しています。 USBVIEW は Windows Driver Model (WDM) に基づいています。</p>
<div class="alert">
<strong>注</strong>USBView ツールでは、取得、実行可能ファイルから Windows Driver Kit (WDK) (ツール&lt;em&gt;&lt;arch&gt; </em>フォルダー)。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

## <a name="building-a-sample"></a>サンプルの構築


サンプルのドライバーを構築する方法の詳細については、次を参照してください。[開発、テスト、および展開ドライバー](https://docs.microsoft.com/windows-hardware/drivers)します。

## <a name="related-topics"></a>関連トピック
[USB クライアント ドライバー開発の概要](getting-started-with-usb-client-driver-development.md)  



