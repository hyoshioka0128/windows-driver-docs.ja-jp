---
title: IP ヘルパーの概要
description: IP ヘルパーの概要
ms.assetid: c7cf1f47-ee0d-4c89-883b-717b719fcc2a
keywords:
- IP ヘルパー WDK ネットワーク
- IP ヘルパー WDK ネットワーク、概要
- ネットワークドライバー WDK、IP ヘルパー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f9818a47e89a1c42a362b6c4466a33a5fd04fbe
ms.sourcegitcommit: 2aa583e3da4ae9338a0d11678bf77f1460286f2d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "70063918"
---
# <a name="ip-helper-overview"></a>IP ヘルパーの概要

インターネットプロトコルヘルパー (IP ヘルパー) を使用すると、ドライバーはローカルコンピューターのネットワーク構成に関する情報を取得し、その構成を変更することができます。 また、IP ヘルパーは、ローカルコンピューターのネットワーク構成の特定の側面が変更されたときに、ドライバーに確実に通知するための通知メカニズムも提供します。 IP ヘルパーは、Windows Vista 以降のバージョンの Microsoft Windows オペレーティングシステムで使用できます。

IP ヘルパー関数の多くは、管理情報ベース (MIB) テクノロジに関連付けられているデータ型を表す構造パラメーターを渡します。 IP ヘルパー関数は、これらの MIB 構造を使用して、さまざまなネットワーク情報を表します。

IP ヘルパードキュメントでは、"adapter" と "interface" という用語を広範囲にわたって使用しています。 *アダプター*は、従来の用語であり、*ネットワークアダプター*の省略形であり、当初は何らかの形式のネットワークハードウェアと呼ばれていました。 アダプターはデータリンクレベルの抽象化です。

IETF RFC ドキュメントでは、*インターフェイス*は、リンクへのノードの添付ファイルを表す抽象概念として記述されています。 インターフェイスは、IP レベルの抽象化です。

ドライバーは、次のカーネルモード関数、MIB 構造体、および MIB と Network Layer (NL) 列挙を使用して、ローカルコンピューター上の伝送制御プロトコル/インターネットプロトコル (TCP/IP) トランスポートの構成設定を取得および変更できます。

**メモドライバーコード**を開発している場合は、ヘッダーファイルを含めるための手順に従って[ください。](including-header-files-for-ip-helper.md)   

 

### <a name="interface-conversion-functions"></a>インターフェイス変換関数

