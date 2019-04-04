---
title: 標準オプション
description: 標準オプションでは、標準的な機能に関連付けられたと GPD 言語によって認識される定義済みの名前によって識別されます。
ms.assetid: db4578c1-0954-4c51-a11a-923ab7df2b5b
keywords:
- WDK Unidrv、標準のプリンター オプション
- 標準オプション WDK Unidrv
ms.date: 01/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: 317a195cc757606fc1684a23b044a31ac4ed1caa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571968"
---
# <a name="standard-options"></a>標準オプション


関連付けられている標準的なオプションは[標準機能](standard-features.md)します。 GPD 言語によって認識される定義済みの名前によって識別されます。 これらの名前を表す文字列のリソース識別子は、stdnames.gpd、Microsoft Windows Driver Kit (WDK) での指定に含まれます。 

> [!IMPORTANT]
> このリソースは、いくつかの言語と国で利用できない可能性があります。

次の表では、標準的な機能ごとに許可されている標準的なオプション名を示します。 これらの名前を引数として使用**\*オプション**エントリ。 印刷スキーマ オプションのキーワードを含める機能は、印刷スキーマ オプションのキーワードに自動的にマップされているオプション名です。 マップすることも GPD オプション印刷スキーマのキーワードを手動でを使用して、 **PrintSchemaKeywordMap**属性。 印刷スキーマは、Microsoft Windows SDK に記載されています。

