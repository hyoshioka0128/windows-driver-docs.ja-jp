---
Description: このセクションでは、このトピックでは、クラス ドライバーや汎用的なクライアント ドライバーでは、Microsoft によって提供される、親複合ドライバーについて説明します。
title: Microsoft が提供する USB ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04cb5e5ba904b5c738b7bffbec6e30e2c6a2a79c
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393120"
---
# <a name="microsoft-provided-usb-drivers"></a>Microsoft が提供する USB ドライバー


このセクションでは、このトピックでは、クラス ドライバーや汎用的なクライアント ドライバーでは、Microsoft によって提供される、親複合ドライバーについて説明します。

## <a name="microsoft-provided-usb-drivers-for-controllers-and-hubs"></a>コント ローラーとハブの Microsoft 提供の USB ドライバー


マイクロソフトでは、これらのドライバーのセットを提供します。

-   USB ホスト コント ローラーとハブ。 詳細については、次を参照してください。 [Windows での USB ホスト側ドライバー](usb-3-0-driver-stack-architecture.md)します。 USB ホスト コント ローラーの拡張機能 (UCX) ドライバーを使用した通信を行うカスタム ホスト コント ローラー ドライバーを開発することができます。 詳細については、次を参照してください。[開発 Windows ドライバーの USB ホスト コント ローラー](developing-windows-drivers-for-usb-host-controllers.md)します。
-   USB デバイスの共通の関数ロジックを処理します。 詳細については、次を参照してください。 [Windows での USB デバイス側ドライバー](usb-device-side-drivers-in-windows.md)します。
-   型 C コネクタをサポートします。 詳細については、次を参照してください。 [USB コネクタ マネージャー クラスの拡張機能 (UcmCx)](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188011(v=vs.85))します。

## <a name="other-microsoft-provided-usb-drivers"></a>その他の Microsoft 提供の USB ドライバー


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>デバイス セットアップ クラス</th>
<th>Microsoft 提供のドライバーと INF</th>
<th>Windows のサポート</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>USB</td>
<td><p>Usbccgp.sys</p>
<p>Usb.inf</p></td>
<td><p>Windows 8.1</p>
<p>Windows 8</p>
<p>Windows 7</p>
<p>Windows Vista</p>
<p>Windows XP</p></td>
<td>Usbccgp.sys は、複数の関数をサポートする複合デバイス用の親のドライバーです。 詳細については、次を参照してください。 <a href="usb-common-class-generic-parent-driver.md" data-raw-source="[USB Generic Parent Driver (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)">USB 汎用親ドライバー (Usbccgp.sys)</a>します。</td>
</tr>
<tr class="even">
<td>生体認証</td>
<td><p>WudfUsbBID.dll</p>
<p>WudfUsbBIDAdvanced.inf</p></td>
<td><p>Windows 8.1</p>
<p>Windows 8</p></td>
<td><p>マイクロソフトは、Windows 生体認証フレームワークを提供することで、USB 生体認証デバイス (指紋リーダー) をサポートします。 参照してください、 <a href="https://docs.microsoft.com/previous-versions/ff536448(v=vs.85)" data-raw-source="[Windows Biometric Framework](https://docs.microsoft.com/previous-versions/ff536448(v=vs.85))">Windows 生体認証フレームワーク</a>します。</p></td>
</tr>
<tr class="odd">
<td>メディア転送プロトコル デバイス</td>
<td>Wpdusb.sys (廃止)</td>
<td><p>Windows Server 2008</p>
<p>Windows Vista</p>
<p>Windows Server 2003</p>
<p>Windows XP</p></td>
<td><div class="alert">
<strong>注:</strong><br/><p>Windows 7 以降、Microsoft は、置き換え、Windows Vista の USB ドライバー スタック (Wpdusb.sys) のカーネル モード コンポーネントの Windows ポータブル デバイス (WPD) ジェネリック Winusb.sys で。</p>
</div>
<div>

</div>
<p>Microsoft では、メディア転送プロトコルをサポートするポータブル デバイスを管理する Wpdusb.sys ドライバーを提供します。 参照してください<a href="https://docs.microsoft.com/previous-versions/ff597864(v=vs.85)" data-raw-source="[WPD Design Guide](https://docs.microsoft.com/previous-versions/ff597864(v=vs.85))">WPD 設計ガイド</a>します。</p></td>
</tr>
<tr class="even">
<td>USBDevice</td>
<td><p>Winusb.sys</p>
<p>Winusb.inf</p></td>
<td><p>Windows 8.1</p>
<p>Windows 8</p>
<p>Windows 7</p>
<p>Windows Vista</p>
<p>Windows XP Service Pack 2 (SP2)</p></td>
<td>Winusb.sys は、ドライバーを実装する代わりに、USB デバイスの機能のドライバーとして使用できます。 参照してください<a href="how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md" data-raw-source="[WinUSB](how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md)">WinUSB</a>します。</td>
</tr>
</tbody>
</table>



## <a name="microsoft-provided-usb-device-class-drivers"></a>Microsoft 提供の USB デバイス クラス ドライバー


マイクロソフトは、USB によって承認されたいくつかの USB デバイス クラスに対するドライバーを提供しています-場合。 Windows では、これらのドライバーと、インストール ファイルが含まれます。 利用できる、 \\Windows\\System32\\DriverStore\\FileRepository フォルダー。

参照してください、 [USB デバイス クラス ドライバーが Windows に含まれる](supported-usb-classes.md)します。

## <a name="related-topics"></a>関連トピック
[ユニバーサル シリアル バス (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  
[USB ドライバー開発ガイド](usb-driver-development-guide.md)  



