---
title: ドライバーの作成の必要性
description: Microsoft Windows には、さまざまなデバイスの種類に対応する組み込みのドライバーが用意されています。 目的のデバイスの種類に対応する組み込みドライバーがあれば、独自のドライバーを作成する必要はありません。 そのデバイスでは組み込みのドライバーを使うことができます。
ms.assetid: B08994F9-9E60-4C49-BD5C-F5C128075D33
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6adf04958f07f0ed460c07a0c9c71091f23f54b4
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "63371364"
---
# <a name="do-you-need-to-write-a-driver"></a>ドライバーの作成の必要性


Microsoft Windows には、さまざまなデバイスの種類に対応する組み込みのドライバーが用意されています。 目的のデバイスの種類に対応する組み込みドライバーがあれば、独自のドライバーを作成する必要はありません。 そのデバイスでは組み込みのドライバーを使うことができます。

## <a name="span-idbuilt-indriversforusbdevicesspanspan-idbuilt-indriversforusbdevicesspanspan-idbuilt-indriversforusbdevicesspanbuilt-in-drivers-for-usb-devices"></a><span id="Built-in_drivers_for_USB_devices"></span><span id="built-in_drivers_for_usb_devices"></span><span id="BUILT-IN_DRIVERS_FOR_USB_DEVICES"></span>USB デバイス用の組み込みドライバー


