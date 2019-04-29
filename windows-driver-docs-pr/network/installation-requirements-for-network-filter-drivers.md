---
title: ネットワーク フィルター ドライバーのインストール要件
description: ネットワーク フィルター ドライバーのインストール要件
ms.assetid: 7fb31e18-a2f0-48fe-b0a8-cf4aca7d27d5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cda84d8ae0a3435906738a902a68cdfbb0c70616
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324910"
---
# <a name="installation-requirements-for-network-filter-drivers"></a>ネットワーク フィルター ドライバーのインストール要件





このトピックでは、ネットワーク フィルター ドライバーの INF ファイルの要件をまとめたものです。 NDIS 6.0 以降では、フィルター ドライバーがサポートされています。 フィルター ドライバーをインストールする方法の詳細については、次を参照してください。 [NDIS フィルター ドライバーのインストール](ndis-filter-driver-installation.md)します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">INF ファイルのセクション</th>
<th align="left">状態</th>
<th align="left">コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="version-section-in-a-network-inf-file.md" data-raw-source="[Version Section](version-section-in-a-network-inf-file.md)">バージョン セクション</a></p></td>
<td align="left"><p>必須</p></td>
<td align="left"><p></p>
<strong>Class</strong>= NetService <strong>ClassGuid</strong>= {4D36E974-E325-11CE-BFC1-08002BE10318}</td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff547478" data-raw-source="[&lt;strong&gt;INF SourceDisksNames Section&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547478)"><strong>INF SourceDisksNames セクション</strong></a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff547472" data-raw-source="[&lt;strong&gt;INF SourceDisksFiles Section&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547472)"> <strong>INF SourceDisksFiles セクション</strong></a></p></td>
<td align="left"><p>省略可能</p></td>
<td align="left"><p>特定のネットワークの要件はありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff547383" data-raw-source="[&lt;strong&gt;INF DestinationDirs Section&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547383)"><strong>INF DestinationDirs セクション</strong></a></p></td>
<td align="left"><p>必須</p></td>
<td align="left"><p>特定のネットワークの要件はありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="controlflags-section-in-a-network-inf-file.md" data-raw-source="[ControlFlags Section](controlflags-section-in-a-network-inf-file.md)">ControlFlags セクション</a></p></td>
<td align="left"><p>省略可能</p></td>
<td align="left"><p>特定のネットワークの要件はありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff547454" data-raw-source="[&lt;strong&gt;INF Manufacturer Section&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547454)"><strong>製造元の INF セクション</strong></a></p></td>
<td align="left"><p>必須</p></td>
<td align="left"><p>特定のネットワークの要件はありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="models-section-in-a-network-inf-file.md" data-raw-source="[Models Section](models-section-in-a-network-inf-file.md)">モデルのセクション</a></p></td>
<td align="left"><p>必須</p></td>
<td align="left"><p><em>Hw id</em>の後にアンダー スコアと製造元名または製品名 (たとえば、MS_DLC)、プロバイダー名で構成する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ddinstall-section-in-a-network-inf-file.md" data-raw-source="[DDInstall Section](ddinstall-section-in-a-network-inf-file.md)">DDInstall セクション</a></p></td>
<td align="left"><p>必須</p></td>
<td align="left"><p><strong>特性</strong>エントリ。</p>
<p>NCF_LW_FILTER (0x40000) が設定されています。 フィルター ドライバーは、NCF_FILTER (0x400) フラグを設定しない必要があります。 NCF_ 値<em>Xxx</em> Netcfgx.h でフラグが定義されます。 NCF_ の詳細については<em>Xxx</em>フラグを参照してください<a href="ddinstall-section-in-a-network-inf-file.md" data-raw-source="[DDInstall Section in a Network INF File](ddinstall-section-in-a-network-inf-file.md)">ネットワーク INF ファイルで DDInstall セクション</a>します。</p>
<p>設定、 <strong>NetCfgInstanceId</strong>エントリ。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ddinstall-services-section-in-a-network-inf-file.md" data-raw-source="[DDInstall.Services Section](ddinstall-services-section-in-a-network-inf-file.md)">DDInstall.Services セクション</a></p></td>
<td align="left"><p>省略可能</p></td>
<td align="left"><p>特定のネットワークの要件はありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="add-registry-sections-in-a-network-inf-file.md" data-raw-source="[Add-registry-sections](add-registry-sections-in-a-network-inf-file.md)">Add-registry-sections</a></p></td>
<td align="left"><p>必須</p></td>
<td align="left"><p>Ndi キーを作成します。</p>
<p><strong>ServiceBinary</strong>内のエントリ、<strong>サービス インストール</strong>INF ファイルのセクションは、フィルター ドライバーのバイナリへのパスを指定します。</p>
<p>設定、 <strong>FilterType</strong>と<strong>FilterRunType</strong>します。 参照してください<a href="types-of-filter-drivers.md" data-raw-source="[Types of Filter Drivers](types-of-filter-drivers.md)">の種類のフィルター ドライバー</a>します。</p>
<p>設定、 <strong>UpperRange</strong>、 <strong>LowerRange</strong>、および<strong>FilterMediaTypes</strong>エントリ。 参照してください<a href="specifying-filter-driver-binding-relationships.md" data-raw-source="[Specifying Filter Driver Binding Relationships](specifying-filter-driver-binding-relationships.md)">フィルター ドライバーのバインディングの関係を指定する</a>します。</p>
<p>フィルターの主要なサービスの名前を指定、 <strong>CoServices</strong>属性。</p>
<p>指定、 <strong>FilterClass</strong>フィルターの変更のスタックの順序を決定します。 参照してください<a href="configuring-an-inf-file-for-a-modifying-filter-driver.md" data-raw-source="[Configuring an INF File for a Modifying Filter Driver](configuring-an-inf-file-for-a-modifying-filter-driver.md)">変更フィルター ドライバーの INF ファイルを構成する</a>します。</p>
<p>参照してください<a href="configuring-an-inf-file-for-a-monitoring-filter-driver.md" data-raw-source="[Configuring an INF File for a Monitoring Filter Driver](configuring-an-inf-file-for-a-monitoring-filter-driver.md)">監視フィルター ドライバーの INF ファイルを構成する</a>、 <a href="adding-service-related-values-to-the-ndi-key.md" data-raw-source="[Adding Service-Related Values to the Ndi Key](adding-service-related-values-to-the-ndi-key.md)">Ndi キーへのサービスに関連する値の追加</a>、および<a href="ddinstall-services-section-in-a-network-inf-file.md" data-raw-source="[DDInstall.Services Section in a Network INF File](ddinstall-services-section-in-a-network-inf-file.md)">ネットワーク INF ファイルで DDInstall.Services セクション</a>.</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="setting-static-parameters.md" data-raw-source="[Setting static parameters for the component](setting-static-parameters.md)">コンポーネントの静的パラメーターを設定します。</a></p>
<p><a href="requiring-the-installation-of-another-network-component.md" data-raw-source="[Requiring the Installation of Another Network Component](requiring-the-installation-of-another-network-component.md)">別のネットワーク コンポーネントのインストールを要求します。</a></p>
<p><a href="adding-a-helptext-value.md" data-raw-source="[Adding a HelpText Value](adding-a-helptext-value.md)">HelpText 値を追加します。</a></p>
<p><a href="adding-registry-values-for-a-notify-object.md" data-raw-source="[Adding Registry Values for a Notify Object](adding-registry-values-for-a-notify-object.md)">通知オブジェクトのレジストリ値を追加します。</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="remove-section-in-a-network-inf-file.md" data-raw-source="[Remove Section](remove-section-in-a-network-inf-file.md)">セクションを削除します。</a></p></td>
<td align="left"><p>省略可能</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff547485" data-raw-source="[&lt;strong&gt;INF Strings Section&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547485)"><strong>INF 文字列 セクション</strong></a></p></td>
<td align="left"><p>必須</p></td>
<td align="left"><p>特定のネットワークの要件はありません。</p></td>
</tr>
</tbody>
</table>

 

 

 





