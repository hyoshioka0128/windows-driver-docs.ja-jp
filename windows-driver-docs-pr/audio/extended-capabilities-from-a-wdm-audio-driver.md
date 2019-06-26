---
title: WDM オーディオ ドライバーからの強化された機能
description: WDM オーディオ ドライバーからの強化された機能
ms.assetid: 8ee081ee-623d-4eaf-953f-20ccfbbe9800
keywords:
- WDM オーディオ拡張 WDK、レガシ サポートの拡張機能について
- WDM オーディオ拡張 WDK、デバイス Id
- デバイス Id の WDK オーディオ
- 一意のデバイス Id の WDK オーディオ
- オーディオ デバイスを識別します。
- WDK オーディオのハードウェアに固有の情報
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b55ac80255b9d74e5ffbcd24105dbdf9266ba31c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360045"
---
# <a name="extended-capabilities-from-a-wdm-audio-driver"></a>WDM オーディオ ドライバーからの強化された機能


## <span id="extended_capabilities_from_a_wdm_audio_driver"></span><span id="EXTENDED_CAPABILITIES_FROM_A_WDM_AUDIO_DRIVER"></span>


処理することによって、 [ **KSPROPERTY\_全般\_COMPONENTID** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-general-componentid)プロパティ、オーディオのフィルターはアプリケーションを使用して一意にするハードウェアに固有の情報を提供できます基になるデバイスを識別します。 Microsoft Windows XP は、この機能をサポートするために Windows の最初のバージョンこの機能は、以前のバージョンでご利用いただけません。

フィルターの形式でハードウェアに固有の情報を提供する、 [ **KSCOMPONENTID** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kscomponentid)次を含む構造体。

-   GUID の製造元

-   製品の GUID

-   コンポーネントの GUID

-   GUID の名前

-   ハードウェアのバージョン番号

-   ハードウェアのリビジョン番号

WDM オーディオ ドライバーはこの情報へのアクセスを提供する、KSPROPERTY をプロパティ ハンドラーを指定します\_全般\_COMPONENTID フィルター automation テーブルにします。

従来の Windows マルチ メディア api は次のドライバーの KSCOMPONENTID 構造からデータにアクセスできるアプリケーション: **aux**、 **midiIn**、 **midiOut**、 **ミキサー**、 **waveIn**、および**waveOut**します。 クライアントでは、次の表に、マルチ メディア機能の 1 つを呼び出すと、2 番目の引数として、拡張機能の構造に渡すことによってドライバーに対してこの情報を照会します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">マルチ メディア関数</th>
<th align="left">拡張機能の構造体</th>
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

 

WDMAud システム ドライバー (Wdmaud.sys) がこの構造体のデータを変換、フィルターのプロパティのハンドラーから KSCOMPONENTID 構造体を受信した後、 *XXX*CAPS2 形式で、 *xxx*GetDevCaps 関数を使用します。

製造元、製品、および名前の Guid を格納するのに十分な大きさが、機能の構造が、関数に渡されることを確認したら、 *xxx*GetDevCaps 関数では、この情報をコピーする前に、拡張の構造に返します。 (現在コンポーネント KSCOMPONENTID から GUID を使用できません)。

WDMAud 連結、**バージョン**と**リビジョン**する 16 ビットのリビジョンを形成する KSCOMPONENTID からメンバーの数値、 *xxx*GetDevCaps 関数、にコピー**vDriverVersion**機能の構造体のメンバー。

**vDriverVersion** = (**バージョン** &lt; &lt; 8) |(**リビジョン**& 0 xff)

以前、Microsoft には、製造元 Id と製品 Id、オーディオ デバイスを登録するベンダーが必要です。 これらの Id は、ヘッダー ファイル Mmreg.h しリリースされました。

Windows XP 以降では、次のように登録されている Id は不要になりました。KSPROPERTY を通じて提供されます。 製造元および製品の Guid に置き換えられます\_全般\_COMPONENTID プロパティ。 Guid は、登録済みの Id Guid は本質的に一意であるためにが簡単に生成され、登録は必要ありませんを使用するベンダーにとってより便利です。

