---
title: WDM オーディオ ドライバーからの強化された機能
description: WDM オーディオ ドライバーからの強化された機能
ms.assetid: 8ee081ee-623d-4eaf-953f-20ccfbbe9800
keywords:
- WDM オーディオ拡張機能 WDK、従来のサポート拡張機能について
- WDM オーディオ拡張機能 WDK、デバイス Id
- デバイス Id WDK オーディオ
- 一意のデバイス Id WDK オーディオ
- オーディオデバイスの識別
- ハードウェア固有の情報 WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b29005666ab8778f022cbc5c5aee7972e95ad2ac
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833394"
---
# <a name="extended-capabilities-from-a-wdm-audio-driver"></a>WDM オーディオ ドライバーからの強化された機能


## <span id="extended_capabilities_from_a_wdm_audio_driver"></span><span id="EXTENDED_CAPABILITIES_FROM_A_WDM_AUDIO_DRIVER"></span>


[ **\_全般\_COMPONENTID**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-general-componentid)プロパティを処理することによって、オーディオフィルターは、アプリケーションが基になるデバイスを一意に識別するために使用できるハードウェア固有の情報を提供できます。 Microsoft Windows XP は、この機能をサポートするための Windows の最初のバージョンです。この機能は、以前のバージョンでは使用できません。

このフィルターは、次のものを含む[**KSCOMPONENTID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kscomponentid)構造体の形式でハードウェア固有の情報を提供します。

-   製造元の GUID

-   製品 GUID

-   コンポーネント GUID

-   名前 GUID

-   ハードウェアのバージョン番号

-   ハードウェアリビジョン番号

この情報へのアクセスを提供するために、WDM オーディオドライバーは、フィルターの自動化テーブルで COMPONENTID 全般\_\_のプロパティハンドラーを指定します。

アプリケーションは、次の従来の Windows マルチメディア Api ( **aux**、 **midiin**、 **midiin**、 **mixer**、 **waveIn**、 **waveOut**) を使用して、ドライバーの KSCOMPONENTID 構造からデータにアクセスできます。 クライアントは、次の表に示すマルチメディア関数のいずれかを呼び出して、2番目の引数として拡張機能の構造体を渡すことによって、ドライバーにこの情報を照会します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">マルチメディア機能</th>
<th align="left">拡張機能の構造</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>auxGetDevCaps</strong></p></td>
<td align="left"><p>AUXCAPS2</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>midiInGetDevCaps</strong></p></td>
<td align="left"><p>MIDIINCAPS2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>midiOutGetDevCaps</strong></p></td>
<td align="left"><p>MINIOUTCAPS2</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>mixerGetDevCaps</strong></p></td>
<td align="left"><p>MIXERCAPS2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>waveInGetDevCaps</strong></p></td>
<td align="left"><p>WAVEINCAPS2</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>waveOutGetDevCaps</strong></p></td>
<td align="left"><p>WAVEOUTCAPS2</p></td>
</tr>
</tbody>
</table>

 

フィルターのプロパティハンドラーから KSCOMPONENTID 構造体を受け取った後、WDMAud システムドライバー (Wdmaud) は、この構造体のデータを、 *xxx*getdevcaps 関数が使用する*xxx*CAPS2 形式に変換します。

関数に渡された機能の構造体が、製造元、製品、および名前の Guid を格納するのに十分な大きさであることを確認した後、この情報を取得する前に、 *xxx*getdevcaps 関数によって拡張構造にコピーします。 (KSCOMPONENTID のコンポーネント GUID は現在使用されていません)。

WDMAud は、**バージョン**と**リビジョン**メンバーを KSCOMPONENTID から連結して、 *xxx*getdevcaps 関数が機能構造の**vdriverversion**メンバーにコピーする16ビットリビジョン番号を形成します。

**Vdriverversion** = (**バージョン**&lt;&lt; 8) |(**リビジョン**& 0xff)

Microsoft は、以前は、お客様のオーディオデバイスの製造元 Id と製品 Id を登録する必要があります。 これらの Id は、ヘッダーファイル Mmreg .h にリリースされました。

