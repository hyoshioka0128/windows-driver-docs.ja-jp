---
title: IP ヘルパー
description: IP ヘルパー
ms.assetid: c7cf1f47-ee0d-4c89-883b-717b719fcc2a
keywords:
- IP ヘルパー WDK ネットワーク
- ネットワーク、約 IP ヘルパー WDK
- ネットワーク ドライバー WDK、IP ヘルパー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cf2962bb108677e8254c9e7637b14749d850d44
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372592"
---
# <a name="ip-helper"></a>IP ヘルパー





インターネット プロトコル ヘルパー (IP ヘルパー) は、ローカル コンピューターのネットワークの構成に関する情報を取得し、その構成を変更するドライバーを使用できます。 IP ヘルパーには、ローカル コンピューターの特定の側面のネットワーク構成の変更時に、ドライバーに通知するかどうかを確認する通知メカニズムも提供します。 IP ヘルパーは、Windows Vista と Microsoft Windows オペレーティング システムの以降のバージョンで使用できます。

IP ヘルパー関数の多くは、管理情報ベース (MIB) テクノロジに関連付けられているデータ型を表す構造体のパラメーターを渡します。 IP ヘルパー関数では、これらの MIB 構造体を使用して、さまざまなネットワー キング情報を表します。

IP ヘルパー ドキュメント「アダプター」という用語を使用して広範な「インターフェイス」とします。 *アダプター*の省略形になっている従来の用語は、*ネットワーク アダプター*、本来の何らかの形式のネットワーク ハードウェアを参照します。 アダプターは、データ リンク レベルの抽象化です。

*インターフェイス*をリンクするノードの添付ファイルを表す抽象概念として、IETF RFC ドキュメントに記載されています。 インターフェイスは、IP レベルの抽象化です。

ドライバーを取得し、ローカル コンピューター上の伝送制御プロトコル/インターネット プロトコル (TCP/IP) のトランスポートの構成設定を変更する次のカーネル モード関数、MIB 構造体、および MIB およびネットワーク レイヤー (NL) 列挙を使用できます。

**注**  ドライバーのコードを開発するための手順に従います[ヘッダー ファイルをインクルードします。](including-header-files-for-ip-helper.md)

 

