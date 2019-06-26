---
title: IPrintOemUI COM インターフェイス
description: IPrintOemUI COM インターフェイス
ms.assetid: 7fd4071a-11ce-49e6-9e23-4f0643da1d98
keywords:
- IPrintOemUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64869d08d944166b8e40cb236fb506b507fe8af0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386945"
---
# <a name="iprintoemui-com-interface"></a>IPrintOemUI COM インターフェイス





`IPrintOemUI`の COM インターフェイスは、の方法で、[プリンター インターフェイス DLL](printer-interface-dll.md) Unidrv または Pscript5 プラグイン UI との通信用。 `IPrintOemUI`インターフェイスは、各 UI プラグインによって実装されます。

次の表とすべてのメソッドについて説明する`IPrintOemUI`インターフェイスの提供が終了します。 UI プラグインでは、一覧内のすべてのメソッドを定義する必要があります。 かどうか、メソッドは必要ありません、単に返すことができます E\_NOTIMPL します。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-commonuiprop" data-raw-source="[&lt;strong&gt;IPrintOemUI::CommonUIProp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-commonuiprop)"><strong>IPrintOemUI::CommonUIProp</strong></a></p></td>
<td><p>既存のプリンター プロパティ シート ページまたはドキュメントのプロパティ シート ページを変更するための UI プラグインを有効にします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-devicecapabilities" data-raw-source="[&lt;strong&gt;IPrintOemUI::DeviceCapabilities&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-devicecapabilities)"><strong>IPrintOemUI::DeviceCapabilities</strong></a></p></td>
<td><p>カスタマイズされたデバイスの機能を指定する UI プラグインを有効にします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-devicepropertysheets" data-raw-source="[&lt;strong&gt;IPrintOemUI::DevicePropertySheets&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-devicepropertysheets)"><strong>IPrintOemUI::DevicePropertySheets</strong></a></p></td>
<td><p>プリンター デバイスのプリンターのプロパティ シートに新しいページを追加する UI プラグインを有効にします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-devmode" data-raw-source="[&lt;strong&gt;IPrintOemUI::DevMode&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-devmode)"><strong>IPrintOemUI::DevMode</strong></a></p></td>
<td><p>UI プラグインのプライベートに対して操作を実行<a href="https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)"> <strong>DEVMODEW</strong> </a>メンバー。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-devqueryprintex" data-raw-source="[&lt;strong&gt;IPrintOemUI::DevQueryPrintEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-devqueryprintex)"><strong>IPrintOemUI::DevQueryPrintEx</strong></a></p></td>
<td><p>印刷ジョブが印刷可能なかどうかを判断するための UI プラグインを有効にします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-documentpropertysheets" data-raw-source="[&lt;strong&gt;IPrintOemUI::DocumentPropertySheets&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-documentpropertysheets)"><strong>IPrintOemUI::DocumentPropertySheets</strong></a></p></td>
<td><p>プリンター デバイスのドキュメントのプロパティ シートに新しいページを追加する UI プラグインを有効にします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-driverevent" data-raw-source="[&lt;strong&gt;IPrintOemUI::DriverEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-driverevent)"><strong>IPrintOemUI::DriverEvent</strong></a></p></td>
<td><p>プリンター ドライバーによってアクションが必要となるドライバー固有のイベントを処理するときに、印刷スプーラーによって呼び出されます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-fontinstallerdlgproc" data-raw-source="[&lt;strong&gt;IPrintOemUI::FontInstallerDlgProc&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-fontinstallerdlgproc)"><strong>IPrintOemUI::FontInstallerDlgProc</strong></a></p></td>
<td><p>Unidrv フォント インストーラーのユーザー インターフェイスが置き換えられます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-getinfo" data-raw-source="[&lt;strong&gt;IPrintOemUI::GetInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-getinfo)"><strong>IPrintOemUI::GetInfo</strong></a></p></td>
<td><p>(必要な実装です。)UI プラグインの識別情報を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-printerevent" data-raw-source="[&lt;strong&gt;IPrintOemUI::PrinterEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-printerevent)"><strong>IPrintOemUI::PrinterEvent</strong></a></p></td>
<td><p>プリンター イベントを処理するプラグインの UI を有効にします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-publishdriverinterface" data-raw-source="[&lt;strong&gt;IPrintOemUI::PublishDriverInterface&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-publishdriverinterface)"><strong>IPrintOemUI::PublishDriverInterface</strong></a></p></td>
<td><p>(必要な実装です。)Unidrv または Pscript5 ドライバーへのポインターを提供<a href="iprintoemdriverui-com-interface.md" data-raw-source="[IPrintOemDriverUI COM interface](iprintoemdriverui-com-interface.md)">IPrintOemDriverUI COM インターフェイス</a>、 <a href="iprintcoreui2-com-interface.md" data-raw-source="[IPrintCoreUI2 COM interface](iprintcoreui2-com-interface.md)">IPrintCoreUI2 COM インターフェイス</a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelperps" data-raw-source="[IPrintCoreHelperPS interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelperps)">IPrintCoreHelperPS インターフェイス</a>、または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelperuni" data-raw-source="[IPrintCoreHelperUni interface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelperuni)">IPrintCoreHelperUni インターフェイス</a>します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-querycolorprofile" data-raw-source="[&lt;strong&gt;IPrintOemUI::QueryColorProfile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-querycolorprofile)"><strong>IPrintOemUI::QueryColorProfile</strong></a></p></td>
<td><p>プリンターのインターフェイスの色の管理に ICC プロファイルを指定する DLL を有効にします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-updateexternalfonts" data-raw-source="[&lt;strong&gt;IPrintOemUI::UpdateExternalFonts&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-updateexternalfonts)"><strong>IPrintOemUI::UpdateExternalFonts</strong></a></p></td>
<td><p>プリンターのインターフェイスを更新するプリンターの DLL を有効に<a href="customized-font-management.md#ddk-unidrv-font-format-files-gg" data-raw-source="[Unidrv font format files](customized-font-management.md#ddk-unidrv-font-format-files-gg)">Unidrv フォント形式ファイル</a>します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-upgradeprinter" data-raw-source="[&lt;strong&gt;IPrintOemUI::UpgradePrinter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui-upgradeprinter)"><strong>IPrintOemUI::UpgradePrinter</strong></a></p></td>
<td><p>レジストリに格納されているデバイス オプションの値をアップグレードするための UI プラグインを有効にします。</p></td>
</tr>
</tbody>
</table>

 

詳細については、次を参照してください。[プリンター ドライバーの COM インターフェイスを実装する](implementing-printer-driver-com-interfaces.md)します。

 

 




