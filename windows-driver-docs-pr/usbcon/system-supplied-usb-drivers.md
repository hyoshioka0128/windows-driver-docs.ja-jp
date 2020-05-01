---
Description: このセクションのトピックでは、Microsoft が提供するクラス ドライバー、汎用クライアント ドライバー、および親複合ドライバーについて説明します。
title: Microsoft が提供する USB ドライバーの概要
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: 689df8bf0f99b3f38a27bb1943a8bae61de86cfc
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "72007642"
---
# <a name="overview-of-microsoft-provided-usb-drivers"></a>Microsoft が提供する USB ドライバーの概要


このセクションのトピックでは、Microsoft が提供するクラス ドライバー、汎用クライアント ドライバー、および親複合ドライバーについて説明します。

## <a name="microsoft-provided-usb-drivers-for-controllers-and-hubs"></a>Microsoft が提供する、コントローラーとハブ用の USB ドライバー


Microsoft では、次の一連のドライバーを提供しています。

-   USB ホスト コントローラーとハブ向け。 詳細については、「[Windows の USB ホスト側ドライバー](usb-3-0-driver-stack-architecture.md)」を参照してください。 USB ホスト コントローラー 拡張 (UCX) ドライバーと通信するカスタム ホスト コントローラー ドライバーを開発することができます。 詳細については、[USB ホスト コントローラー用 Windows ドライバーの開発](developing-windows-drivers-for-usb-host-controllers.md)に関する記事を参照してください。
-   USB デバイス共通の関数ロジックの処理向け。 詳細については、「[Windows の USB デバイス側ドライバー](usb-device-side-drivers-in-windows.md)」を参照してください。
-   サポートされる Type-C コネクタ向け。 詳細については、[USB コネクタ マネージャー クラス拡張 (UcmCx)](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188011(v=vs.85))に関する記事を参照してください。

## <a name="other-microsoft-provided-usb-drivers"></a>Microsoft が提供するその他の USB ドライバー


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
<th>Microsoft 提供のドライバーおよび INF</th>
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
<td>Usbccgp.sys は、複数の機能をサポートする複合デバイス用の親ドライバーです。 詳細については、「<a href="usb-common-class-generic-parent-driver.md" data-raw-source="[USB Generic Parent Driver (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)">USB 汎用親ドライバー (Usbccgp.sys)</a>」を参照してください。</td>
</tr>
<tr class="even">
<td>生体認証</td>
<td><p>WudfUsbBID.dll</p>
<p>WudfUsbBIDAdvanced.inf</p></td>
<td><p>Windows 8.1</p>
<p>Windows 8</p></td>
<td><p>Microsoft では、Windows 生体認証フレームワークを提供することで、USB 生体認証デバイス (指紋リーダー) をサポートしています。 詳細については、「<a href="https://docs.microsoft.com/previous-versions/ff536448(v=vs.85)" data-raw-source="[Windows Biometric Framework](https://docs.microsoft.com/previous-versions/ff536448(v=vs.85))">Windows 生体認証フレームワーク</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td>メディア転送プロトコル デバイス</td>
<td>Wpdusb.sys (廃止)</td>
<td><p>Windows Server 2008</p>
<p>Windows Vista</p>
<p>Windows Server 2003</p>
<p>Windows XP</p></td>
<td><div class="alert">
<strong>注:</strong><br/><p>Windows 7 以降では、Windows ポータブル デバイス (WPD) の Windows Vista USB ドライバー スタック (Wpdusb) のカーネル モード コンポーネントが汎用 Winusb.sys に置き換えられました。</p>
</div>
<div>

</div>
<p>Microsoft では、メディア転送プロトコルをサポートするポータブル デバイスを管理するための Wpdusb.sys ドライバーを提供しています。 詳細については、「<a href="https://docs.microsoft.com/previous-versions/ff597864(v=vs.85)" data-raw-source="[WPD Design Guide](https://docs.microsoft.com/previous-versions/ff597864(v=vs.85))">WPD 設計ガイド</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td>USBDevice</td>
<td><p>Winusb.sys</p>
<p>Winusb.inf</p></td>
<td><p>Windows 8.1</p>
<p>Windows 8</p>
<p>Windows 7</p>
<p>Windows Vista</p>
<p>Windows XP with Service Pack 2 (SP2)</p></td>
<td>Winusb.sys は、ドライバーを実装する代わりに、USB デバイスの関数ドライバーとして使用できます。 詳細については、「<a href="how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md" data-raw-source="[WinUSB](how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md)">WinUSB</a>」を参照してください。</td>
</tr>
</tbody>
</table>



## <a name="microsoft-provided-usb-device-class-drivers"></a>Microsoft 提供の USB デバイス クラス ドライバー


Microsoft では、USB-IF によって承認された複数の USB デバイス クラス用のドライバーを提供しています。 これらのドライバーとそのインストール ファイルは、Windows に含まれています。 これらは、\\Windows\\System32\\DriverStore\\FileRepository フォルダーにあります。

詳細については、「[Windows に含まれる USB デバイス クラス ドライバー](supported-usb-classes.md)」を参照してください。

## <a name="related-topics"></a>関連トピック
[ユニバーサル シリアル バス (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  
[USB ドライバー開発ガイド](usb-driver-development-guide.md)  