### <a name="interface-conversion-functions"></a>変換関数をインターフェイスします。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546130(v=vs.85)" data-raw-source="[&lt;strong&gt;ConvertInterfaceAliasToLuid&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546130(v=vs.85))"><strong>ConvertInterfaceAliasToLuid</strong></a></p></td>
<td align="left"><p>ネットワーク インターフェイスは Unicode インターフェイス名のローカル一意識別子 (LUID) に変換します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546137(v=vs.85)" data-raw-source="[&lt;strong&gt;ConvertInterfaceGuidToLuid&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546137(v=vs.85))"><strong>ConvertInterfaceGuidToLuid</strong></a></p></td>
<td align="left"><p>インターフェイスの LUID にネットワーク インターフェイスのグローバル一意識別子 (GUID) に変換します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546141(v=vs.85)" data-raw-source="[&lt;strong&gt;ConvertInterfaceIndexToLuid&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546141(v=vs.85))"><strong>ConvertInterfaceIndexToLuid</strong></a></p></td>
<td align="left"><p>インターフェイスの LUID には、ネットワーク インターフェイスのローカル インデックスを変換します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546151(v=vs.85)" data-raw-source="[&lt;strong&gt;ConvertInterfaceLuidToAlias&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546151(v=vs.85))"><strong>ConvertInterfaceLuidToAlias</strong></a></p></td>
<td align="left"><p>ネットワーク インターフェイスの LUID をインターフェイスのエイリアスに変換します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546156(v=vs.85)" data-raw-source="[&lt;strong&gt;ConvertInterfaceLuidToGuid&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546156(v=vs.85))"><strong>ConvertInterfaceLuidToGuid</strong></a></p></td>
<td align="left"><p>ネットワーク インターフェイスの LUID をインターフェイスの GUID に変換します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546167(v=vs.85)" data-raw-source="[&lt;strong&gt;ConvertInterfaceLuidToIndex&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546167(v=vs.85))"><strong>ConvertInterfaceLuidToIndex</strong></a></p></td>
<td align="left"><p>ネットワーク インターフェイスの LUID をインターフェイスのローカルのインデックスに変換します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546171(v=vs.85)" data-raw-source="[&lt;strong&gt;ConvertInterfaceLuidToNameA&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546171(v=vs.85))"><strong>ConvertInterfaceLuidToNameA</strong></a></p></td>
<td align="left"><p>ネットワーク インターフェイスの LUID を ANSI にインターフェイス名に変換します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546175(v=vs.85)" data-raw-source="[&lt;strong&gt;ConvertInterfaceLuidToNameW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546175(v=vs.85))"><strong>ConvertInterfaceLuidToNameW</strong></a></p></td>
<td align="left"><p>ネットワーク インターフェイスの LUID を Unicode にインターフェイス名に変換します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546185(v=vs.85)" data-raw-source="[&lt;strong&gt;ConvertInterfaceNameToLuidA&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546185(v=vs.85))"><strong>ConvertInterfaceNameToLuidA</strong></a></p></td>
<td align="left"><p>インターフェイスの LUID ANSI ネットワーク インターフェイス名に変換します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546192(v=vs.85)" data-raw-source="[&lt;strong&gt;ConvertInterfaceNameToLuidW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546192(v=vs.85))"><strong>ConvertInterfaceNameToLuidW</strong></a></p></td>
<td align="left"><p>インターフェイスの LUID には、Unicode のネットワーク インターフェイス名を変換します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553785(v=vs.85)" data-raw-source="[&lt;strong&gt;if_indextoname&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553785(v=vs.85))"><strong>if_indextoname</strong></a></p></td>
<td align="left"><p>ローカル ネットワーク インターフェイスのインデックスを ANSI にインターフェイス名に変換します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553788(v=vs.85)" data-raw-source="[&lt;strong&gt;if_nametoindex&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553788(v=vs.85))"><strong>if_nametoindex</strong></a></p></td>
<td align="left"><p>ネットワーク インターフェイスの ANSI インターフェイス名をローカル インターフェイスのインデックスに変換します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="interface-management-functions"></a>インターフェイス管理関数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552517(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIfEntry2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552517(v=vs.85))"><strong>GetIfEntry2</strong></a></p></td>
<td align="left"><p>ローカル コンピューターの指定されたインターフェイスの情報を取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552521(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIfStackTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552521(v=vs.85))"><strong>GetIfStackTable</strong></a></p></td>
<td align="left"><p>インターフェイスのスタックに対してネットワーク インターフェイスの関係を指定するネットワーク インターフェイス スタック行エントリのテーブルを取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552524(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIfTable2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552524(v=vs.85))"><strong>GetIfTable2</strong></a></p></td>
<td align="left"><p>MIB-II インターフェイス テーブルを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552528(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIfTable2Ex&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552528(v=vs.85))"><strong>GetIfTable2Ex</strong></a></p></td>
<td align="left"><p>取得するインターフェイスの情報のレベルに MIB-II インターフェイス テーブルを取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552531(v=vs.85)" data-raw-source="[&lt;strong&gt;GetInvertedIfStackTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552531(v=vs.85))"><strong>GetInvertedIfStackTable</strong></a></p></td>
<td align="left"><p>インターフェイスのスタックに対してネットワーク インターフェイスの関係を指定する反転したネットワーク インターフェイス スタック行エントリのテーブルを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552540(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIpInterfaceEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552540(v=vs.85))"><strong>GetIpInterfaceEntry</strong></a></p></td>
<td align="left"><p>ローカル コンピューターの指定されたインターフェイスの IP の情報を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552543(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIpInterfaceTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552543(v=vs.85))"><strong>GetIpInterfaceTable</strong></a></p></td>
<td align="left"><p>ローカル コンピューターの IP インターフェイスのエントリを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554883(v=vs.85)" data-raw-source="[&lt;strong&gt;InitializeIpInterfaceEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554883(v=vs.85))"><strong>InitializeIpInterfaceEntry</strong></a></p></td>
<td align="left"><p>メンバーは初期化、 <a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559254(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IPINTERFACE_ROW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559254(v=vs.85))"> <strong>MIB_IPINTERFACE_ROW</strong> </a>既定値を持つエントリを構造体します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570774(v=vs.85)" data-raw-source="[&lt;strong&gt;SetIpInterfaceEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570774(v=vs.85))"><strong>SetIpInterfaceEntry</strong></a></p></td>
<td align="left"><p>ローカル コンピューターの IP インターフェイスのプロパティを設定します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="ip-address-management-functions"></a>IP アドレスの管理機能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546204(v=vs.85)" data-raw-source="[&lt;strong&gt;CreateAnycastIpAddressEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546204(v=vs.85))"><strong>CreateAnycastIpAddressEntry</strong></a></p></td>
<td align="left"><p>ローカル コンピューターの新しいエニー キャスト IP アドレスのエントリを追加します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546219(v=vs.85)" data-raw-source="[&lt;strong&gt;CreateSortedAddressPairs&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546219(v=vs.85))"><strong>CreateSortedAddressPairs</strong></a></p></td>
<td align="left"><p>ペアと共に、ホスト マシンのローカル IP アドレスし、の通信の優先順位に従ってペアの並べ替え変換先の指定された一覧に対処します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546227(v=vs.85)" data-raw-source="[&lt;strong&gt;CreateUnicastIpAddressEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546227(v=vs.85))"><strong>CreateUnicastIpAddressEntry</strong></a></p></td>
<td align="left"><p>ローカル コンピューターのユニキャスト IP アドレスの新しいエントリを追加します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546363(v=vs.85)" data-raw-source="[&lt;strong&gt;DeleteAnycastIpAddressEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546363(v=vs.85))"><strong>DeleteAnycastIpAddressEntry</strong></a></p></td>
<td align="left"><p>ローカル コンピューターの既存のエニー キャスト IP アドレス エントリを削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546370(v=vs.85)" data-raw-source="[&lt;strong&gt;DeleteUnicastIpAddressEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546370(v=vs.85))"><strong>DeleteUnicastIpAddressEntry</strong></a></p></td>
<td align="left"><p>ローカル コンピューターから既存のユニキャスト IP アドレスのエントリを削除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552504(v=vs.85)" data-raw-source="[&lt;strong&gt;GetAnycastIpAddressEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552504(v=vs.85))"><strong>GetAnycastIpAddressEntry</strong></a></p></td>
<td align="left"><p>ローカル コンピューターの既存のエニー キャスト IP アドレスのエントリの情報を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552508(v=vs.85)" data-raw-source="[&lt;strong&gt;GetAnycastIpAddressTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552508(v=vs.85))"><strong>GetAnycastIpAddressTable</strong></a></p></td>
<td align="left"><p>ローカル コンピューター上のエニー キャスト IP アドレス テーブルを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552565(v=vs.85)" data-raw-source="[&lt;strong&gt;GetMulticastIpAddressEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552565(v=vs.85))"><strong>GetMulticastIpAddressEntry</strong></a></p></td>
<td align="left"><p>ローカル コンピューターの既存の IP マルチキャスト アドレス エントリの情報を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552570(v=vs.85)" data-raw-source="[&lt;strong&gt;GetMulticastIpAddressTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552570(v=vs.85))"><strong>GetMulticastIpAddressTable</strong></a></p></td>
<td align="left"><p>ローカル コンピューター上のマルチキャスト IP アドレス テーブルを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552589(v=vs.85)" data-raw-source="[&lt;strong&gt;GetUnicastIpAddressEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552589(v=vs.85))"><strong>GetUnicastIpAddressEntry</strong></a></p></td>
<td align="left"><p>ローカル コンピューターの既存のユニキャスト IP アドレスのエントリの情報を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552594(v=vs.85)" data-raw-source="[&lt;strong&gt;GetUnicastIpAddressTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552594(v=vs.85))"><strong>GetUnicastIpAddressTable</strong></a></p></td>
<td align="left"><p>ローカル コンピューターのユニキャスト IP アドレス テーブルを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554886(v=vs.85)" data-raw-source="[&lt;strong&gt;InitializeUnicastIpAddressEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554886(v=vs.85))"><strong>InitializeUnicastIpAddressEntry</strong></a></p></td>
<td align="left"><p>初期化します、 <a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559308(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_UNICASTIPADDRESS_ROW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559308(v=vs.85))"> <strong>MIB_UNICASTIPADDRESS_ROW</strong> </a>ローカル コンピューター上のユニキャスト IP アドレスのエントリの既定の値構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568807(v=vs.85)" data-raw-source="[&lt;strong&gt;NotifyStableUnicastIpAddressTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568807(v=vs.85))"><strong>NotifyStableUnicastIpAddressTable</strong></a></p></td>
<td align="left"><p>ローカル コンピューター上の固定のユニキャスト IP アドレス テーブルを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570800(v=vs.85)" data-raw-source="[&lt;strong&gt;SetUnicastIpAddressEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570800(v=vs.85))"><strong>SetUnicastIpAddressEntry</strong></a></p></td>
<td align="left"><p>ローカル コンピューターの既存のユニキャスト IP アドレスのエントリのプロパティを設定します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="ip-neighbor-address-management-functions"></a>IP の近隣ノード アドレスの管理機能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546217(v=vs.85)" data-raw-source="[&lt;strong&gt;CreateIpNetEntry2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546217(v=vs.85))"><strong>CreateIpNetEntry2</strong></a></p></td>
<td align="left"><p>ローカル コンピューターの新しい近隣 IP アドレスのエントリを作成します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546368(v=vs.85)" data-raw-source="[&lt;strong&gt;DeleteIpNetEntry2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546368(v=vs.85))"><strong>DeleteIpNetEntry2</strong></a></p></td>
<td align="left"><p>ローカル コンピューターから、近隣ノードの IP アドレスのエントリを削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550029(v=vs.85)" data-raw-source="[&lt;strong&gt;FlushIpNetTable2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550029(v=vs.85))"><strong>FlushIpNetTable2</strong></a></p></td>
<td align="left"><p>ローカル コンピューターの IP の近隣ノード テーブルをフラッシュします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552546(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIpNetEntry2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552546(v=vs.85))"><strong>GetIpNetEntry2</strong></a></p></td>
<td align="left"><p>ローカル コンピューターの近隣ノードの IP アドレスのエントリの情報を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552551(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIpNetTable2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552551(v=vs.85))"><strong>GetIpNetTable2</strong></a></p></td>
<td align="left"><p>ローカル コンピューターの IP の近隣ノード テーブルを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570686(v=vs.85)" data-raw-source="[&lt;strong&gt;ResolveIpNetEntry2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570686(v=vs.85))"><strong>ResolveIpNetEntry2</strong></a></p></td>
<td align="left"><p>ローカル コンピューターの近隣ノード IP アドレスのエントリの物理アドレスを解決します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570775(v=vs.85)" data-raw-source="[&lt;strong&gt;SetIpNetEntry2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570775(v=vs.85))"><strong>SetIpNetEntry2</strong></a></p></td>
<td align="left"><p>ローカル コンピューターの近隣ノード IP アドレスのエントリは、既存の物理アドレスを設定します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="ip-path-management-functions"></a>IP のパスの管理機能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550031(v=vs.85)" data-raw-source="[&lt;strong&gt;FlushIpPathTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550031(v=vs.85))"><strong>FlushIpPathTable</strong></a></p></td>
<td align="left"><p>ローカル コンピューターの IP のパスのテーブルをフラッシュします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552556(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIpPathEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552556(v=vs.85))"><strong>GetIpPathEntry</strong></a></p></td>
<td align="left"><p>ローカル コンピューターの IP パスのエントリの情報を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552559(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIpPathTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552559(v=vs.85))"><strong>GetIpPathTable</strong></a></p></td>
<td align="left"><p>ローカル コンピューターの IP パスのエントリの情報を取得します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="ip-route-management-functions"></a>IP のルートの管理機能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546209(v=vs.85)" data-raw-source="[&lt;strong&gt;CreateIpForwardEntry2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546209(v=vs.85))"><strong>CreateIpForwardEntry2</strong></a></p></td>
<td align="left"><p>ローカル コンピューターの新しい IP ルート エントリを作成します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546365(v=vs.85)" data-raw-source="[&lt;strong&gt;DeleteIpForwardEntry2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546365(v=vs.85))"><strong>DeleteIpForwardEntry2</strong></a></p></td>
<td align="left"><p>ローカル コンピューターからの IP のルート エントリを削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552511(v=vs.85)" data-raw-source="[&lt;strong&gt;GetBestRoute2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552511(v=vs.85))"><strong>GetBestRoute2</strong></a></p></td>
<td align="left"><p>最適なルート指定の宛先 IP アドレスをローカル コンピューターの IP のルート エントリを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552535(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIpForwardEntry2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552535(v=vs.85))"><strong>GetIpForwardEntry2</strong></a></p></td>
<td align="left"><p>ローカル コンピューターの IP のルート エントリの情報を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552536(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIpForwardTable2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552536(v=vs.85))"><strong>GetIpForwardTable2</strong></a></p></td>
<td align="left"><p>ローカル コンピューターの IP のルート エントリを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554882(v=vs.85)" data-raw-source="[&lt;strong&gt;InitializeIpForwardEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554882(v=vs.85))"><strong>InitializeIpForwardEntry</strong></a></p></td>
<td align="left"><p>初期化します、 <a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559245(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IPFORWARD_ROW2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559245(v=vs.85))"> <strong>MIB_IPFORWARD_ROW2</strong> </a>ローカル コンピューターの IP のルート エントリの既定の値構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570773(v=vs.85)" data-raw-source="[&lt;strong&gt;SetIpForwardEntry2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570773(v=vs.85))"><strong>SetIpForwardEntry2</strong></a></p></td>
<td align="left"><p>ローカル コンピューターの IP のルート エントリのプロパティを設定します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="ip-table-memory-management-functions"></a>IP テーブルのメモリ管理関数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550045(v=vs.85)" data-raw-source="[&lt;strong&gt;FreeMibTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550045(v=vs.85))"><strong>FreeMibTable</strong></a></p></td>
<td align="left"><p>ネットワーク インターフェイス、アドレス、およびルートのテーブルを返す関数によって割り当てられるバッファーを解放 (たとえば、 <a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552524(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIfTable2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552524(v=vs.85))"> <strong>GetIfTable2</strong> </a>と<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552508(v=vs.85)" data-raw-source="[&lt;strong&gt;GetAnycastIpAddressTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552508(v=vs.85))"> <strong>GetAnycastIpAddressTable</strong></a>)。</p></td>
</tr>
</tbody>
</table>

 