<table>
    <tbody>
        <tr>
            <td><b>機能名</b></td>
            <td><b>標準的なオプション名</b></td>
            <td><b>既定の印刷スキーマ オプションのキーワード</b></td>
            <td><b>カスタマイズされたオプションが許可されているか。</b></td>
        </tr>
        <tr>
            <td><b>部単位印刷します。</b></td>
            <td>無効<br>ON</td>
            <td>丁合いなし<br>部単位で印刷</td>
            <td>いいえ</td>
        </tr>
        <tr>
            <td><b>返さ</b></td>
            <td colspan="2">標準オプションなし</td>
            <td>はい<br>参照してください<a href="https://docs.microsoft.com/windows-hardware/drivers/print/handling-color-formats">色の書式設定の処理</a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/print/controlling-image-quality">画質を制御する</a>します。</td>
        </tr>
        <tr>
            <td><b>Duplex</b></td>
            <td>水平方向<br>垂直<br>なし</td>
            <td>TwoSidedShortEdge<br>TwoSidedLongEdge<br>OneSided</td>
            <td>いいえ</td>
        </tr>
        <tr>
            <td><b>ハーフトーン</b></td>
            <td colspan="2">HT_PATSIZE_2x2<br>HT_PATSIZE_2x2_M<br>HT_PATSIZE_4x4<br>HT_PATSIZE_4x4_M<br>HT_PATSIZE_6x6<br>HT_PATSIZE_6x6_M<br>HT_PATSIZE_8x8<br>HT_PATSIZE_8x8_M<br>HT_PATSIZE_10x10<br>HT_PATSIZE_10x10_M<br>HT_PATSIZE_12x12<br>HT_PATSIZE_12x12_M<br>HT_PATSIZE_14x14<br>HT_PATSIZE_14x14_M<br>HT_PATSIZE_16x16<br>HT_PATSIZE_16x16_M<br>HT_PATSIZE_SUPERCELL<br>HT_PATSIZE_SUPERCELL_M<br>HT_PATSIZE_AUTO</td>
            <td>はい<br>参照してください<a href="https://docs.microsoft.com/windows-hardware/drivers/print/halftoning-with-unidrv">Unidrv のハーフトーン</a>します。</td>
        </tr>
        <tr>
            <td rowspan="5"><b>InputBin</b></td>
            <td>自動<br>カセット<br>ENVFEED<br>ENVMANUAL</td>
            <td>カセット</td>
            <td rowspan="5">はい</td>
        </tr>
        <tr>
            <td>FORMSOURCE</td>
            <td>AutoSelect</td>
        </tr>
        <tr>
            <td>LARGECAPACITY<br>LARGEFMT<br>低い</td>
            <td>高</td>
        </tr>
        <tr>
            <td>手動<br>中間<br>SMALLFMT</td>
            <td>手動</td>
        </tr>
        <tr>
            <td>供給<br>上限</td>
            <td>供給</td>
        </tr>
        <tr>
            <td><b>メディアの種類</b></td>
            <td>光沢紙<br>標準<br>透過性</td>
            <td>PhotographicGlossy<br>プレーン<br>透過性</td>
            <td>はい<br>参照してください<a href="https://docs.microsoft.com/windows-hardware/drivers/print/controlling-image-quality">画質を制御する</a>します。</td>
        </tr>
        <tr>
            <td><b>メモリ</b></td>
            <td colspan="2">標準オプションなし</td>
            <td>はい</td>
        </tr>
        <tr>
            <td><b>印刷の向き</b></td>
            <td>縦向き<br>LANDSCAPE_CC90<br>LANDSCAPE_CC270<br><br>後者の 2 つのオプションの詳細については、<a href="https://docs.microsoft.com/windows-hardware/drivers/print/specifying-paper-orientation">用紙の向きを指定する</a>を参照してください。</td>
            <td>縦向き<br>横向き<br>ReverseLandscape</td>
            <td>いいえ</td>
        </tr>
        <tr>
            <td><b>PageProtect</b></td>
            <td colspan="2">ON<br>無効</td>
            <td>いいえ</td>
        </tr>
        <tr>
            <td rowspan="29"><b>用紙サイズ</b></td>
            <td>10 X 11 インチ<br>10 X 14<br>11 X 17 インチ</td>
            <td>NorthAmerica10x11<br>NorthAmerica10x14<br>NorthAmerica11x17</td>
            <td rowspan="29">はい<br><b>注</b>カスタマイズされた名前で指定された長さを超えない<b>CCHFORMNAME</b>で<b>wingdi.h</b>します。</td>
        </tr>
        <tr>
            <td colspan="2">12 X 11 インチ<br>15 X 11 インチ</td>
        </tr>
        <tr>
            <td>9 X 11 インチ<br>A_PLUS</td>
            <td>NorthAmerica9x11<br>NorthAmericaSuperA</td>
        </tr>
        <tr>
            <td>A2<br>A3</td>
            <td>ISOA2<br>ISOA3</td>
        </tr>
        <tr>
            <td>A3_EXTRA<br>A3_EXTRA_TRANSVERSE</td>
            <td>ISOA3Extra</td>
        </tr>
        <tr>
            <td>A3_ROTATED<br>A3_TRANSVERSE</td>
            <td>ISOA3Rotated</td>
        </tr>
        <tr>
            <td>A4<br>A4_EXTRA<br>A4_PLUS</td>
            <td>ISOA4<br>ISOA4Extra<br>OtherMetricA4Plus</td>
        </tr>
        <tr>
            <td>A4_ROTATED<br>A4_TRANSVERSE</td>
            <td>ISOA4Rotated</td>
        </tr>
        <tr>
            <td colspan="2">A4SMALL</td>
        </tr>
        <tr>
            <td>A5<br>A5_EXTRA</td>
            <td>ISOA5<br>ISOA5Extra</td>
        </tr>
        <tr>
            <td>A5_ROTATED<br>A5_TRANSVERSE</td>
            <td>ISOA5Rotated</td>
        </tr>
        <tr>
            <td>A6<br>A6_ROTATED<br>B_PLUS<br>B4<br>B4_JIS_ROTATED<br>B5<br>B5_EXTRA</td>
            <td>ISOA6<br>ISOA6Rotated<br>NorthAmericaSuperB<br>JISB4<br>JISB4Rotated<br>JISB5<br>ISOB5Extra</td>
        </tr>
        <tr>
            <td>B5_JIS_ROTATED<br>B5_TRANSVERSE</td>
            <td>JISB5Rotated</td>
        </tr>
        <tr>
            <td>B6_JIS<br>B6_JIS_ROTATED</td>
            <td>JISB6<br>JISB6Rotated</td>
        </tr>
        <tr>
            <td>CSHEET<br>CUSTOMSIZE</td>
            <td>NorthAmericaCSheet</td>
        </tr>
        <tr>
            <td>DBL_JAPANESE_POSTCARD<br>DBL_JAPANESE_POSTCARD_ROTATED<br>DSHEET<br>ENV_10<br>ENV_11<br>ENV_12<br>ENV_14<br>ENV_9<br>ENV_B4<br>ENV_B5</td>
            <td>JapanDoubleHagakiPostcard<br>JapanDoubleHagakiPostcardRotated<br>NorthAmericaDSheet<br>NorthAmericaNumber10Envelope<br>NorthAmericaNumber11Envelope<br>NorthAmericaNumber12Envelope<br>NorthAmericaNumber14Envelope<br>NorthAmericaNumber9Envelope<br>ISOB4Envelope<br>ISOB5Envelope</td>
        </tr>
        <tr>
            <td colspan="2">ENV_B6</td>
        </tr>
        <tr>
            <td>ENV_C3<br>ENV_C4<br>ENV_C5<br>ENV_C6<br>ENV_C65<br>ENV_DL<br>ENV_INVITE<br>ENV_ITALY<br>ENV_MONARCH<br>ENV_PERSONAL<br>E シート<br>役員<br>FANFOLD_LGL_GERMAN</td>
            <td>ISOC3Envelope<br>ISOC4Envelope<br>ISOC5Envelope<br>ISOC6Envelope<br>ISOC6C5Envelope<br>ISODLEnvelope<br>OtherMetricInviteEnvelope<br>OtherMetricItalianEnvelope<br>NorthAmericaMonarchEnvelope<br>NorthAmericaPersonalEnvelope<br>NorthAmericaESheet<br>NorthAmericaExecutive<br>NorthAmericaGermanLegalFanfold</td>
        </tr>
        <tr>
            <td>FANFOLD_STD_GERMAN<br>FANFOLD_US</td>
            <td>NorthAmericaGermanStandardFanfold</td>
        </tr>
        <tr>
            <td>FOLIO<br>ISO_B4<br>JAPANESE_POSTCARD<br>JAPANESE_POSTCARD_ROTATED<br>JENV_CHOU3<br>JENV_CHOU3_ROTATED<br>JENV_CHOU4<br>JENV_CHOU4_ROTATED<br>JENV_KAKU2<br>JENV_KAKU2_ROTATED<br>JENV_KAKU3<br>JENV_KAKU3_ROTATED<br>JENV_YOU4<br>JENV_YOU4_ROTATED</td>
            <td>OtherMetricFolio<br>ISOB4<br>JapanHagakiPostcard<br>JapanHagakiPostcardRotated<br>JapanChou3Envelope<br>JapanChou3EnvelopeRotated<br>JapanChou4Envelope<br>JapanChou4EnvelopeRotated<br>JapanKaku2Envelope<br>JapanKaku2EnvelopeRotated<br>JapanKaku3Envelope<br>JapanKaku3EnvelopeRotated<br>JapanYou4Envelope<br>JapanYou4EnvelopeRotated</td>
        </tr>
        <tr>
            <td colspan="2">台帳</td>
        </tr>
        <tr>
            <td>法的<br>LEGAL_EXTRA<br>文字</td>
            <td>NorthAmericaLegal<br>NorthAmericaLegalExtra<br>NorthAmericaLetter</td>
        </tr>
        <tr>
            <td>一覧<br>LETTER_EXTRA_TRANSVERSE</td>
            <td>NorthAmericaLetterExtra</td>
        </tr>
        <tr>
            <td>LETTER_PLUS</td>
            <td>NorthAmericaLetterPlus</td>
        </tr>
        <tr>
            <td>LETTER_ROTATED<br>LETTER_TRANSVERSE</td>
            <td>NorthAmericaLetterRotated</td>
        </tr>
        <tr>
            <td colspan="2">LETTERSMALL</td>
        </tr>
        <tr>
            <td>注<br>P16K<br>P16K_ROTATED<br>P32K<br>P32K_ROTATED</td>
            <td>NorthAmericaNote<br>PRC16K<br>PRC16KRotated<br>PRC32K<br>PRC32KRotated</td>
        </tr>
        <tr>
            <td>P32KBIG<br>P32KBIG_ROTATED</td>
            <td>PRC32KBig</td>
        </tr>
        <tr>
            <td>PENV_1<br>PENV_1_ROTATED<br>PENV_10<br>PENV_10_ROTATED<br>PENV_2<br>PENV_2_ROTATED<br>PENV_3<br>PENV_3_ROTATED<br>PENV_4<br>PENV_4_ROTATED<br>PENV_5<br>PENV_5_ROTATED<br>PENV_6<br>PENV_6_ROTATED<br>PENV_7<br>PENV_7_ROTATED<br>PENV_8<br>PENV_8_ROTATED<br>PENV_9<br>PENV_9_ROTATED<br>QUARTO<br>ステートメント<br>TABLOID<br>TABLOID_EXTRA</td>
            <td>PRC1Envelope<br>PRC1EnvelopeRotated<br>PRC10Envelope<br>PRC10EnvelopeRotated<br>PRC2Envelope<br>PRC2EnvelopeRotated<br>PRC3Envelope<br>PRC3EnvelopeRotated<br>PRC4Envelope<br>PRC4EnvelopeRotated<br>PRC5Envelope<br>PRC5EnvelopeRotated<br>PRC6Envelope<br>PRC6EnvelopeRotated<br>PRC7Envelope<br>PRC7EnvelopeRotated<br>PRC8Envelope<br>PRC8EnvelopeRotated<br>PRC9Envelope<br>PRC9EnvelopeRotated<br>NorthAmericaQuarto<br>NorthAmericaStatement<br>NorthAmericaTabloid<br>NorthAmericaTabloidExtra</td>
        </tr>
        <tr>
            <td><b>解決方法</b></td>
            <td colspan="2">標準オプションなし</td>
            <td>はい</td>
        </tr>
    </tbody>
</table>


## <a name="related-topics"></a>関連トピック


[イメージ品質を制御します。](controlling-image-quality.md)  
[ハーフトーン Unidrv で](halftoning-with-unidrv.md)  
[用紙の向きを指定します。](specifying-paper-orientation.md)  
[標準的な機能](standard-features.md)  





