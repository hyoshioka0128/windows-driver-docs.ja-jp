---
title: ネットワーク MUX 中間ドライバーのインストール要件
description: ネットワーク MUX 中間ドライバーのインストール要件
ms.assetid: 2c51c40a-2015-4131-9ffa-6956313183f5
keywords:
- MUX WDK 中間ドライバー インストールの要件
- INF ファイル WDK ネットワークをプロトコルします。
- デバイス INF ファイル WDK ネットワー キング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd70fe2fe83d5f8f34800b6fd7fa722616a9da33
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578668"
---
# <a name="installation-requirements-for-network-mux-intermediate-drivers"></a>ネットワーク MUX 中間ドライバーのインストール要件





このトピックでは、ネットワーク MUX 中間ドライバーのインストール要件をまとめたものです。 MUX 中間ドライバーのインストール要件の詳細については、[中間ドライバーをインストールする](installing-an-intermediate-driver.md)を参照してください。

ネットワーク MUX 中間ドライバーをインストールするには、2 つの INF ファイルが必要です。

-   ドライバーのプロトコル (**クラス**NetTrans =)

-   ドライバーのデバイス (**クラス**= Net)

### <a name="protocol-inf-file-for-a-network-mux-intermediate-driver"></a>プロトコルのネットワーク MUX 中間ドライバーの INF ファイル

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
<td align="left"><p><strong>クラス</strong>NetTrans を =</p>
<p><strong>ClassGuid</strong>= {4D36E975-E325-11CE-BFC1-08002BE10318}</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff547478" data-raw-source="[&lt;strong&gt;INF SourceDisksNames Section&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547478)"><strong>INF SourceDisksNames セクション</strong></a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff547472" data-raw-source="[&lt;strong&gt;INF SourceDisksFiles Section&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547472)"> <strong>INF SourceDisksFiles セクション</strong></a></p></td>
<td align="left"><p>必要な場合は.</p></td>
<td align="left"><p>INF ファイルは、Windows 2000 では配布されませんが必要です。 INF ファイルが Windows 2000 で分散している場合、 <strong>LayoutFile</strong>でエントリを指定する必要があります、<strong>バージョン</strong>セクション、および<strong>SourceDisksNames</strong>と<strong>SourceDisksFiles</strong>のセクションでは使用されません。</p>
<p>特定のネットワークの要件はありません。</p></td>
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
<td align="left"><p><em>Hw id</em>プロバイダー名がアンダー スコアと、製造元の名前または - 製品名の例で構成されている必要があります。MS_DLC.</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ddinstall-section-in-a-network-inf-file.md" data-raw-source="[DDInstall Section](ddinstall-section-in-a-network-inf-file.md)">DDInstall セクション</a></p></td>
<td align="left"><p>必須</p></td>
<td align="left"><p><strong>特性</strong>エントリ。</p>
<p>NCF_HAS_UI が必要です。</p>
<p>デバイスの INF は、INF のシステム ディレクトリにコピーする必要がありますを参照してください<a href="https://msdn.microsoft.com/library/windows/hardware/ff540117" data-raw-source="[Copying INFs](https://msdn.microsoft.com/library/windows/hardware/ff540117)">コピー Inf</a>します。</p></td>
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
<p>UpperRange:</p>
<p>noupper</p>
<p><strong>LowerRange</strong>:</p>
<p>イーサネット、atm、トークン リング、シリアル、fddi、ベースバンド、ブロード バンド、arcnet、isdn、localtalk、wan します。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff547485" data-raw-source="[&lt;strong&gt;INF Strings Section&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547485)"><strong>INF 文字列 セクション</strong></a></p></td>
<td align="left"><p>必須</p></td>
<td align="left"><p>特定のネットワークの要件はありません。</p></td>
</tr>
</tbody>
</table>

 

### <a name="device-inf-file-for-a-network-mux-intermediate-driver"></a>デバイスの INF ファイル、ネットワーク MUX 中間ドライバー

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
<td align="left"><p><strong>クラス</strong>Net を =</p>
<p><strong>ClassGuid</strong>= {4D36E972-E325-11CE-BFC1-08002BE10318}</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="controlflags-section-in-a-network-inf-file.md" data-raw-source="[ControlFlags Section](controlflags-section-in-a-network-inf-file.md)">ControlFlags セクション</a></p></td>
<td align="left"><p>必須</p></td>
<td align="left"><p>このセクションを含める必要があります、 <strong>ExcludeFromSelect</strong>デバイスのエントリ。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff547454" data-raw-source="[&lt;strong&gt;INF Manufacturer Section&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547454)"><strong>製造元の INF セクション</strong></a></p></td>
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
<td align="left"><p><strong>特性</strong>エントリ。</p>
<p>NCF_VIRTUAL が必要です。 NCF_HIDDEN と NCF_NOT_USER_REMOVABLE は省略可能です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ddinstall-services-section-in-a-network-inf-file.md" data-raw-source="[DDInstall.Services Section](ddinstall-services-section-in-a-network-inf-file.md)">DDInstall.Services セクション</a></p></td>
<td align="left"><p>必須</p></td>
<td align="left"><p>特定のネットワークの要件はありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="add-registry-sections-in-a-network-inf-file.md" data-raw-source="[Add-registry-sections](add-registry-sections-in-a-network-inf-file.md)">Add-registry-sections</a></p></td>
<td align="left"><p>必須</p></td>
<td align="left"><p>Ndi キーを作成します。</p>
<p><a href="adding-service-related-values-to-the-ndi-key.md" data-raw-source="[Specifying service-related values](adding-service-related-values-to-the-ndi-key.md)">サービスに関連する値を指定します。</a></p>
<p><a href="specifying-binding-interfaces.md" data-raw-source="[Specifying Binding Interfaces](specifying-binding-interfaces.md)">バインド インターフェイスを指定します。</a></p>
<p>バインド インターフェイスが可能な。</p>
<p><strong>UpperRange</strong>:</p>
<p>ndis5, ndisatm, ndiswan, ndiscowan, noupper, ndis5_atalk, ndis5_dlc, ndis5_ip, ndis5_ipx, ndis5_nbf, ndis5_streams</p>
<p>LowerRange:</p>
<p>nolower</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="setting-static-parameters.md" data-raw-source="[Setting static parameters for the component](setting-static-parameters.md)">コンポーネントの静的パラメーターを設定します。</a></p>
<p><a href="requiring-the-installation-of-another-network-component.md" data-raw-source="[Requiring the Installation of Another Network Component](requiring-the-installation-of-another-network-component.md)">別のネットワーク コンポーネントのインストールを要求します。</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff547485" data-raw-source="[&lt;strong&gt;INF Strings Section&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547485)"><strong>INF 文字列 セクション</strong></a></p></td>
<td align="left"><p>必須</p></td>
<td align="left"><p>特定のネットワークの要件はありません。</p></td>
</tr>
</tbody>
</table>

 

 

 