### <a name="notification-functions"></a>通知関数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544864(v=vs.85)" data-raw-source="[&lt;strong&gt;CancelMibChangeNotify2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544864(v=vs.85))"><strong>CancelMibChangeNotify2</strong></a></p></td>
<td align="left"><p>IP インターフェイスの変更、IP アドレスの変更、IP ルートの変更、および固定のユニキャスト IP アドレス テーブルを取得する要求の変更通知用のドライバーの登録を解除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568805(v=vs.85)" data-raw-source="[&lt;strong&gt;NotifyIpInterfaceChange&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568805(v=vs.85))"><strong>NotifyIpInterfaceChange</strong></a></p></td>
<td align="left"><p>ドライバーのすべての IP インターフェイス、IPv4 インターフェイス、またはローカル コンピューター上の IPv6 インターフェイスへの変更が通知を登録します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568806(v=vs.85)" data-raw-source="[&lt;strong&gt;NotifyRouteChange2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568806(v=vs.85))"><strong>NotifyRouteChange2</strong></a></p></td>
<td align="left"><p>ローカル コンピューター上の IP のルート エントリへの変更の通知を登録します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568809(v=vs.85)" data-raw-source="[&lt;strong&gt;NotifyUnicastIpAddressChange&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568809(v=vs.85))"><strong>NotifyUnicastIpAddressChange</strong></a></p></td>
<td align="left"><p>すべての IP インターフェイスのユニキャスト、ユニキャスト IPv4 アドレス、またはローカル コンピューター上のユニキャスト IPv6 アドレスへの変更の通知を登録します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="teredo-ipv6-client-management-functions"></a>Teredo IPv6 クライアント管理機能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552578(v=vs.85)" data-raw-source="[&lt;strong&gt;GetTeredoPort&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552578(v=vs.85))"><strong>GetTeredoPort</strong></a></p></td>
<td align="left"><p>ローカル コンピューターの Teredo クライアントが使用する動的の UDP ポート番号を取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568808(v=vs.85)" data-raw-source="[&lt;strong&gt;NotifyTeredoPortChange&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568808(v=vs.85))"><strong>NotifyTeredoPortChange</strong></a></p></td>
<td align="left"><p>Teredo クライアントがローカル コンピューター上の Teredo サービス ポートを使用する UDP ポート番号への変更の通知を登録します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568807(v=vs.85)" data-raw-source="[&lt;strong&gt;NotifyStableUnicastIpAddressTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568807(v=vs.85))"><strong>NotifyStableUnicastIpAddressTable</strong></a></p></td>
<td align="left"><p>ローカル コンピューター上の固定のユニキャスト IP アドレス テーブルを取得します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="mib-structures"></a>MIB 構造体

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">構造体</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557013(v=vs.85)" data-raw-source="[&lt;strong&gt;IP_ADDRESS_PREFIX&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557013(v=vs.85))"><strong>IP_ADDRESS_PREFIX</strong></a></p></td>
<td align="left"><p>IP アドレスのプレフィックスを格納します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559190(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_ANYCASTIPADDRESS_ROW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559190(v=vs.85))"><strong>MIB_ANYCASTIPADDRESS_ROW</strong></a></p></td>
<td align="left"><p>エニー キャスト IP アドレスに関する情報を格納します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559193(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_ANYCASTIPADDRESS_TABLE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559193(v=vs.85))"><strong>MIB_ANYCASTIPADDRESS_TABLE</strong></a></p></td>
<td align="left"><p>エニー キャスト IP アドレスのエントリのテーブルが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559214(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IF_ROW2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559214(v=vs.85))"><strong>MIB_IF_ROW2</strong></a></p></td>
<td align="left"><p>特定のインターフェイスに関する情報を格納します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559224(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IF_TABLE2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559224(v=vs.85))"><strong>MIB_IF_TABLE2</strong></a></p></td>
<td align="left"><p>論理および物理インターフェイス エントリのテーブルが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559207(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IFSTACK_ROW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559207(v=vs.85))"><strong>MIB_IFSTACK_ROW</strong></a></p></td>
<td align="left"><p>2 つのネットワーク インターフェイスの間のリレーションシップを表します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559210(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IFSTACK_TABLE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559210(v=vs.85))"><strong>MIB_IFSTACK_TABLE</strong></a></p></td>
<td align="left"><p>ネットワーク インターフェイス スタック内の行エントリのテーブルが含まれています。 このテーブルは、インターフェイスのスタックに対してネットワーク インターフェイスのリレーションシップを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559234(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_INVERTEDIFSTACK_ROW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559234(v=vs.85))"><strong>MIB_INVERTEDIFSTACK_ROW</strong></a></p></td>
<td align="left"><p>2 つのネットワーク インターフェイスの間のリレーションシップを表します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559240(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_INVERTEDIFSTACK_TABLE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559240(v=vs.85))"><strong>MIB_INVERTEDIFSTACK_TABLE</strong></a></p></td>
<td align="left"><p>逆のネットワーク インターフェイスのスタックの行エントリのテーブルが含まれています。 このテーブルは、逆の順序でインターフェイスのスタックに対してネットワーク インターフェイスのリレーションシップを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559245(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IPFORWARD_ROW2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559245(v=vs.85))"><strong>MIB_IPFORWARD_ROW2</strong></a></p></td>
<td align="left"><p>IP のルート エントリに関する情報を格納します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559252(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IPFORWARD_TABLE2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559252(v=vs.85))"><strong>MIB_IPFORWARD_TABLE2</strong></a></p></td>
<td align="left"><p>IP のルート エントリのテーブルが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559254(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IPINTERFACE_ROW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559254(v=vs.85))"><strong>MIB_IPINTERFACE_ROW</strong></a></p></td>
<td align="left"><p>ストアのインターフェイスのネットワーク インターフェイスで特定の IP アドレス ファミリの管理情報。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559260(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IPINTERFACE_TABLE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559260(v=vs.85))"><strong>MIB_IPINTERFACE_TABLE</strong></a></p></td>
<td align="left"><p>IP インターフェイスのエントリのテーブルが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559263(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IPNET_ROW2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559263(v=vs.85))"><strong>MIB_IPNET_ROW2</strong></a></p></td>
<td align="left"><p>近隣ノードの IP アドレスに関する情報を格納します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559267(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IPNET_TABLE2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559267(v=vs.85))"><strong>MIB_IPNET_TABLE2</strong></a></p></td>
<td align="left"><p>近隣ノードの IP アドレスのエントリのテーブルが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559270(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IPPATH_ROW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559270(v=vs.85))"><strong>MIB_IPPATH_ROW</strong></a></p></td>
<td align="left"><p>IP パスのエントリに関する情報を格納します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559273(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IPPATH_TABLE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559273(v=vs.85))"><strong>MIB_IPPATH_TABLE</strong></a></p></td>
<td align="left"><p>IP のパスのエントリのテーブルが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559277(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_MULTICASTIPADDRESS_ROW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559277(v=vs.85))"><strong>MIB_MULTICASTIPADDRESS_ROW</strong></a></p></td>
<td align="left"><p>マルチキャスト IP アドレスに関する情報を格納します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559281(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_MULTICASTIPADDRESS_TABLE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559281(v=vs.85))"><strong>MIB_MULTICASTIPADDRESS_TABLE</strong></a></p></td>
<td align="left"><p>マルチキャスト IP アドレスのエントリのテーブルが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559308(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_UNICASTIPADDRESS_ROW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559308(v=vs.85))"><strong>MIB_UNICASTIPADDRESS_ROW</strong></a></p></td>
<td align="left"><p>ユニキャスト IP アドレスに関する情報を格納します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559322(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_UNICASTIPADDRESS_TABLE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559322(v=vs.85))"><strong>MIB_UNICASTIPADDRESS_TABLE</strong></a></p></td>
<td align="left"><p>ユニキャスト IP アドレスのエントリのテーブルが含まれています。</p></td>
</tr>
</tbody>
</table>

 

