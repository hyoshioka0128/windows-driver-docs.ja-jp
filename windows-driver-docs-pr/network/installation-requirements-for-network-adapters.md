---
title: ネットワーク アダプターのインストール要件
description: ネットワーク アダプターのインストール要件
ms.assetid: 682a262a-a712-4fab-a753-d0c6fc08bac8
keywords:
- ネットワーク アダプターのインストール要件 WDK
- アダプターの WDK ネットワー キング、インストール要件
- WAN WDK は、ネットワーク アダプターのインストール要件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1acbeac904781f26c3aab1e721f706b33c39732b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324918"
---
# <a name="installation-requirements-for-network-adapters"></a>ネットワーク アダプターのインストール要件





このトピックでは、ネットワーク アダプターのインストール要件をまとめたものです。

**注**  NDIS 6.0 とそれ以降のドライバーのセットをサポートする[標準化されているネットワーク デバイスの INF キーワード](standardized-inf-keywords-for-network-devices.md)します。

 

### <a name="general-requirements"></a>一般的な要件

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
<td align="left"><p>必須</p></td>
<td align="left"><p>含める必要があります、 <strong>ExcludeFromSelect</strong> INF ファイルによってインストールされている各プラグ アンド プレイ (PnP) アダプターのエントリ。</p>
<p>非 PnP ISA および EISA アダプターなどの非 PnP のアダプターの一覧を表示しない必要があります。 Windows XP およびそれ以降のオペレーティング システムはサポートされていないことおよび EISA アダプター非 PnP ISA アダプターに注意してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff547454" data-raw-source="[&lt;strong&gt;INF Manufacturer Section&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547454)"><strong>製造元の INF セクション</strong></a></p></td>
<td align="left"><p>必須</p></td>
<td align="left"><p>特定のネットワークの要件はありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="models-section-in-a-network-inf-file.md" data-raw-source="[Models Section](models-section-in-a-network-inf-file.md)">モデルのセクション</a></p></td>
<td align="left"><p>必須</p></td>
<td align="left"><p><em>Hw id</em> PnP マネージャーにアダプターによって提供される、ハードウェア ID が一致する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ddinstall-section-in-a-network-inf-file.md" data-raw-source="[DDInstall Section](ddinstall-section-in-a-network-inf-file.md)">DDInstall セクション</a></p></td>
<td align="left"><p>必須</p></td>
<td align="left"><p><strong>特性</strong>エントリ</p>
<p>許容される値:</p>
<p>NCF_VIRTUAL、</p>
<p>NCF_SOFTWARE_ENUMERATED, NCF_PHYSICAL, NCF_MULTIPORT_INSTANCED_ADAPTER, NCF_HAS_UI, NCF_HIDDEN, NCF_NOT_USER_REMOVABLE</p>
<p>NCF_VIRTUAL、NCF_SOFTWARE_ENUMERATED、および NCF_PHYSICAL は相互に排他的です。</p>
<p><strong>BusType</strong>エントリが物理アダプターに必要です。</p>
<p><strong>EisaCompressedId</strong>エントリは EISA アダプターの必須です。 このエントリは、EISA 圧縮の ID と、アダプターのアダプター マスクの両方を指定します。 Windows XP およびそれ以降のオペレーティング システムでは、EISA アダプターはサポートされません。</p>
<p>A <strong>Port1DeviceNumber</strong>または<strong>Port1FunctionNumber</strong>エントリがマルチポートのネットワーク アダプターに必要です。</p></td>
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
<p><a href="specifying-bundle-membership.md" data-raw-source="[Specifying Bundle Membership](specifying-bundle-membership.md)">バンドルのメンバーシップを指定する</a>(だけの LBFO ミニポート ドライバー)</p>
<p><a href="specifying-binding-interfaces.md" data-raw-source="[Specifying Binding Interfaces](specifying-binding-interfaces.md)">バインド インターフェイスを指定します。</a></p>
<p>バインド インターフェイスが可能な。</p>
<p><strong>UpperRange</strong>:</p>
<p>ndis5, ndisatm, ndiswan, ndiscowan, noupper, ndis5_atalk, ndis5_dlc, ndis5_ip, ndis5_ipx, ndis5_nbf, ndis5_streams</p>
<p><strong>LowerRange</strong>:</p>
<p>イーサネット、atm、トークン リング、シリアル、fddi、ベースバンド、ブロード バンド、arcnet、isdn、localtalk、wan します。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>省略可能</p></td>
<td align="left"><p><a href="setting-static-parameters.md" data-raw-source="[Setting static parameters for the component](setting-static-parameters.md)">コンポーネントの静的パラメーターを設定します。</a></p>
<p><a href="requiring-the-installation-of-another-network-component.md" data-raw-source="[Requiring the Installation of Another Network Component](requiring-the-installation-of-another-network-component.md)">別のネットワーク コンポーネントのインストールを要求します。</a></p>
<p><a href="specifying-configuration-parameters-for-the-advanced-properties-page.md" data-raw-source="[Specifying Configuration Parameters for the Advanced Properties Page](specifying-configuration-parameters-for-the-advanced-properties-page.md)">高度なプロパティ ページの構成パラメーターの指定</a></p>
<p><a href="specifying-custom-property-pages-for-network-adapters.md" data-raw-source="[Specifying Custom Property Pages for Network Adapters](specifying-custom-property-pages-for-network-adapters.md)">ネットワーク アダプターのカスタム プロパティ ページを指定します。</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff547485" data-raw-source="[&lt;strong&gt;INF Strings Section&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547485)"><strong>INF 文字列 セクション</strong></a></p></td>
<td align="left"><p>必須</p></td>
<td align="left"><p>特定のネットワークの要件はありません。</p></td>
</tr>
</tbody>
</table>

 

### <a name="additional-requirements-for-wan-adapters"></a>WAN アダプターの追加要件

WAN アダプターでは、次のトピックで説明されている追加のインストール要件があります。

[WAN アダプターの WAN のエンドポイントを指定します。](specifying-wan-endpoints-for-a-wan-adapter.md)

[ISDN アダプターの ISDN キーと値を指定します。](specifying-isdn-keys-and-values-for-an-isdn-adapter.md)

[マルチ プロトコルの WAN NIC をインストールします。](installing-a-multiprotocol-wan-nic.md)

**注**  、[セクションの削除](remove-section-in-a-network-inf-file.md)と[ネットワーク コンポーネントのオブジェクトの通知](notify-objects-for-network-components.md)はサポートされていません。

 

 

 





