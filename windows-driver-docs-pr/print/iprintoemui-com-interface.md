---
title: IPrintOemUI COM インターフェイス
description: IPrintOemUI COM インターフェイス
ms.assetid: 7fd4071a-11ce-49e6-9e23-4f0643da1d98
keywords:
- IPrintOemUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: def2328270192eb63d59efa73d98ad58dc9b364a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539050"
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554159" data-raw-source="[&lt;strong&gt;IPrintOemUI::CommonUIProp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554159)"><strong>IPrintOemUI::CommonUIProp</strong></a></p></td>
<td><p>既存のプリンター プロパティ シート ページまたはドキュメントのプロパティ シート ページを変更するための UI プラグインを有効にします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554162" data-raw-source="[&lt;strong&gt;IPrintOemUI::DeviceCapabilities&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554162)"><strong>IPrintOemUI::DeviceCapabilities</strong></a></p></td>
<td><p>カスタマイズされたデバイスの機能を指定する UI プラグインを有効にします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554165" data-raw-source="[&lt;strong&gt;IPrintOemUI::DevicePropertySheets&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554165)"><strong>IPrintOemUI::DevicePropertySheets</strong></a></p></td>
<td><p>により、プリンター デバイスに新しいページを追加する UI プラグイン&#39;s プリンターのプロパティ シートです。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554167" data-raw-source="[&lt;strong&gt;IPrintOemUI::DevMode&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554167)"><strong>IPrintOemUI::DevMode</strong></a></p></td>
<td><p>プラグインの UI での操作を実行します。&#39;s プライベート<a href="https://msdn.microsoft.com/library/windows/hardware/ff552837" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552837)"> <strong>DEVMODEW</strong> </a>メンバー。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554172" data-raw-source="[&lt;strong&gt;IPrintOemUI::DevQueryPrintEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554172)"><strong>IPrintOemUI::DevQueryPrintEx</strong></a></p></td>
<td><p>印刷ジョブが印刷可能なかどうかを判断するための UI プラグインを有効にします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554173" data-raw-source="[&lt;strong&gt;IPrintOemUI::DocumentPropertySheets&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554173)"><strong>IPrintOemUI::DocumentPropertySheets</strong></a></p></td>
<td><p>により、プリンター デバイスに新しいページを追加する UI プラグイン&#39;s ドキュメントのプロパティ シートです。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554175" data-raw-source="[&lt;strong&gt;IPrintOemUI::DriverEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554175)"><strong>IPrintOemUI::DriverEvent</strong></a></p></td>
<td><p>プリンター ドライバーによってアクションが必要となるドライバー固有のイベントを処理するときに、印刷スプーラーによって呼び出されます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554176" data-raw-source="[&lt;strong&gt;IPrintOemUI::FontInstallerDlgProc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554176)"><strong>IPrintOemUI::FontInstallerDlgProc</strong></a></p></td>
<td><p>Unidrv フォントのインストーラーを置き換える&#39;s ユーザー インターフェイス。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554178" data-raw-source="[&lt;strong&gt;IPrintOemUI::GetInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554178)"><strong>IPrintOemUI::GetInfo</strong></a></p></td>
<td><p>(必要な実装です。)プラグインの UI を返す&#39;情報を識別します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554182" data-raw-source="[&lt;strong&gt;IPrintOemUI::PrinterEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554182)"><strong>IPrintOemUI::PrinterEvent</strong></a></p></td>
<td><p>プリンター イベントを処理するプラグインの UI を有効にします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554184" data-raw-source="[&lt;strong&gt;IPrintOemUI::PublishDriverInterface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554184)"><strong>IPrintOemUI::PublishDriverInterface</strong></a></p></td>
<td><p>(必要な実装です。)Unidrv または Pscript5 ドライバーへのポインターを提供&#39;s <a href="iprintoemdriverui-com-interface.md" data-raw-source="[IPrintOemDriverUI COM interface](iprintoemdriverui-com-interface.md)">IPrintOemDriverUI COM インターフェイス</a>、 <a href="iprintcoreui2-com-interface.md" data-raw-source="[IPrintCoreUI2 COM interface](iprintcoreui2-com-interface.md)">IPrintCoreUI2 COM インターフェイス</a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff552906" data-raw-source="[IPrintCoreHelperPS interface](https://msdn.microsoft.com/library/windows/hardware/ff552906)">IPrintCoreHelperPS インターフェイス</a>、または<a href="https://msdn.microsoft.com/library/windows/hardware/ff552940" data-raw-source="[IPrintCoreHelperUni interface](https://msdn.microsoft.com/library/windows/hardware/ff552940)">IPrintCoreHelperUni インターフェイス</a>します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554186" data-raw-source="[&lt;strong&gt;IPrintOemUI::QueryColorProfile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554186)"><strong>IPrintOemUI::QueryColorProfile</strong></a></p></td>
<td><p>プリンターのインターフェイスの色の管理に ICC プロファイルを指定する DLL を有効にします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554188" data-raw-source="[&lt;strong&gt;IPrintOemUI::UpdateExternalFonts&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554188)"><strong>IPrintOemUI::UpdateExternalFonts</strong></a></p></td>
<td><p>プリンター インターフェイス プリンターを更新する DLL を有効に&#39;s <a href="customized-font-management.md#ddk-unidrv-font-format-files-gg" data-raw-source="[Unidrv font format files](customized-font-management.md#ddk-unidrv-font-format-files-gg)">Unidrv フォント形式ファイル</a>します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554189" data-raw-source="[&lt;strong&gt;IPrintOemUI::UpgradePrinter&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554189)"><strong>IPrintOemUI::UpgradePrinter</strong></a></p></td>
<td><p>レジストリに格納されているデバイス オプションの値をアップグレードするための UI プラグインを有効にします。</p></td>
</tr>
</tbody>
</table>

 

詳細については、次を参照してください。[プリンター ドライバーの COM インターフェイスを実装する](implementing-printer-driver-com-interfaces.md)します。

 

 




