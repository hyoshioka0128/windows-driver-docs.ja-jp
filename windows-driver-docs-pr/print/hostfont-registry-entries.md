---
title: ホストフォント レジストリ エントリ
description: ホストフォント レジストリ エントリ
ms.assetid: f7ce2591-197a-4094-8b21-5e0cc48506ea
keywords:
- PostScript プリンター ドライバー WDK を印刷する HostFontXxx レジストリ エントリ
- Pscript WDK 印刷、HostFontXxx レジストリ エントリ
- レジストリ エントリの HostFontXxx WDK Pscript
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf5315ae20c417bddc4aca6391adcb2e7b85164c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378590"
---
# <a name="hostfont-registry-entries"></a>ホストフォント レジストリ エントリ





OEM プラグイン %hostfont% 対応 PostScript インタープリターに一連のフォントと Pscript5 ドライバーに印刷ジョブの過程でダウンロードできるものと同じですが、使用できるを CIDFonts Pscript5 ドライバーに通知できます。 通知のフォントがこのように処理するは、レジストリ キーを配置することによって行われます。 Pscript5 ドライバーは、新しい情報がレジストリを確認します。 ときにその[ **DrvEnablePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)関数が呼び出されます。 プラグインことを確認、PDEV を有効にするには、現在のデータが。

次の表は、%hostfont% レジストリ エントリの名前、その種類、および値を示します。 プラグインの OEM は、これらのエントリの名前を設定する SetPrinterData (Microsoft Windows SDK のドキュメントで説明) を呼び出す必要があります。 HostFont*Xxx*エントリの名前は相互に排他的です。 つまり、任意の時点で、レジストリに次のエントリの名前の 1 つだけ存在できます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>エントリ名</th>
<th>型と値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>HostFontExceptCIDFonts</p></td>
<td><p>REG_BINARY</p>
<p>含めることができます、PostScript フォントメトリックファイル名を含む、複数の NULL で終わる ASCII 文字列です。 最終的な文字列は、追加の null 文字で終了します。</p></td>
<td><p>HostFontExceptFonts に似ていますが、CIDFonts に適用されます。</p></td>
</tr>
<tr class="even">
<td><p>HostFontExceptFonts</p></td>
<td><p>REG_BINARY</p>
<p>含めることができます、PostScript フォント名を含む、複数の NULL で終わる ASCII 文字列です。 最終的な文字列は、追加の null 文字で終了します。</p></td>
<td><p>Pscript5 ドライバー「を表示しない」として使用可能なおよび %hostfont% 対応 PostScript インタープリターで、フォントに同じフォント。 Pscript5 ドライバーでは、これらのフォントをダウンロードします。</p></td>
</tr>
<tr class="odd">
<td><p>HostFontHasMostFonts</p></td>
<td><p>REG_DWORD</p>
<p>値を指定できます。</p></td>
<td><p>すべてのフォントを %hostfont として扱う-できません。 このエントリの名前は、任意の値と共に表示され、Pscript5 ドライバーでは、任意のフォントはダウンロードされません。</p></td>
</tr>
<tr class="even">
<td><p>HostFontIncludesCIDFonts</p></td>
<td><p>REG_BINARY</p>
<p>含めることができます、PostScript フォントメトリックファイル名を含む、複数の NULL で終わる ASCII 文字列です。 最終的な文字列は、追加の null 文字で終了します。</p></td>
<td><p>HostFontIncludesFonts に似ていますが、CIDFonts に適用されます。</p></td>
</tr>
<tr class="odd">
<td><p>HostFontIncludesFonts</p></td>
<td><p>REG_BINARY</p>
<p>含めることができます、PostScript フォント名を含む、複数の NULL で終わる ASCII 文字列です。 最終的な文字列は、追加の null 文字で終了します。</p></td>
<td><p>使用可能なおよび %hostfont% 対応 PostScript インタープリターで同じであるだけのものと、「認識」を Pscript5 ドライバー フォント。 Pscript5 ドライバーでは、これらのフォントはダウンロードされません。</p></td>
</tr>
</tbody>
</table>

 

### <a name="additional-notes-on-hostfont-registry-entry-names"></a>Hostfont レジストリ エントリの名前で追加の注意事項

HostFontExceptFonts は REG\_TTF ベース、OTF ベースまたは PFB ベースのエンコードおよびグリフ-名前-ベースのフォントの PostScript findfont 名を含む NULL で終わる 1 バイト文字列のシーケンスで構成されるバイナリ データ。 名前が; 任意の順序で一覧表示します。最後の名前は、2 つの Null で終了し、後の Null バイトがないです。 HostFontHasMostFonts が検出されなかった場合にのみ、このエントリの名前がチェックされます。

割り当てられている任意の値を持つ HostFontHasMostFonts キーが存在することを示し、ドライバーと想定されますをすべて TTF ベース、OTF ベース、PostScript フォントまたはとしてフォントメトリックファイル形式として PFB ベースのホストのフォントは、「ネイティブ」形式では、使用可能です適切なターゲット インタープリターです。

HostFontIncludesFonts は HostFontExceptFonts に似ていますが、ターゲットのインタープリターで使用できる PostScript フォント名が明示的に一覧表示されます。

 

 




