---
title: ネットワーク プロトコルのインストール要件
description: ネットワーク プロトコルのインストール要件
ms.assetid: 6383fec5-29ce-4aa4-8fc3-c8d95f7bd02b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a4fa722cb138093cac03f394aa3928882326822
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324907"
---
# <a name="installation-requirements-for-network-protocols"></a>ネットワーク プロトコルのインストール要件





このトピックでは、ネットワーク プロトコルのインストール要件をまとめたものです。

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
<td align="left"><p><em>Hw id</em>の後にアンダー スコアと、製造元の名前または製品名、たとえば、プロバイダー名で構成する必要があります。MS_DLC.</p></td>
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
<td align="left"><p>［必須］:</p>
<p>Ndi キーを作成します。</p>
<p><a href="specifying-binding-interfaces.md" data-raw-source="[Specifying Binding Interfaces](specifying-binding-interfaces.md)">バインド インターフェイスを指定します。</a></p>
<p>バインド インターフェイスが可能な。</p>
<p><strong>UpperRange</strong>:</p>
<p>netbios, ipx, tdi, winsock, noupper</p>
<p><strong>LowerRange</strong>:</p>
<p>ndis5 ndisatm、nolower</p></td>
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
<td align="left"><p><a href="winsock-sections-in-a-network-inf-file.md" data-raw-source="[Winsock Sections](winsock-sections-in-a-network-inf-file.md)">Winsock セクション</a></p></td>
<td align="left"><p>省略可能</p></td>
<td align="left"><p>Winsock インターフェイスを提供するプロトコル、 <strong>Winsock インストール</strong>セクションが必要です、 <strong>Winsock 削除</strong>セクションは省略可能です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff547485" data-raw-source="[&lt;strong&gt;INF Strings Section&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547485)"><strong>INF 文字列 セクション</strong></a></p></td>
<td align="left"><p>必須</p></td>
<td align="left"><p>特定のネットワークの要件はありません。</p></td>
</tr>
</tbody>
</table>

 

 

 