<table>  
<colgroup><col width="50%" /> <col width="50%" /></colgroup>  
<thead>  
<tr class="header">  
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546130(v=vs.85)" data-raw-source="[&lt;strong&gt;ConvertInterfaceAliasToLuid&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546130(v=vs.85))"><strong>ConvertInterfaceAliasToLuid</strong></a></p></td>
<td align="left"><p>ネットワークインターフェイスのローカル一意識別子 (LUID) を Unicode インターフェイス名に変換します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546137(v=vs.85)" data-raw-source="[&lt;strong&gt;ConvertInterfaceGuidToLuid&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546137(v=vs.85))"><strong>ConvertInterfaceGuidToLuid</strong></a></p></td>
<td align="left"><p>ネットワークインターフェイスのグローバル一意識別子 (GUID) を、インターフェイスの LUID に変換します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546141(v=vs.85)" data-raw-source="[&lt;strong&gt;ConvertInterfaceIndexToLuid&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546141(v=vs.85))"><strong>ConvertInterfaceIndexToLuid</strong></a></p></td>
<td align="left"><p>ネットワークインターフェイスのローカルインデックスを、インターフェイスの LUID に変換します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546151(v=vs.85)" data-raw-source="[&lt;strong&gt;ConvertInterfaceLuidToAlias&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546151(v=vs.85))"><strong>ConvertInterfaceLuidToAlias</strong></a></p></td>
<td align="left"><p>ネットワークインターフェイスの LUID をインターフェイスエイリアスに変換します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546156(v=vs.85)" data-raw-source="[&lt;strong&gt;ConvertInterfaceLuidToGuid&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546156(v=vs.85))"><strong>ConvertInterfaceLuidToGuid</strong></a></p></td>
<td align="left"><p>ネットワークインターフェイスの LUID をインターフェイスの GUID に変換します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546167(v=vs.85)" data-raw-source="[&lt;strong&gt;ConvertInterfaceLuidToIndex&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546167(v=vs.85))"><strong>ConvertInterfaceLuidToIndex</strong></a></p></td>
<td align="left"><p>ネットワークインターフェイスの LUID を、インターフェイスのローカルインデックスに変換します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546171(v=vs.85)" data-raw-source="[&lt;strong&gt;ConvertInterfaceLuidToNameA&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546171(v=vs.85))"><strong>ConvertInterfaceLuidToNameA</strong></a></p></td>
<td align="left"><p>ネットワークインターフェイスの LUID を ANSI インターフェイス名に変換します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546175(v=vs.85)" data-raw-source="[&lt;strong&gt;ConvertInterfaceLuidToNameW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546175(v=vs.85))"><strong>ConvertInterfaceLuidToNameW</strong></a></p></td>
<td align="left"><p>ネットワークインターフェイスの LUID を Unicode インターフェイス名に変換します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546185(v=vs.85)" data-raw-source="[&lt;strong&gt;ConvertInterfaceNameToLuidA&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546185(v=vs.85))"><strong>ConvertInterfaceNameToLuidA</strong></a></p></td>
<td align="left"><p>ANSI ネットワークインターフェイス名をインターフェイスの LUID に変換します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546192(v=vs.85)" data-raw-source="[&lt;strong&gt;ConvertInterfaceNameToLuidW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546192(v=vs.85))"><strong>ConvertInterfaceNameToLuidW</strong></a></p></td>
<td align="left"><p>Unicode ネットワークインターフェイス名をインターフェイスの LUID に変換します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553785(v=vs.85)" data-raw-source="[&lt;strong&gt;if_indextoname&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553785(v=vs.85))"><strong>if_indextoname</strong></a></p></td>
<td align="left"><p>ネットワークインターフェイスのローカルインデックスを ANSI インターフェイス名に変換します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553788(v=vs.85)" data-raw-source="[&lt;strong&gt;if_nametoindex&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553788(v=vs.85))"><strong>if_nametoindex</strong></a></p></td>
<td align="left"><p>ネットワークインターフェイスの ANSI インターフェイス名をインターフェイスのローカルインデックスに変換します。</p></td>
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
<td align="left"><p>ローカルコンピューター上の指定されたインターフェイスの情報を取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552521(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIfStackTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552521(v=vs.85))"><strong>GetIfStackTable</strong></a></p></td>
<td align="left"><p>インターフェイススタック上のネットワークインターフェイスの関係を指定するネットワークインターフェイススタックの行エントリのテーブルを取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552524(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIfTable2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552524(v=vs.85))"><strong>GetIfTable2</strong></a></p></td>
<td align="left"><p>MIB-II インターフェイステーブルを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552528(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIfTable2Ex&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552528(v=vs.85))"><strong>GetIfTable2Ex</strong></a></p></td>
<td align="left"><p>取得するインターフェイス情報のレベルを指定して、MIB-II インターフェイステーブルを取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552531(v=vs.85)" data-raw-source="[&lt;strong&gt;GetInvertedIfStackTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552531(v=vs.85))"><strong>GetInvertedIfStackTable</strong></a></p></td>
<td align="left"><p>インターフェイススタック上のネットワークインターフェイスの関係を指定する、反転されたネットワークインターフェイススタック行エントリのテーブルを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552540(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIpInterfaceEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552540(v=vs.85))"><strong>Ge? Interfaceentry</strong></a></p></td>
<td align="left"><p>ローカルコンピューター上の指定されたインターフェイスの IP 情報を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552543(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIpInterfaceTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552543(v=vs.85))"><strong>Ge? Interfacetable</strong></a></p></td>
<td align="left"><p>ローカルコンピューター上の IP インターフェイスエントリを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554883(v=vs.85)" data-raw-source="[&lt;strong&gt;InitializeIpInterfaceEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554883(v=vs.85))"><strong>初期化 Eipinterfaceentry</strong></a></p></td>
<td align="left"><p>既定値を使用して<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559254(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IPINTERFACE_ROW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559254(v=vs.85))"><strong>MIB_IPINTERFACE_ROW</strong></a> structure エントリのメンバーを初期化します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570774(v=vs.85)" data-raw-source="[&lt;strong&gt;SetIpInterfaceEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570774(v=vs.85))"><strong>Se? Interfaceentry</strong></a></p></td>
<td align="left"><p>ローカルコンピューターの IP インターフェイスのプロパティを設定します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="ip-address-management-functions"></a>IP アドレス管理機能

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
<td align="left"><p>ローカルコンピューターに新しいエニーキャスト IP アドレスエントリを追加します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546219(v=vs.85)" data-raw-source="[&lt;strong&gt;CreateSortedAddressPairs&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546219(v=vs.85))"><strong>パッケージの一括</strong></a></p></td>
<td align="left"><p>指定された宛先アドレスの一覧とホストコンピューターのローカル IP アドレスを組み合わせて、優先順位に従ってペアを並べ替えます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546227(v=vs.85)" data-raw-source="[&lt;strong&gt;CreateUnicastIpAddressEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546227(v=vs.85))"><strong>CreateUnicastIpAddressEntry</strong></a></p></td>
<td align="left"><p>ローカルコンピューターに新しいユニキャスト IP アドレスエントリを追加します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546363(v=vs.85)" data-raw-source="[&lt;strong&gt;DeleteAnycastIpAddressEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546363(v=vs.85))"><strong>DeleteAnycastIpAddressEntry</strong></a></p></td>
<td align="left"><p>ローカルコンピューター上の既存のエニーキャスト IP アドレスエントリを削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546370(v=vs.85)" data-raw-source="[&lt;strong&gt;DeleteUnicastIpAddressEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546370(v=vs.85))"><strong>DeleteUnicastIpAddressEntry</strong></a></p></td>
<td align="left"><p>ローカルコンピューターから既存のユニキャスト IP アドレスエントリを削除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552504(v=vs.85)" data-raw-source="[&lt;strong&gt;GetAnycastIpAddressEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552504(v=vs.85))"><strong>GetAnycastIpAddressEntry</strong></a></p></td>
<td align="left"><p>ローカルコンピューター上の既存のエニーキャスト IP アドレスエントリの情報を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552508(v=vs.85)" data-raw-source="[&lt;strong&gt;GetAnycastIpAddressTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552508(v=vs.85))"><strong>GetAnycastIpAddressTable</strong></a></p></td>
<td align="left"><p>ローカルコンピューター上のエニーキャスト IP アドレステーブルを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552565(v=vs.85)" data-raw-source="[&lt;strong&gt;GetMulticastIpAddressEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552565(v=vs.85))"><strong>GetMulticastIpAddressEntry</strong></a></p></td>
<td align="left"><p>ローカルコンピューター上の既存のマルチキャスト IP アドレスエントリの情報を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552570(v=vs.85)" data-raw-source="[&lt;strong&gt;GetMulticastIpAddressTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552570(v=vs.85))"><strong>GetMulticastIpAddressTable</strong></a></p></td>
<td align="left"><p>ローカルコンピューター上のマルチキャスト IP アドレステーブルを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552589(v=vs.85)" data-raw-source="[&lt;strong&gt;GetUnicastIpAddressEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552589(v=vs.85))"><strong>GetUnicastIpAddressEntry</strong></a></p></td>
<td align="left"><p>ローカルコンピューター上の既存のユニキャスト IP アドレスエントリの情報を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552594(v=vs.85)" data-raw-source="[&lt;strong&gt;GetUnicastIpAddressTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552594(v=vs.85))"><strong>GetUnicastIpAddressTable</strong></a></p></td>
<td align="left"><p>ローカルコンピューター上のユニキャスト IP アドレステーブルを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554886(v=vs.85)" data-raw-source="[&lt;strong&gt;InitializeUnicastIpAddressEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554886(v=vs.85))"><strong>InitializeUnicastIpAddressEntry</strong></a></p></td>
<td align="left"><p>ローカルコンピューター上のユニキャスト IP アドレスエントリの既定値を使用して、 <a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559308(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_UNICASTIPADDRESS_ROW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559308(v=vs.85))"><strong>MIB_UNICASTIPADDRESS_ROW</strong></a>構造体を初期化します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568807(v=vs.85)" data-raw-source="[&lt;strong&gt;NotifyStableUnicastIpAddressTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568807(v=vs.85))"><strong>NotifyStableUnicastIpAddressTable</strong></a></p></td>
<td align="left"><p>ローカルコンピューター上の安定したユニキャスト IP アドレステーブルを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570800(v=vs.85)" data-raw-source="[&lt;strong&gt;SetUnicastIpAddressEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570800(v=vs.85))"><strong>SetUnicastIpAddressEntry</strong></a></p></td>
<td align="left"><p>ローカルコンピューター上の既存のユニキャスト IP アドレスエントリのプロパティを設定します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="ip-neighbor-address-management-functions"></a>IP 近隣アドレス管理機能

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
<td align="left"><p>ローカルコンピューターに新しい近隣ノード IP アドレスエントリを作成します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546368(v=vs.85)" data-raw-source="[&lt;strong&gt;DeleteIpNetEntry2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546368(v=vs.85))"><strong>DeleteIpNetEntry2</strong></a></p></td>
<td align="left"><p>ローカルコンピューターから近隣ノード IP アドレスエントリを削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550029(v=vs.85)" data-raw-source="[&lt;strong&gt;FlushIpNetTable2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550029(v=vs.85))"><strong>FlushIpNetTable2</strong></a></p></td>
<td align="left"><p>ローカルコンピューター上の IP 近隣テーブルをフラッシュします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552546(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIpNetEntry2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552546(v=vs.85))"><strong>GetIpNetEntry2</strong></a></p></td>
<td align="left"><p>ローカルコンピューター上の近隣 IP アドレスエントリの情報を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552551(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIpNetTable2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552551(v=vs.85))"><strong>GetIpNetTable2</strong></a></p></td>
<td align="left"><p>ローカルコンピューター上の IP 近隣テーブルを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570686(v=vs.85)" data-raw-source="[&lt;strong&gt;ResolveIpNetEntry2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570686(v=vs.85))"><strong>ResolveIpNetEntry2</strong></a></p></td>
<td align="left"><p>ローカルコンピューター上の近隣 IP アドレスエントリの物理アドレスを解決します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570775(v=vs.85)" data-raw-source="[&lt;strong&gt;SetIpNetEntry2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570775(v=vs.85))"><strong>SetIpNetEntry2</strong></a></p></td>
<td align="left"><p>ローカルコンピューター上の既存の近隣ノード IP アドレスエントリの物理アドレスを設定します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="ip-path-management-functions"></a>IP パス管理機能

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
<td align="left"><p>ローカルコンピューター上の IP パステーブルをフラッシュします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552556(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIpPathEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552556(v=vs.85))"><strong>Ge? Pathentry</strong></a></p></td>
<td align="left"><p>ローカルコンピューター上の IP パスエントリの情報を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552559(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIpPathTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552559(v=vs.85))"><strong>Ge? Pathtable</strong></a></p></td>
<td align="left"><p>ローカルコンピューター上の IP パスエントリの情報を取得します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="ip-route-management-functions"></a>IP ルート管理機能

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
<td align="left"><p>ローカルコンピューター上に新しい IP ルートエントリを作成します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546365(v=vs.85)" data-raw-source="[&lt;strong&gt;DeleteIpForwardEntry2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546365(v=vs.85))"><strong>DeleteIpForwardEntry2</strong></a></p></td>
<td align="left"><p>ローカルコンピューターから IP ルートエントリを削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552511(v=vs.85)" data-raw-source="[&lt;strong&gt;GetBestRoute2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552511(v=vs.85))"><strong>GetBestRoute2</strong></a></p></td>
<td align="left"><p>指定された宛先 IP アドレスに最適なルートを取得するために、ローカルコンピューター上の IP ルートエントリを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552535(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIpForwardEntry2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552535(v=vs.85))"><strong>GetIpForwardEntry2</strong></a></p></td>
<td align="left"><p>ローカルコンピューター上の IP ルートエントリの情報を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552536(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIpForwardTable2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552536(v=vs.85))"><strong>GetIpForwardTable2</strong></a></p></td>
<td align="left"><p>ローカルコンピューター上の IP ルートエントリを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554882(v=vs.85)" data-raw-source="[&lt;strong&gt;InitializeIpForwardEntry&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554882(v=vs.85))"><strong>初期化 Eipforwardエントリ</strong></a></p></td>
<td align="left"><p>ローカルコンピューター上の IP ルートエントリの既定値を使用して、 <a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559245(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IPFORWARD_ROW2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559245(v=vs.85))"><strong>MIB_IPFORWARD_ROW2</strong></a>構造体を初期化します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570773(v=vs.85)" data-raw-source="[&lt;strong&gt;SetIpForwardEntry2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570773(v=vs.85))"><strong>SetIpForwardEntry2</strong></a></p></td>
<td align="left"><p>ローカルコンピューター上の IP ルートエントリのプロパティを設定します。</p></td>
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
<td align="left"><p>ネットワークインターフェイス、アドレス、およびルートのテーブル ( <a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552524(v=vs.85)" data-raw-source="[&lt;strong&gt;GetIfTable2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552524(v=vs.85))"><strong>GetIfTable2</strong></a> 、 <a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552508(v=vs.85)" data-raw-source="[&lt;strong&gt;GetAnycastIpAddressTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552508(v=vs.85))"><strong>GetAnycastIpAddressTable</strong></a>など) を返す関数によって割り当てられたバッファーを解放します。</p></td>
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
<td align="left"><p>解除は、IP インターフェイスの変更、IP アドレスの変更、IP ルートの変更、および安定したユニキャスト IP アドレステーブルを取得するための要求について、変更通知用のドライバーを使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568805(v=vs.85)" data-raw-source="[&lt;strong&gt;NotifyIpInterfaceChange&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568805(v=vs.85))"><strong>NotifyIpInterfaceChange</strong></a></p></td>
<td align="left"><p>ローカルコンピューター上のすべての IP インターフェイス、IPv4 インターフェイス、または IPv6 インターフェイスに対する変更が通知されるように、ドライバーに登録します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568806(v=vs.85)" data-raw-source="[&lt;strong&gt;NotifyRouteChange2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568806(v=vs.85))"><strong>NotifyRouteChange2</strong></a></p></td>
<td align="left"><p>ローカルコンピューター上の IP ルートエントリに対する変更が通知されるように登録します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568809(v=vs.85)" data-raw-source="[&lt;strong&gt;NotifyUnicastIpAddressChange&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568809(v=vs.85))"><strong>NotifyUnicastIpAddressChange</strong></a></p></td>
<td align="left"><p>ローカルコンピューター上のすべてのユニキャスト IP インターフェイス、ユニキャスト IPv4 アドレス、またはユニキャスト IPv6 アドレスに対する変更が通知されるように登録します。</p></td>
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
<td align="left"><p>Teredo クライアントがローカルコンピューター上で使用する動的な UDP ポート番号を取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568808(v=vs.85)" data-raw-source="[&lt;strong&gt;NotifyTeredoPortChange&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568808(v=vs.85))"><strong>NotifyTeredoPortChange</strong></a></p></td>
<td align="left"><p>Teredo クライアントがローカルコンピューターの Teredo サービスポートに使用する UDP ポート番号の変更が通知されるように登録します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568807(v=vs.85)" data-raw-source="[&lt;strong&gt;NotifyStableUnicastIpAddressTable&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568807(v=vs.85))"><strong>NotifyStableUnicastIpAddressTable</strong></a></p></td>
<td align="left"><p>ローカルコンピューター上の安定したユニキャスト IP アドレステーブルを取得します。</p></td>
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
<td align="left"><p>IP アドレスプレフィックスを格納します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559190(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_ANYCASTIPADDRESS_ROW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559190(v=vs.85))"><strong>MIB_ANYCASTIPADDRESS_ROW</strong></a></p></td>
<td align="left"><p>エニーキャスト IP アドレスに関する情報を格納します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559193(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_ANYCASTIPADDRESS_TABLE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559193(v=vs.85))"><strong>MIB_ANYCASTIPADDRESS_TABLE</strong></a></p></td>
<td align="left"><p>エニーキャスト IP アドレスエントリの表が含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559214(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IF_ROW2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559214(v=vs.85))"><strong>MIB_IF_ROW2</strong></a></p></td>
<td align="left"><p>特定のインターフェイスに関する情報を格納します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559224(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IF_TABLE2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559224(v=vs.85))"><strong>MIB_IF_TABLE2</strong></a></p></td>
<td align="left"><p>論理および物理インターフェイスエントリのテーブルが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559207(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IFSTACK_ROW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559207(v=vs.85))"><strong>MIB_IFSTACK_ROW</strong></a></p></td>
<td align="left"><p>2つのネットワークインターフェイス間のリレーションシップを表します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559210(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IFSTACK_TABLE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559210(v=vs.85))"><strong>MIB_IFSTACK_TABLE</strong></a></p></td>
<td align="left"><p>ネットワークインターフェイススタック内の行エントリのテーブルを格納します。 次の表は、インターフェイススタック上のネットワークインターフェイスの関係を示しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559234(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_INVERTEDIFSTACK_ROW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559234(v=vs.85))"><strong>MIB_INVERTEDIFSTACK_ROW</strong></a></p></td>
<td align="left"><p>2つのネットワークインターフェイス間のリレーションシップを表します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559240(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_INVERTEDIFSTACK_TABLE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559240(v=vs.85))"><strong>MIB_INVERTEDIFSTACK_TABLE</strong></a></p></td>
<td align="left"><p>反転されたネットワークインターフェイススタックの行エントリのテーブルを格納します。 次の表は、インターフェイススタック上のネットワークインターフェイスの逆の順序の関係を示しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559245(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IPFORWARD_ROW2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559245(v=vs.85))"><strong>MIB_IPFORWARD_ROW2</strong></a></p></td>
<td align="left"><p>IP ルートエントリに関する情報を格納します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559252(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IPFORWARD_TABLE2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559252(v=vs.85))"><strong>MIB_IPFORWARD_TABLE2</strong></a></p></td>
<td align="left"><p>IP ルートエントリのテーブルが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559254(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IPINTERFACE_ROW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559254(v=vs.85))"><strong>MIB_IPINTERFACE_ROW</strong></a></p></td>
<td align="left"><p>特定の IP アドレスファミリのインターフェイス管理情報をネットワークインターフェイスに格納します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559260(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IPINTERFACE_TABLE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559260(v=vs.85))"><strong>MIB_IPINTERFACE_TABLE</strong></a></p></td>
<td align="left"><p>IP インターフェイスエントリのテーブルが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559263(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IPNET_ROW2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559263(v=vs.85))"><strong>MIB_IPNET_ROW2</strong></a></p></td>
<td align="left"><p>近隣 IP アドレスに関する情報を格納します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559267(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IPNET_TABLE2&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559267(v=vs.85))"><strong>MIB_IPNET_TABLE2</strong></a></p></td>
<td align="left"><p>近隣 IP アドレスエントリのテーブルが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559270(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IPPATH_ROW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559270(v=vs.85))"><strong>MIB_IPPATH_ROW</strong></a></p></td>
<td align="left"><p>IP パスエントリに関する情報を格納します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559273(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_IPPATH_TABLE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559273(v=vs.85))"><strong>MIB_IPPATH_TABLE</strong></a></p></td>
<td align="left"><p>IP パスエントリのテーブルが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559277(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_MULTICASTIPADDRESS_ROW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559277(v=vs.85))"><strong>MIB_MULTICASTIPADDRESS_ROW</strong></a></p></td>
<td align="left"><p>マルチキャスト IP アドレスに関する情報を格納します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559281(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_MULTICASTIPADDRESS_TABLE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559281(v=vs.85))"><strong>MIB_MULTICASTIPADDRESS_TABLE</strong></a></p></td>
<td align="left"><p>マルチキャスト IP アドレスエントリの表が含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559308(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_UNICASTIPADDRESS_ROW&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559308(v=vs.85))"><strong>MIB_UNICASTIPADDRESS_ROW</strong></a></p></td>
<td align="left"><p>ユニキャスト IP アドレスに関する情報を格納します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559322(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_UNICASTIPADDRESS_TABLE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559322(v=vs.85))"><strong>MIB_UNICASTIPADDRESS_TABLE</strong></a></p></td>
<td align="left"><p>ユニキャスト IP アドレスエントリのテーブルが含まれています。</p></td>
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
<td align="left"><p>取得するインターフェイス情報のレベルを定義します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559286(v=vs.85)" data-raw-source="[&lt;strong&gt;MIB_NOTIFICATION_TYPE&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff559286(v=vs.85))"><strong>MIB_NOTIFICATION_TYPE</strong></a></p></td>
<td align="left"><p>通知が発生したときにコールバック関数に渡される通知の種類を定義します。</p></td>
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
<td align="left"><p>重複するアドレス検出 (DAD) の状態を定義します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-_nl_link_local_address_behavior" data-raw-source="[&lt;strong&gt;NL_LINK_LOCAL_ADDRESS_BEHAVIOR&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-_nl_link_local_address_behavior)"><strong>NL_LINK_LOCAL_ADDRESS_BEHAVIOR</strong></a></p></td>
<td align="left"><p>リンクローカルアドレスの動作を定義します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-_nl_neighbor_state" data-raw-source="[&lt;strong&gt;NL_NEIGHBOR_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-_nl_neighbor_state)"><strong>NL_NEIGHBOR_STATE</strong></a></p></td>
<td align="left"><p>RFC 2461 のセクション7.3.2 で説明されているように、ネットワークレイヤーの近隣ノード IP アドレスの状態を定義します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568762(v=vs.85)" data-raw-source="[&lt;strong&gt;NL_PREFIX_ORIGIN&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568762(v=vs.85))"><strong>NL_PREFIX_ORIGIN</strong></a></p></td>
<td align="left"><p>IP アドレスのプレフィックスまたはネットワーク部分の起点を定義します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-_nl_route_origin" data-raw-source="[&lt;strong&gt;NL_ROUTE_ORIGIN&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-_nl_route_origin)"><strong>NL_ROUTE_ORIGIN</strong></a></p></td>
<td align="left"><p>IP ルートの起点を定義します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-nl_route_protocol" data-raw-source="[&lt;strong&gt;NL_ROUTE_PROTOCOL&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-nl_route_protocol)"><strong>NL_ROUTE_PROTOCOL</strong></a></p></td>
<td align="left"><p>RFC 4292 で説明されているように、IP ルートを追加したルーティング機構を定義します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-_nl_router_discovery_behavior" data-raw-source="[&lt;strong&gt;NL_ROUTER_DISCOVERY_BEHAVIOR&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/nldef/ne-nldef-_nl_router_discovery_behavior)"><strong>NL_ROUTER_DISCOVERY_BEHAVIOR</strong></a></p></td>
<td align="left"><p>RFC 2461 で説明されているように、ルーター検出の動作を定義します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568768(v=vs.85)" data-raw-source="[&lt;strong&gt;NL_SUFFIX_ORIGIN&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568768(v=vs.85))"><strong>NL_SUFFIX_ORIGIN</strong></a></p></td>
<td align="left"><p>IP アドレスのサフィックスまたはホスト部分の起点を定義します。</p></td>
</tr>
</tbody>
</table>

 

 

 