Windows XP 以降では、登録済み Id は不要になりました。これらは、KSK プロパティ\_GENERAL\_COMPONENTID プロパティによって提供される製造元と製品 Guid に置き換えられます。 Guid は本質的に一意であり、簡単に生成でき、登録を必要としないため、ベンダーが登録済み Id よりも使用する方が便利です。

ただし、製品と製造元の Id が既に Microsoft に登録されている場合 (および Mmreg .h に含まれている場合)、マクロ INIT\_MMREG\_PID と INIT\_MMREG\_MID にあるを使用して、製品と製造元の Id を変換できます。を Guid に変換します。 これらのマクロを使用して Guid を生成する場合、WDMAud は、Guid から元の製品と製造元の Id を回復し、これらの Id を、 *xxx*によって入力された機能の構造の**Wpid**および**wmid**メンバーにコピーできます。GetDevCaps 呼び出し。

それ以外の場合は、製造元と製品 Id が登録されていない場合は、Guidgen.exe ユーティリティを使用して製造元と製品の Guid を生成するだけです。 (Guidgen.exe は Microsoft Windows SDK に含まれています)。ドライバーの Guid がこの型である場合、WDMAud は、既定の定数 MM\_マップされていないこと、および MM\_PID\_、それぞれ xxx によって入力された機能の構造の**Wmid**および**wpid**のメンバーにマップされていないことを示します。Getdevcaps 呼び出し。

WDMAud は、KSCOMPONENTID 構造体の**名前**GUID を使用して、レジストリ内の "name" キーを検索します。 このキーは、レジストリパス名 HKLM\\System\\CurrentControlSet\\Control\\MediaCategories にあります。 デバイスの "Name" キーには、デバイス名を含む文字列値が関連付けられています。 *Xxx*getdevcaps 関数は、この名前文字列の最初の31文字を capabilities 構造体の**szPname**メンバーにコピーします。 31文字を超えるデバイス名の場合、クライアントアプリケーションはレジストリキーを開き、文字列全体を直接読み取ることができます。 ドライバーは、次の2つの方法のいずれかでこのレジストリエントリを設定できます。

-   ドライバーは、インストール時にデバイスの INF ファイルのエントリを指定できます。

-   ドライバーは、フィルター初期化ルーチンの実行中にエントリを読み込むことができます。

名前 GUID は省略可能です。 ドライバーが KSCOMPONENTID の**Name**メンバーを GUID\_NULL 値に設定した場合、WDMAud はデバイスのフレンドリ名を*xxx*getdevcaps 関数に提供します。これにより、この名前が機能の**szPname**メンバーにコピーされます。データ.

フィルターで KSK プロパティ\_GENERAL\_COMPONENTID プロパティのハンドラーが公開されていない場合、WDMAud は KSCOMPONENTID 構造体のデータの代わりに既定値を使用します。 機能構造の従来の部分の既定値は次のとおりです。

-   **Wmid** = MM\_MICROSOFT

-   **Wpid** = 次の一覧のデバイスクラス: MM\_MSFT\_wdmaudio\_WAVEOUT MM\_MSFT\_WDMAUDIO\_WAVEIN MM\_MSFT\_wdmaudio\_MIDIOUT MM\_msft\_WDMAUDIO\_MIDIIN MM\_MSFT\_WDMAUDIO\_ミキサー MM\_MSFT\_WDMAUDIO\_AUX
-   **Vdriverversion** = 0x050a (windows xp の場合) または 0x0500 (windows xp 以前)

Windows XP より前のバージョンの Windows では、機能構造の従来のメンバーは常に上記の既定値に設定されています。 Windows XP 以降では、拡張機能の既定値は次のとおりです。

-   **Nameguid** = GUID\_NULL

-   INIT\_MMREG\_MID (&**ManufacturerGuid**、 **wmid**)

-   初期化\_MMREG\_PID (&**Productguid**, **wpid**)

上記の初期化\_MMREG\_MID および INIT\_MMREG\_PID マクロは、Ksmedia. h で定義されています。 これらのマクロは、 **Wmid**メンバーと**wpid**メンバーの製造元と製品 id を、 **ManufacturerGuid**および**productguid**メンバーに読み込まれた guid に変換するために使用されます。

 

 




