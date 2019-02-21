---
title: IPrintCoreUI2 COM インターフェイス
description: IPrintCoreUI2 COM インターフェイス
ms.assetid: 3c9df0ac-d823-4c27-bd34-85765f48b972
keywords:
- IPrintCoreUI2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04d4d2f522fe96544211ee643024c70b6620e673
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551338"
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553036" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::DrvGetDriverSetting&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553036)"><strong>IPrintCoreUI2::DrvGetDriverSetting</strong></a></p></td>
<td><p>プリンターの機能とその他の内部情報の現在の状態を取得するための UI プラグインを有効にします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553039" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::DrvUpdateUISetting&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553039)"><strong>IPrintCoreUI2::DrvUpdateUISetting</strong></a></p></td>
<td><p>変更されたユーザー インターフェイスのオプションのドライバーに通知する UI プラグインを有効にします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553041" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::DrvUpgradeRegistrySetting&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553041)"><strong>IPrintCoreUI2::DrvUpgradeRegistrySetting</strong></a></p></td>
<td><p>プライベート レジストリの設定をアップグレードする OEM プラグインを有効にします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553045" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::EnumConstrainedOptions&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553045)"><strong>IPrintCoreUI2::EnumConstrainedOptions</strong></a></p></td>
<td><p>機能のオプションが制約を決定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553050" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::EnumFeatures&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553050)"><strong>IPrintCoreUI2::EnumFeatures</strong></a></p></td>
<td><p>プリンターを列挙&#39;s の使用可能な機能です。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553052" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::EnumOptions&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553052)"><strong>IPrintCoreUI2::EnumOptions</strong></a></p></td>
<td><p>特定の機能の使用可能なオプションを列挙します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553056" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::GetFeatureAttribute&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553056)"><strong>IPrintCoreUI2::GetFeatureAttribute</strong></a></p></td>
<td><p>機能の属性リストまたは特定の機能の属性の値を取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553059" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::GetGlobalAttribute&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553059)"><strong>IPrintCoreUI2::GetGlobalAttribute</strong></a></p></td>
<td><p>グローバル属性の一覧または特定のグローバル属性の値を取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553064" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::GetOptionAttribute&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553064)"><strong>IPrintCoreUI2::GetOptionAttribute</strong></a></p></td>
<td><p>オプションの属性リストまたは特定のオプションの属性の値を取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553069" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::GetOptions&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553069)"><strong>IPrintCoreUI2::GetOptions</strong></a></p></td>
<td><p>ドライバーを取得します。&#39;s 機能またはオプションのキーワードの組み合わせの一覧の形式で現在機能の設定。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553074" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::QuerySimulationSupport&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553074)"><strong>IPrintCoreUI2::QuerySimulationSupport</strong></a></p></td>
<td><p>スプーラがサポートしているシミュレーションの種類を示す、スプーラーのシミュレーションの機能構造を取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553081" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::SetOptions&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553081)"><strong>IPrintCoreUI2::SetOptions</strong></a></p></td>
<td><p>ドライバーの設定&#39;s 機能の設定。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553087" data-raw-source="[&lt;strong&gt;IPrintCoreUI2::WhyConstrained&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553087)"><strong>IPrintCoreUI2::WhyConstrained</strong></a></p></td>
<td><p>指定された機能またはオプションの選択範囲を制限する理由を判断します。</p></td>
</tr>
</tbody>
</table>

 

詳細については、次を参照してください。[プリンター ドライバーの COM インターフェイスを実装する](implementing-printer-driver-com-interfaces.md)します。

 

 




