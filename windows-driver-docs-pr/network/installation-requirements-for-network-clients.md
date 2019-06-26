---
title: ネットワーク クライアントのインストール要件
description: ネットワーク クライアントのインストール要件
ms.assetid: 175f9006-d77b-41ff-875e-c64842ff5cb9
keywords:
- ネットワーク クライアントのインストール要件 WDK
- クライアントのインストール要件の WDK のネットワーク接続
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ebe2a520242b88cbc446889f319e9b5218a1f1f4
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393382"
---
# <a name="installation-requirements-for-network-clients"></a>ネットワーク クライアントのインストール要件





このトピックでは、ネットワーク クライアントのインストール要件をまとめたものです。

**注**  **NetClient**コンポーネントは Windows 8.1、Windows Server 2012 R2 で非推奨以降。

 

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
<td align="left"><p><strong>クラス</strong>NetClient を =</p>
<p><strong>ClassGuid</strong>= {4D36E973-E325-11CE-BFC1-08002BE10318}</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksnames-section" data-raw-source="[&lt;strong&gt;INF SourceDisksNames Section&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksnames-section)"><strong>INF SourceDisksNames セクション</strong></a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksfiles-section" data-raw-source="[&lt;strong&gt;INF SourceDisksFiles Section&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksfiles-section)"> <strong>INF SourceDisksFiles セクション</strong></a></p></td>
<td align="left"><p>必要な場合は.</p></td>
<td align="left"><p>INF ファイルは、Windows 2000 では配布されませんが必要です。 INF ファイルが Windows 2000 で分散している場合、 <strong>LayoutFile</strong>でエントリを指定する必要があります、<strong>バージョン</strong>セクション、および<strong>SourceDisksNames</strong>と<strong>SourceDisksFiles</strong>のセクションでは使用されません。</p>
<p>特定のネットワークの要件はありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section" data-raw-source="[&lt;strong&gt;INF DestinationDirs Section&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section)"><strong>INF DestinationDirs セクション</strong></a></p></td>
<td align="left"><p>必須</p></td>
<td align="left"><p>特定のネットワークの要件はありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="controlflags-section-in-a-network-inf-file.md" data-raw-source="[ControlFlags Section](controlflags-section-in-a-network-inf-file.md)">ControlFlags セクション</a></p></td>
<td align="left"><p>省略可能</p></td>
<td align="left"><p>特定のネットワークの要件はありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-manufacturer-section" data-raw-source="[&lt;strong&gt;INF Manufacturer Section&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/install/inf-manufacturer-section)"><strong>製造元の INF セクション</strong></a></p></td>
<td align="left"><p>必須</p></td>
<td align="left"><p>特定のネットワークの要件はありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="models-section-in-a-network-inf-file.md" data-raw-source="[Models Section](models-section-in-a-network-inf-file.md)">モデルのセクション</a></p></td>
<td align="left"><p>必須</p></td>
<td align="left"><p><em>Hw id</em>プロバイダー名がアンダー スコアと、製造元の名前または - 製品名の例で構成されている必要があります。MS_DLC.</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ddinstall-section-in-a-network-inf-file.md" data-raw-source="[DDInstall Section](ddinstall-section-in-a-network-inf-file.md)">DDInstall セクション</a></p></td>
<td align="left"><p>必須</p></td>
<td align="left"><p><strong>特性</strong>エントリ</p>
<p>許容される値:</p>
<p>NCF_HIDDEN</p>
<p>NCF_NO_SERVICE</p>
<p>NCF_NOT_USER_REMOVABLE</p>
<p>NCF_HAS_UI</p></td>
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
<p><a href="specifying-binding-interfaces.md" data-raw-source="[Specifying Binding Interfaces](specifying-binding-interfaces.md)">バインド インターフェイスを指定します。</a></p>
<p>バインド インターフェイスが可能な。</p>
<p>UpperRange: noupper</p>
<p><strong>LowerRange</strong>: ipx、tdi、winsock、netbios、nolower</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="add-registry-sections-in-a-network-inf-file.md" data-raw-source="[Add-registry-sections](add-registry-sections-in-a-network-inf-file.md)">Add-registry-sections</a></p></td>
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="setting-static-parameters.md" data-raw-source="[Setting static parameters for the component](setting-static-parameters.md)">コンポーネントの静的パラメーターを設定します。</a></p>
<p><a href="requiring-the-installation-of-another-network-component.md" data-raw-source="[Requiring the Installation of Another Network Component](requiring-the-installation-of-another-network-component.md)">別のネットワーク コンポーネントのインストールを要求します。</a></p>
<p><a href="adding-service-related-values-to-the-ndi-key.md" data-raw-source="[Specifying service-related values](adding-service-related-values-to-the-ndi-key.md)">サービスに関連する値を指定します。</a></p>
<p><a href="adding-a-helptext-value.md" data-raw-source="[Adding a HelpText Value](adding-a-helptext-value.md)">HelpText 値を追加します。</a></p>
<p><a href="adding-registry-values-for-a-notify-object.md" data-raw-source="[Adding Registry Values for a Notify Object](adding-registry-values-for-a-notify-object.md)">通知オブジェクトのレジストリ値を追加します。</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="remove-section-in-a-network-inf-file.md" data-raw-source="[Remove Section](remove-section-in-a-network-inf-file.md)">セクションを削除します。</a></p></td>
<td align="left"><p>省略可能</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><a href="networkprovider-and-printprovider-sections-in-a-network-inf-file.md" data-raw-source="[NetworkProvider and PrintProvider Sections](networkprovider-and-printprovider-sections-in-a-network-inf-file.md)">NetworkProvider とした PrintProvider セクション</a></p></td>
<td align="left"><p>必要な場合は.</p></td>
<td align="left"><p>必要なかどうかは、ネットワーク クライアントに対して、別のデバイス名が指定またはで使用するため、コンポーネントの短い名前が指定されて、 <strong>「net view</strong>コマンド。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="networkprovider-and-printprovider-sections-in-a-network-inf-file.md" data-raw-source="[NetworkProvider and PrintProvider Sections](networkprovider-and-printprovider-sections-in-a-network-inf-file.md)">NetworkProvider とした PrintProvider セクション</a></p></td>
<td align="left"><p>必要な場合は.</p></td>
<td align="left"><p>ネットワーク クライアントが、印刷プロバイダーが必要です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section" data-raw-source="[&lt;strong&gt;INF Strings Section&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section)"><strong>INF 文字列 セクション</strong></a></p></td>
<td align="left"><p>必須</p></td>
<td align="left"><p>特定のネットワークの要件はありません。</p></td>
</tr>
</tbody>
</table>

 

 

 





