---
title: IPrintCoreUI2 COM インターフェイス
description: IPrintCoreUI2 COM インターフェイス
ms.assetid: 3c9df0ac-d823-4c27-bd34-85765f48b972
keywords:
- IPrintCoreUI2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6fba8d8e0b9f7114afe814f8eb1407b78453d88
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384187"
---
# <a name="iprintcoreui2-com-interface"></a>IPrintCoreUI2 COM インターフェイス





`IPrintCoreUI2` COM インターフェイスは、拡張、 [IPrintOemDriverUI COM インターフェイス](iprintoemdriverui-com-interface.md)します。 Windows XP 以降では、Pscript5 ドライバーは、提供、 `IPrintCoreUI2` COM インターフェイスです。 このインターフェイスのメソッドは Pscript5 UI プラグインでのみ使用されます。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-drvgetdriversetting" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::DrvGetDriverSetting&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-drvgetdriversetting)"><strong>IPrintCoreUI2::DrvGetDriverSetting</strong></a></p></td>
<td><p>プリンターの機能とその他の内部情報の現在の状態を取得するための UI プラグインを有効にします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-drvupdateuisetting" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::DrvUpdateUISetting&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-drvupdateuisetting)"><strong>IPrintCoreUI2::DrvUpdateUISetting</strong></a></p></td>
<td><p>変更されたユーザー インターフェイスのオプションのドライバーに通知する UI プラグインを有効にします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-drvupgraderegistrysetting" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::DrvUpgradeRegistrySetting&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-drvupgraderegistrysetting)"><strong>IPrintCoreUI2::DrvUpgradeRegistrySetting</strong></a></p></td>
<td><p>プライベート レジストリの設定をアップグレードする OEM プラグインを有効にします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-enumconstrainedoptions" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::EnumConstrainedOptions&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-enumconstrainedoptions)"><strong>IPrintCoreUI2::EnumConstrainedOptions</strong></a></p></td>
<td><p>機能のオプションが制約を決定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-enumfeatures" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::EnumFeatures&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-enumfeatures)"><strong>IPrintCoreUI2::EnumFeatures</strong></a></p></td>
<td><p>プリンターの使用可能な機能を列挙します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-enumoptions" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::EnumOptions&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-enumoptions)"><strong>IPrintCoreUI2::EnumOptions</strong></a></p></td>
<td><p>特定の機能の使用可能なオプションを列挙します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-getfeatureattribute" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::GetFeatureAttribute&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-getfeatureattribute)"><strong>IPrintCoreUI2::GetFeatureAttribute</strong></a></p></td>
<td><p>機能の属性リストまたは特定の機能の属性の値を取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-getglobalattribute" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::GetGlobalAttribute&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-getglobalattribute)"><strong>IPrintCoreUI2::GetGlobalAttribute</strong></a></p></td>
<td><p>グローバル属性の一覧または特定のグローバル属性の値を取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-getoptionattribute" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::GetOptionAttribute&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-getoptionattribute)"><strong>IPrintCoreUI2::GetOptionAttribute</strong></a></p></td>
<td><p>オプションの属性リストまたは特定のオプションの属性の値を取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-getoptions" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::GetOptions&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-getoptions)"><strong>IPrintCoreUI2::GetOptions</strong></a></p></td>
<td><p>ドライバーの機能またはオプションのキーワードの組み合わせの一覧の形式で現在機能の設定を取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-querysimulationsupport" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::QuerySimulationSupport&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-querysimulationsupport)"><strong>IPrintCoreUI2::QuerySimulationSupport</strong></a></p></td>
<td><p>スプーラがサポートしているシミュレーションの種類を示す、スプーラーのシミュレーションの機能構造を取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-setoptions" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::SetOptions&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-setoptions)"><strong>IPrintCoreUI2::SetOptions</strong></a></p></td>
<td><p>ドライバーの機能の設定を設定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-whyconstrained" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::WhyConstrained&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-whyconstrained)"><strong>IPrintCoreUI2::WhyConstrained</strong></a></p></td>
<td><p>指定された機能またはオプションの選択範囲を制限する理由を判断します。</p></td>
</tr>
</tbody>
</table>

 

詳細については、次を参照してください。[プリンター ドライバーの COM インターフェイスを実装する](implementing-printer-driver-com-interfaces.md)します。

 

 




