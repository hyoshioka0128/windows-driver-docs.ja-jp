---
title: IPrintOemUI COM インターフェイス
description: IPrintOemUI COM インターフェイス
ms.assetid: 7fd4071a-11ce-49e6-9e23-4f0643da1d98
keywords:
- IPrintOemUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 804a9b8f276219b40e251c0e866bf3dbd7c8b0a7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844318"
---
# <a name="iprintoemui-com-interface"></a>IPrintOemUI COM インターフェイス





`IPrintOemUI` COM インターフェイスは、Unidrv または Pscript5 の[プリンターインターフェイス DLL](printer-interface-dll.md)が UI プラグインと通信する手段です。 `IPrintOemUI` インターフェイスは、各 UI プラグインによって実装されます。

次の表に、`IPrintOemUI` インターフェイスによって提供されるすべてのメソッドとその説明を示します。 UI プラグインでは、表示されているすべてのメソッドを定義する必要があります。 メソッドが不要な場合は、単に E\_NOTIMPL を返すことができます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メソッド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-commonuiprop" data-raw-source="[&lt;strong&gt;IPrintOemUI::CommonUIProp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-commonuiprop)"><strong>IPrintOemUI:: CommonUIProp</strong></a></p></td>
<td><p>既存のプリンタープロパティシートページまたはドキュメントプロパティシートページを UI プラグインで変更できるようにします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devicecapabilities" data-raw-source="[&lt;strong&gt;IPrintOemUI::DeviceCapabilities&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devicecapabilities)"><strong>IPrintOemUI::D eviceCapabilities</strong></a></p></td>
<td><p>UI プラグインでカスタマイズされたデバイス機能を指定できるようにします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devicepropertysheets" data-raw-source="[&lt;strong&gt;IPrintOemUI::DevicePropertySheets&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devicepropertysheets)"><strong>IPrintOemUI::D evicePropertySheets</strong></a></p></td>
<td><p>UI プラグインを使用して、プリンターデバイスのプリンタープロパティシートに新しいページを追加できるようにします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devmode" data-raw-source="[&lt;strong&gt;IPrintOemUI::DevMode&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devmode)"><strong>IPrintOemUI::D evMode</strong></a></p></td>
<td><p>UI プラグインのプライベート<a href="https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)"><strong>Devmodew</strong></a>メンバーに対して操作を実行します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devqueryprintex" data-raw-source="[&lt;strong&gt;IPrintOemUI::DevQueryPrintEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devqueryprintex)"><strong>IPrintOemUI::D evQueryPrintEx</strong></a></p></td>
<td><p>印刷ジョブが印刷可能かどうかを判断するために UI プラグインを有効にします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-documentpropertysheets" data-raw-source="[&lt;strong&gt;IPrintOemUI::DocumentPropertySheets&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-documentpropertysheets)"><strong>IPrintOemUI::D ocumentPropertySheets</strong></a></p></td>
<td><p>UI プラグインを使用して、プリンターデバイスのドキュメントプロパティシートに新しいページを追加できるようにします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-driverevent" data-raw-source="[&lt;strong&gt;IPrintOemUI::DriverEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-driverevent)"><strong>IPrintOemUI::D riverEvent</strong></a></p></td>
<td><p>プリンタードライバーによる操作を必要とする可能性のあるドライバー固有のイベントを処理するときに、印刷スプーラによって呼び出されます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-fontinstallerdlgproc" data-raw-source="[&lt;strong&gt;IPrintOemUI::FontInstallerDlgProc&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-fontinstallerdlgproc)"><strong>IPrintOemUI:: Fontインストーラ Dlgproc</strong></a></p></td>
<td><p>Unidrv フォントインストーラーのユーザーインターフェイスを置き換えます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-getinfo" data-raw-source="[&lt;strong&gt;IPrintOemUI::GetInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-getinfo)"><strong>IPrintOemUI:: GetInfo</strong></a></p></td>
<td><p>(実装が必要です)。UI プラグインの識別情報を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-printerevent" data-raw-source="[&lt;strong&gt;IPrintOemUI::PrinterEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-printerevent)"><strong>IPrintOemUI::P rinterEvent</strong></a></p></td>
<td><p>UI プラグインがプリンターイベントを処理できるようにします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-publishdriverinterface" data-raw-source="[&lt;strong&gt;IPrintOemUI::PublishDriverInterface&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-publishdriverinterface)"><strong>IPrintOemUI::P ublishDriverInterface</strong></a></p></td>
<td><p>(実装が必要です)。Unidrv または Pscript5 ドライバーの<a href="iprintoemdriverui-com-interface.md" data-raw-source="[IPrintOemDriverUI COM interface](iprintoemdriverui-com-interface.md)">Iprintoemdriverui com インターフェイス</a>、 <a href="iprintcoreui2-com-interface.md" data-raw-source="[IPrintCoreUI2 COM interface](iprintcoreui2-com-interface.md)">IPrintCoreUI2 com インターフェイス</a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperps" data-raw-source="[IPrintCoreHelperPS interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperps)">iprintcore perps</a>インターフェイス、または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni" data-raw-source="[IPrintCoreHelperUni interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni)">iprintcore peruni インターフェイス</a>へのポインターを提供します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-querycolorprofile" data-raw-source="[&lt;strong&gt;IPrintOemUI::QueryColorProfile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-querycolorprofile)"><strong>IPrintOemUI:: QueryColorProfile</strong></a></p></td>
<td><p>プリンターインターフェイス DLL がカラー管理用の ICC プロファイルを指定できるようにします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-updateexternalfonts" data-raw-source="[&lt;strong&gt;IPrintOemUI::UpdateExternalFonts&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-updateexternalfonts)"><strong>IPrintOemUI:: UpdateExternalFonts</strong></a></p></td>
<td><p>プリンターインターフェイス DLL がプリンターの<a href="customized-font-management.md#ddk-unidrv-font-format-files-gg" data-raw-source="[Unidrv font format files](customized-font-management.md#ddk-unidrv-font-format-files-gg)">Unidrv フォントフォーマットファイル</a>を更新できるようにします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-upgradeprinter" data-raw-source="[&lt;strong&gt;IPrintOemUI::UpgradePrinter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-upgradeprinter)"><strong>IPrintOemUI:: UpgradePrinter</strong></a></p></td>
<td><p>レジストリに格納されているデバイスオプション値を UI プラグインでアップグレードできるようにします。</p></td>
</tr>
</tbody>
</table>

 

詳細については、「[プリンタドライバ COM インターフェイスの実装](implementing-printer-driver-com-interfaces.md)」を参照してください。

 

 