ただし、Microsoft と product や manufacturer の Id を既に登録 (および Mmreg.h にいる) 場合は、INIT マクロを使用できます\_MMREG\_PID および INIT\_MMREG\_で変換する Ksmedia.h MID、Guid に product や manufacturer の Id。 WDMAud が元の product や manufacturer の Id を Guid から回復にこれらの Id をコピーできる Guid を生成するこれらのマクロを使用する場合、**監視**と**wMid**機能のメンバー構造体によって入力されますが、 *xxx*GetDevCaps を呼び出します。

それ以外の場合、登録済みの製造元と製品 Id がいない場合だけ、GuidGen ユーティリティを使用して製造元および製品の Guid を生成します。 (GuidGen は、Microsoft Windows SDK に含まれます)。ドライバーの Guid がこの型で WDMAud 読み込みます既定定数 MM\_マップ解除済みと MM\_PID\_にマップされていない、 **wMid**と**監視**メンバーによって入力機能構造のそれぞれの*xxx*GetDevCaps 呼び出します。

WDMAud を使用して、**名前**レジストリ内の"Name"キーを検索する KSCOMPONENTID 構造内の GUID。 このキーが HKLM レジストリ パス名の下にある\\システム\\CurrentControlSet\\コントロール\\MediaCategories します。 デバイスの"Name"キーには、デバイス名を含む関連付けられている文字列値があります。 *Xxx*GetDevCaps 関数にこの名前の文字列の最初の 31 文字のコピー、 **szPname**機能の構造体のメンバー。 デバイスの名前は 31 文字より長い、クライアント アプリケーションは、レジストリ キーを開くし、直接文字列全体を読み取る。 ドライバーは、2 つの方法のいずれかでこのレジストリ エントリを設定できます。

-   ドライバーでデバイスの INF ファイルのエントリのインストール時に指定できます。

-   ドライバーは、そのフィルター初期化ルーチンの実行中に、エントリを読み込むことができます。

名前の GUID は省略可能です。 ドライバーが設定されている場合、**名前**guid KSCOMPONENTID でメンバー\_NULL の値に、デバイスのフレンドリ名を提供する WDMAud、 *xxx*GetDevCaps 関数には、この名前をコピーする、**szPname**機能の構造体のメンバー。

場合は、フィルター、KSPROPERTY のハンドラー公開しません\_全般\_COMPONENTID プロパティ、WDMAud KSCOMPONENTID 構造体からのデータの代わりに既定値を使用します。 機能の構造体の従来の部分の既定値は次のとおりです。

-   **wMid** = MM\_MICROSOFT

-   **監視**= 次の一覧からデバイス クラス。MM\_MSFT\_WDMAUDIO\_WAVEOUT MM\_MSFT\_WDMAUDIO\_WAVEIN MM\_MSFT\_WDMAUDIO\_MIDIOUT MM\_MSFT\_WDMAUDIO\_MIDIIN MM\_MSFT\_WDMAUDIO\_ミキサー MM\_MSFT\_WDMAUDIO\_AUX
-   **vDriverVersion** = 0x050a (for Windows XP の場合) または 0x0500 にならなければなりません (以前の Windows XP の場合)

Windows のリリースで Windows XP より前の機能の構造の従来のメンバーは常に設定上記の既定値。 Windows xp 以降、拡張機能の既定値はような。

-   **NameGuid** GUID =\_NULL

-   INIT\_MMREG\_MID ((& a)**ManufacturerGuid**、 **wMid**)

-   INIT\_MMREG\_PID ((& a)**ProductGuid**、**監視**)

INIT\_MMREG\_MID および INIT\_MMREG\_Ksmedia.h で上記の PID マクロが定義されます。 これらのマクロは、製造元と製品の Id での変換に使用、 **wMid**と**監視**メンバーに読み込まれている Guid を**ManufacturerGuid**と**ProductGuid**メンバー。

 

 