デバイスが USB Device Working Group (DWG) によって定義されるデバイス クラスに属している場合は、既に Windows USB クラス ドライバーが用意されている可能性があります。 詳しくは、「[サポートされる USB デバイス クラスのドライバー](https://msdn.microsoft.com/library/windows/hardware/ff538820)」をご覧ください。

## <a name="span-idbuilt-indriversforotherdevicesspanspan-idbuilt-indriversforotherdevicesspanspan-idbuilt-indriversforotherdevicesspanbuilt-in-drivers-for-other-devices"></a><span id="Built-in_drivers_for_other_devices"></span><span id="built-in_drivers_for_other_devices"></span><span id="BUILT-IN_DRIVERS_FOR_OTHER_DEVICES"></span>その他のデバイス用の組み込みドライバー


現在、Microsoft は以下の種類のデバイスに対して組み込みドライバーを提供しています。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">デバイス テクノロジとドライバー</th>
<th align="left">組み込みドライバー</th>
<th align="left">Windows のサポート</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ACPI: ACPI ドライバー</p></td>
<td align="left"><p>Acpi.sys</p></td>
<td align="left"><p>Windows XP 以降</p></td>
<td align="left"><p>Microsoft は、Acpi.sys ドライバーと ACPI BIOS を通じて基本的な ACPI デバイス機能をサポートしています。 ベンダーでは、ACPI デバイスの機能を強化するために WDM ファンクション ドライバーを提供できます。 Windows の ACPI サポートについて詳しくは、ACPI 設計ガイドの <a href="https://msdn.microsoft.com/library/windows/hardware/ff536161" data-raw-source="[Supporting ACPI Devices](https://msdn.microsoft.com/library/windows/hardware/ff536161)">ACPI デバイスのサポートに関するページ</a>をご覧ください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>オーディオ:Microsoft オーディオ クラス ドライバー</p></td>
<td align="left"><p>PortCls.sys</p></td>
<td align="left"><p>Windows XP 以降</p></td>
<td align="left"><p>Microsoft は、ポート クラス ドライバー (PortCls) を通じて基本的なオーディオ レンダリングとオーディオ キャプチャをサポートしています。 PortCls と連携するアダプター ドライバーを提供するのは、オーディオ デバイスのハードウェア ベンダーの役割です。 アダプター ドライバーには、初期化コード、ドライバー管理コード (DriverEntry 関数を含む)、オーディオ ミニポート ドライバーのコレクションが含まれます。 詳しくは、<a href="https://msdn.microsoft.com/library/windows/hardware/ff536829" data-raw-source="[Introduction to Port Class](https://msdn.microsoft.com/library/windows/hardware/ff536829)">ポート クラスの概要に関するページ</a>をご覧ください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>バス: ネイティブ SD バス ドライバー、ネイティブ SD ストレージ クラス ドライバー、ストレージ ミニポート ドライバー</p></td>
<td align="left"><p>sdbus.sys、sffdisk.sys、sffp_sd.sys</p></td>
<td align="left"><p>Windows Vista 以降</p></td>
<td align="left"><p>Microsoft では、SD カード リーダーを次のようにサポートしています。まず、オペレーティング システムにより、PCI バスに直接接続する SD ホスト コントローラーのサポートが提供されます。 システムが SD ホスト コントローラーを列挙するときに、ネイティブの SD バス ドライバー (sdbus.sys) が読み込まれます。 ユーザーが SD メモリ カードを挿入すると、Windows は、このバス ドライバーの上位にネイティブの SD ストレージ クラス ドライバー (sffdisk.sys) とストレージ ミニポート ドライバー (sffp_sd.sys) を読み込みます。 GPS やワイヤレス LAN など、機能の異なる SD カードが挿入された場合は、そのデバイス用にベンダーから提供されているドライバーが読み込まれます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HID: HID I2C ドライバー</p></td>
<td align="left"><p>HIDI2C.sys</p></td>
<td align="left"><p>Windows 8 以降</p></td>
<td align="left"><p>Microsoft は、SPB (Simple Peripheral Bus) と汎用 I/O (GPIO) をサポートする SoC システムで HID over I2C デバイスをサポートしています。 これには HIDI2C.sys ドライバーが使われます。 詳しくは、「<a href="https://msdn.microsoft.com/library/windows/hardware/jj127208" data-raw-source="[HID over I2C](https://msdn.microsoft.com/library/windows/hardware/jj127208)">HID over I2C</a>」をご覧ください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HID: レガシ ゲーム ポート ドライバー</p></td>
<td align="left"><p>HidGame.sys、Gameenum.sys</p></td>
<td align="left"><p>Windows Vista</p>
<p>Windows Server 2003</p>
<p>Windows XP</p></td>
<td align="left"><p>Windows Vista 以前では、Microsoft は HidGame.sys ドライバーと Gameenum.sys ドライバーを通じてレガシ (USB でなく、Bluetooth でなく、I2C でもない) ゲーム ポートをサポートしています。 詳しくは、「<a href="https://msdn.microsoft.com/library/windows/hardware/jj126201" data-raw-source="[HID Transports Supported in Windows](https://msdn.microsoft.com/library/windows/hardware/jj126201)">Windows でサポートされる HID トランスポート</a>」をご覧ください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HID: レガシ キーボード クラス ドライバー</p></td>
<td align="left"><p>Kbdclass.sys</p></td>
<td align="left"><p>Windows XP 以降</p></td>
<td align="left"><p>Microsoft は、Kbdclass.sys ドライバーを通じてレガシ (USB でなく、Bluetooth でなく、I2C でもない) キーボードをサポートしています。 詳しくは、キーボードとマウスの HID クライアント ドライバーをご覧ください。 ベンダーでは、レガシ キーボードの機能を強化するためにキーボード フィルター ドライバーを提供できます。 詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=618052" data-raw-source="[Kbfiltr sample](https://go.microsoft.com/fwlink/p/?LinkId=618052)">Kbfiltr のサンプル</a>をご覧ください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HID: レガシ マウス クラス ドライバー</p></td>
<td align="left"><p>Mouclass.sys</p></td>
<td align="left"><p>Windows XP 以降</p></td>
<td align="left"><p>Microsoft は、Mouclass.sys ドライバーを通じてレガシ (USB でなく、Bluetooth でなく、I2C でもない) マウスをサポートしています。 キーボードとマウスの HID クライアント ドライバーをご覧ください。 ベンダーでは、レガシ マウスの機能を強化するためにマウス フィルター ドライバーを提供できます。 詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=618052" data-raw-source="[Moufiltr sample](https://go.microsoft.com/fwlink/p/?LinkId=618052)">Moufiltr のサンプル</a>をご覧ください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HID: PS/2 (i8042prt) ドライバー</p></td>
<td align="left"><p>I8042prt.sys</p></td>
<td align="left"><p>Windows XP 以降</p></td>
<td align="left"><p>Microsoft は、I8042.sys ドライバーを通じてレガシ PS/2 キーボードとマウスをサポートしています。 ベンダーでは、PS/2 マウスまたはキーボードの機能を強化するために、キーボードまたはマウスのフィルター ドライバーを提供できます。 詳しくは、<a href="https://go.microsoft.com/fwlink/p/?LinkId=618052" data-raw-source="[Kbfiltr sample](https://go.microsoft.com/fwlink/p/?LinkId=618052)">Kbfiltr のサンプル</a>と <a href="https://go.microsoft.com/fwlink/p/?LinkId=618052" data-raw-source="[Moufiltr sample](https://go.microsoft.com/fwlink/p/?LinkId=618052)">Moufiltr のサンプル</a>をご覧ください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>イメージング: Web Services for Devices (WSD) スキャン クラス ドライバー</p></td>
<td align="left"><p>WSDScan.sys</p></td>
<td align="left"><p>Windows Vista 以降</p></td>
<td align="left"><p>Microsoft は、WSD スキャン ドライバー (wsdscan.sys) を通じて Web サービス スキャナー (Web 経由で使われるスキャナー) をサポートしています。 ただし、WSD 分散スキャン管理をサポートする Web サービス スキャナー デバイスには 2 つの Web サービス プロトコルを実装する必要があります。 詳しくは、<a href="https://msdn.microsoft.com/library/windows/hardware/ff553313" data-raw-source="[WIA with Web Services for Devices](https://msdn.microsoft.com/library/windows/hardware/ff553313)">WIA と Web Services for Devices に関するページ</a>をご覧ください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>印刷:Microsoft プロッター ドライバー</p></td>
<td align="left"><p>Msplot</p></td>
<td align="left"><p>Windows XP 以降</p></td>
<td align="left"><p>Microsoft は、Microsoft プロッター ドライバー (Msplot) を通じて、Hewlett-Packard Graphics Language をサポートするプロッターをサポートしています。 プロッターの機能を強化するために、1 つ以上の Plotter Characterization Data (PCD) ファイルから成るミニドライバーを作成できます。 詳しくは、<a href="https://msdn.microsoft.com/library/windows/hardware/ff559833" data-raw-source="[Plotter Driver Minidrivers](https://msdn.microsoft.com/library/windows/hardware/ff559833)">プロッター ドライバーのミニドライバーに関するページ</a>をご覧ください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>印刷:Microsoft PostScript プリンター ドライバー</p></td>
<td align="left"><p>Pscript</p></td>
<td align="left"><p>Windows XP 以降</p></td>
<td align="left"><p>Microsoft は、PostScript プリンター ドライバー (Pscript) を通じて PostScript プリンターをサポートしています。 PostScript プリンターの機能を強化するために、1 つ以上の PostScript Printer Description (PPD) ファイルとフォント (NTF) ファイルから成るミニドライバーを作成できます。 詳しくは、<a href="https://msdn.microsoft.com/library/windows/hardware/ff561810" data-raw-source="[Pscript Minidrivers](https://msdn.microsoft.com/library/windows/hardware/ff561810)">Pscript ミニドライバーに関するページ</a>をご覧ください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>印刷:Microsoft ユニバーサル プリンター ドライバー</p></td>
<td align="left"><p>Unidrv</p></td>
<td align="left"><p>Windows XP 以降</p></td>
<td align="left"><p>Microsoft は、ユニバーサル プリンター ドライバー (Unidrv) を通じて PostScript 以外のプリンターをサポートしています。 PostScript 以外のプリンターの機能を強化するために、1 つ以上の Generic Printer Description (GPD) ファイルから成るミニドライバーを作成できます。 詳しくは、<a href="https://msdn.microsoft.com/library/windows/hardware/ff556567" data-raw-source="[Microsoft Universal Printer Driver](https://msdn.microsoft.com/library/windows/hardware/ff556567)">Microsoft ユニバーサル プリンター ドライバーに関するページ</a>をご覧ください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>印刷:Microsoft v4 プリンター ドライバー</p></td>
<td align="left"></td>
<td align="left"><p>Windows 8 以降</p></td>
<td align="left"><p>Windows 8 以降では、PostScript と PostScript 以外のプリンター、およびプロッターをサポートする 1 つのインボックス クラス ドライバーが Microsoft から提供されています。 このドライバーは、Microsoft プロッター ドライバー、Microsoft ユニバーサル プリンター ドライバー、Microsoft PostScript プリンター ドライバーよりも優先されます。 このプリンター ドライバーは、変更せずに単独で使用した場合に、基本的な印刷機能をサポートします。 詳しくは、<a href="https://msdn.microsoft.com/library/windows/hardware/hh706306" data-raw-source="[V4 Printer Driver](https://msdn.microsoft.com/library/windows/hardware/hh706306)">V4 プリンター ドライバーに関するページ</a>をご覧ください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>印刷:Microsoft XPS プリンター ドライバー</p></td>
<td align="left"><p>XPSDrv</p></td>
<td align="left"><p>Windows Vista 以降</p></td>
<td align="left"><p>Microsoft は、XPS プリンター ドライバー (XPSDrv) によって XPS ドキュメント形式の印刷をサポートしています。 このドライバーは、Microsoft の GDI ベースのバージョン 3 プリンター ドライバー アーキテクチャを拡張して、XML Paper Specification (XPS) ドキュメントの処理をサポートします。 XPSDrv プリンター ドライバーにより、XPS ドキュメント形式はスプール ファイル形式としてもドキュメント ファイル形式としても使われます。 XPSDrv プリンター ドライバーは、変更しなくても単独で基本的な XPS 印刷機能をサポートします。 詳しくは、<a href="https://msdn.microsoft.com/library/windows/hardware/ff564289" data-raw-source="[XPSDrv Printer Drivers](https://msdn.microsoft.com/library/windows/hardware/ff564289)">XPSDrv プリンター ドライバーに関するページ</a>をご覧ください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>センサー: センサー HID クラス ドライバー</p></td>
<td align="left"><p>SensorsHIDClassDriver.dll</p></td>
<td align="left"><p>Windows 8 以降</p></td>
<td align="left"><p>Microsoft は、HID クラス ドライバーを通じて、モーション センサーやアクティビティ センサー、その他の種類のセンサーをサポートしています。 Windows 8 には、この HID クラス ドライバーと、対応する HID I2C および HID USB ミニポート ドライバーが用意されているため、独自のドライバーを実装する必要はありません。 必要な処理は、このホワイト ペーパーに説明されている使用法をセンサーのファームウェアで報告することだけです。 Windows は、ファームウェアと Windows 自身の HID ドライバーを使ってセンサーの有効化と初期設定を行い、関連する Windows API からセンサーにアクセスできるようにします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>タッチ: Windows ポインター デバイス ドライバー</p></td>
<td align="left"></td>
<td align="left"><p>Windows 8 以降</p></td>
<td align="left"><p>Microsoft は、HID クラス ドライバーを通じてペン デバイスとタッチ デバイスをサポートしています。 Windows 8 には、この HID クラス ドライバーと、対応する HID I2C および HID USB ミニポート ドライバーが用意されているため、独自のドライバーを実装する必要はありません。 必要な処理は、このホワイト ペーパーに説明されている使用法をポインター デバイスのファームウェアで報告することだけです。 Windows は、ファームウェアと Windows 自身の HID ドライバーを使ってタッチとポインターの機能を有効にして、Windows のタッチおよびポインター API からデバイスにアクセスできるようにします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WPD: メディア転送プロトコル クラス ドライバー</p></td>
<td align="left"><p>WpdMtpDr.dll、WpdMtp.dll、WpdMtpUs.dll、WpdConns.dll、WpdUsb.sys</p></td>
<td align="left"><p>Windows Vista 以降</p></td>
<td align="left"><p>Microsoft は、メディア転送プロトコル クラス ドライバーを通じて、Windows との接続が必要となるポータブル デバイスをサポートしています。このようなデバイスには、音楽プレーヤー、デジタル カメラ、携帯電話、健康管理デバイスなどがあります。 このクラス ドライバーを使うベンダーは、デバイスに MTP クラス プロトコルを実装する必要があります (デジタル スチル カメラの場合、MTP の実装は PTP との下位互換性を保つ必要があります)。詳しくは、「<a href="https://msdn.microsoft.com/library/windows/hardware/ff597573" data-raw-source="[Guidance for the Hardware Vendor](https://msdn.microsoft.com/library/windows/hardware/ff597573)">Guidance for the Hardware Vendor (ハードウェア ベンダー向けのガイダンス)</a>」をご覧ください。</p></td>
</tr>
</tbody>
</table>

 

 

 





