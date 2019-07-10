---
Description: このセクションのトピックでは、クライアント ドライバーが自分のデバイスを構成する必要がある方法について説明します。
title: USB ドライバーの概要で USB 構成の選択の概要
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 395cbcf02cecc65194073f52b6cb8248c6d26133
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716960"
---
# <a name="overview-of-selecting-a-usb-configuration-in-usb-drivers"></a>USB ドライバーで USB 構成の選択の概要


このセクションのトピックでは、クライアント ドライバーが自分のデバイスを構成する必要がある方法について説明します。

USB デバイスの一連のインターフェイスと呼ばれる形式でその機能を公開する、 *USB 構成*します。 各インターフェイスは 1 つまたは複数の代替設定と各代替の設定は、一連のエンドポイントの構成されます。 デバイスは、少なくとも 1 つの構成を提供する必要がありますが、デバイスで実行できる内容の定義を相互に排他的である複数の構成を提供することができます。 構成記述子の詳細については、次を参照してください。 [USB 構成記述子](usb-configuration-descriptors.md)します。

デバイスの構成には、各インターフェイスで、USB 構成、および代替インターフェイスを選択するクライアント ドライバーを実行するタスク。 クライアント ドライバーがデバイスの構成を読み取る必要がありますデバイスへの I/O 要求を送信する前には、情報を解析して、適切な構成を選択します。 クライアント ドライバーは、デバイスを職場にするためにでサポートされる構成の少なくとも 1 つを選択する必要があります。

WDM ベースのクライアント ドライバーは、USB デバイスで、構成のいずれかを選択できます。

クライアント ドライバーが基づいている場合[カーネル モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)または[ユーザー モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)、USB デバイスを構成するため、各フレームワーク インターフェイスを使用する必要があります。 Microsoft Visual Studio Professional 2012 と共に用意されている USB テンプレートを使用する場合に、テンプレート コードは、各インターフェイスの最初の構成と既定の代替設定を選択します。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>トピック</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="how-to-select-a-configuration-for-a-usb-device.md" data-raw-source="[How to select a configuration for a USB device](how-to-select-a-configuration-for-a-usb-device.md)">USB デバイスの構成を選択する方法</a></p></td>
<td><p>このトピックでは、ユニバーサル シリアル バス (USB) デバイスで、構成を選択する方法について説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="select-a-usb-alternate-setting.md" data-raw-source="[How to select an alternate setting in a USB interface](select-a-usb-alternate-setting.md)">USB インターフェイスで代替の設定を選択する方法</a></p></td>
<td><p>このトピックでは、選択インターフェイス USB インターフェイスでの代替設定をアクティブ化要求を発行する手順について説明します。 クライアント ドライバーでは、USB の設定を選択した後、この要求を発行する必要があります。 その構成内の各インターフェイスでの最初の代替設定をアクティブにも既定では、構成を選択します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="selecting-the-configuration-for-a-multiple-interface--composite--usb-d.md" data-raw-source="[Configuring Usbccgp.sys to Select a Non-Default USB Configuration](selecting-the-configuration-for-a-multiple-interface--composite--usb-d.md)">既定ではない USB 構成を選択する構成で、Usbccgp.sys</a></p></td>
<td><p>このトピックで、Usbccgp.sys USB 構成を選択する方法を構成するレジストリ設定について説明します。 Usbccgp.sys が複合デバイスの機能のいずれかを制御するクライアント ドライバーによって送信された選択構成要求を処理する方法についても説明します。</p></td>
</tr>
</tbody>
</table>

 

ファームウェアのダウンロードを必要とするデバイスの構成に関連する特別な考慮事項については、次を参照してください。 [USB デバイスの構成を必要とファームウェアのダウンロード](configuring-usb-devices-that-require-firmware-downloads.md)します。

## <a name="limitations-for-selecting-a-configuration"></a>構成を選択するための制限事項


クライアント ドライバーは WDF オブジェクトや、デバイスが 1 つのインターフェイスまたは複数のインターフェイスにあるかどうかを使用している場合、特定の制限が適用されます。 既定の構成を変更する前に、次の制限を考慮してください。

-   インターフェイスまたはインターフェイスのコレクションを管理する複合デバイス用のクライアント ドライバー、[汎用的な親の USB ドライバー](usb-common-class-generic-parent-driver.md) (Usbccgp.sys) デバイスの構成値を変更することはできません。 ただし、クライアント ドライバーでは、最初の (既定値) の構成以外の構成 を選択で、Usbccgp.sys を構成できます。 詳細については、次を参照してください。[既定以外の USB の構成を選択する構成で、Usbccgp.sys](selecting-the-configuration-for-a-multiple-interface--composite--usb-d.md)します。
-   フレームワークを使用している KMDF ベースのクライアント ドライバー [USB I/O ターゲット](https://docs.microsoft.com/windows-hardware/drivers/wdf/usb-i-o-targets)最初の構成のみを選択できます。
-   [WinUSB](winusb.md)最初の構成のみをサポートします。
-   多くの場合、クラス ドライバーには、複数の構成のサポートが不足しています。 デバイスが USB クラス仕様で定義されているクラスを実装する場合を参照してください、 [USB テクノロジ](https://go.microsoft.com/fwlink/p/?linkid=8769)デバイス クラスとクラス仕様に関する情報の web サイト。 Microsoft では、サポートされている USB デバイス クラスのクラス ドライバーを提供します。 詳しくは、「[サポートされる USB デバイス クラスのドライバー](supported-usb-classes.md)」をご覧ください。

## <a name="related-topics"></a>関連トピック
[USB ドライバー開発ガイド](usb-driver-development-guide.md)  
[USB 構成記述子](usb-configuration-descriptors.md)  
[USB デバイスを使用してください。](https://docs.microsoft.com/windows-hardware/drivers/wdf/working-with-usb-devices)  
[UMDF で USB インターフェイスの操作](https://docs.microsoft.com/windows-hardware/drivers/wdf/working-with-usb-interfaces-in-umdf-1-x-drivers)  