### <a name="mib-enumerations"></a>MIB 列挙型

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">列挙値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/netioapi/ne-netioapi-_mib_if_table_level" data-raw-source="[&lt;strong&gt;MIB_IF_TABLE_LEVEL&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/netioapi/ne-netioapi-_mib_if_table_level)"><strong>MIB_IF_TABLE_LEVEL</strong></a></p></td>
<td align="left"><p>取得するインターフェイスの情報のレベルを定義します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559286(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_NOTIFICATION_TYPE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559286(v=vs.85))"><strong>MIB_NOTIFICATION_TYPE</strong></a></p></td>
<td align="left"><p>通知の発生時に、コールバック関数に渡される通知の種類を定義します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="nl-enumerations"></a>NL 列挙型

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">列挙値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-nl_address_type" data-raw-source="[&lt;strong&gt;NL_ADDRESS_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-nl_address_type)"><strong>NL_ADDRESS_TYPE</strong></a></p></td>
<td align="left"><p>ネットワーク層の IP アドレスの種類を指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568758(v=vs.85)" data-raw-source="[&lt;strong&gt;NL_DAD_STATE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568758(v=vs.85))"><strong>NL_DAD_STATE</strong></a></p></td>
<td align="left"><p>重複アドレス検出 (DAD) の状態を定義します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-_nl_link_local_address_behavior" data-raw-source="[&lt;strong&gt;NL_LINK_LOCAL_ADDRESS_BEHAVIOR&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-_nl_link_local_address_behavior)"><strong>NL_LINK_LOCAL_ADDRESS_BEHAVIOR</strong></a></p></td>
<td align="left"><p>リンク ローカル アドレスの動作を定義します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-_nl_neighbor_state" data-raw-source="[&lt;strong&gt;NL_NEIGHBOR_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-_nl_neighbor_state)"><strong>NL_NEIGHBOR_STATE</strong></a></p></td>
<td align="left"><p>RFC 2461、セクション 7.3.2」の説明に従って、ネットワーク層の近隣ノード IP アドレスの状態を定義します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568762(v=vs.85)" data-raw-source="[&lt;strong&gt;NL_PREFIX_ORIGIN&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568762(v=vs.85))"><strong>NL_PREFIX_ORIGIN</strong></a></p></td>
<td align="left"><p>IP アドレスのプレフィックスまたはネットワーク部分の原点を定義します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-_nl_route_origin" data-raw-source="[&lt;strong&gt;NL_ROUTE_ORIGIN&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-_nl_route_origin)"><strong>NL_ROUTE_ORIGIN</strong></a></p></td>
<td align="left"><p>IP のルートの起点を定義します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-nl_route_protocol" data-raw-source="[&lt;strong&gt;NL_ROUTE_PROTOCOL&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-nl_route_protocol)"><strong>NL_ROUTE_PROTOCOL</strong></a></p></td>
<td align="left"><p>RFC 4292」の説明に従って IP ルートを使用すると、追加されたルーティング メカニズムを定義します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-_nl_router_discovery_behavior" data-raw-source="[&lt;strong&gt;NL_ROUTER_DISCOVERY_BEHAVIOR&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-_nl_router_discovery_behavior)"><strong>NL_ROUTER_DISCOVERY_BEHAVIOR</strong></a></p></td>
<td align="left"><p>RFC 2461」の説明に従って、ルーター検出の動作を定義します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568768(v=vs.85)" data-raw-source="[&lt;strong&gt;NL_SUFFIX_ORIGIN&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568768(v=vs.85))"><strong>NL_SUFFIX_ORIGIN</strong></a></p></td>
<td align="left"><p>IP アドレスのサフィックスまたはホストの一部の配信元を定義します。</p></td>
</tr>
</tbody>
</table>

 

 

 





