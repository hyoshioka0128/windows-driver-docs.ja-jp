---
title: Pscript5 キーワード
description: Pscript5 キーワード
ms.assetid: a5f4384a-8d78-4dc6-969b-f7a1fa6cb5e7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67764e4db2fea599b805c81e6a094e83e66b6a8a
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57463874"
---
# <a name="pscript5-keywords"></a>Pscript5 キーワード


渡されるヘルパー インターフェイス、Pscript5 からプラグイン機能とオプションの名前は、PPD ファイルで定義されている機能とオプションの文字列名です。 さらに、予約済みの特定の文字列は、PPD ファイルでは表されない Pscript5 core ドライバーに実装されている機能に対して定義されます。 すべての次の表に記載されているオプションで決定できます実行時に呼び出すことに注意してください。 **EnumOptions**します。 ただし、範囲、数値の設定が必要な機能について、 **EnumOptions**メソッドは、 **NULL**値でその*pOptionList*パラメーターと、0 の数オプション\* *pdwNumOptions*します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>機能名</th>
<th>および</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>%AddEuro</p></td>
<td><p></p>
"False"の"true"</td>
<td><p>デバイス フォントには、ユーロの通貨記号を追加します。</p>
<p>プリンター付箋。</p>
<p>PostScript レベル 2 が必要です。 注 1 を次の次の表を参照してください。</p></td>
</tr>
<tr class="even">
<td><p>% CtrlDAfter</p></td>
<td><p></p>
"False"の"true"</td>
<td><p>各ジョブの完了後に、CTRL + D を送信します。</p>
<p>プリンター付箋。</p></td>
</tr>
<tr class="odd">
<td><p>% CtrlDBefore</p></td>
<td><p></p>
"False"の"true"</td>
<td><p>各ジョブの前に、CTRL + D を送信します。</p>
<p>プリンター付箋。</p></td>
</tr>
<tr class="even">
<td><p>%CustomPageSize</p></td>
<td><p>複雑な形式は、カスタムのページ サイズのオプションであります。 注 2 を次の次の表を参照してください。</p></td>
<td><p>読み取りまたはカスタム ページのサイズ設定を指定します。 原因でこの機能を設定、 <strong>dmPaperSize</strong> 、public のメンバー <a href="https://msdn.microsoft.com/library/windows/hardware/ff552837" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552837)"> <strong>DEVMODEW</strong> </a> DMPAPER_CUSTOMSIZE (PS のカスタム サイズを示す)、および設定にリセットする構造体DM_PAPERSIZE ビット フラグです。 この機能は、読み取り専用パブリック DEVMODEW 構造体は、カスタム用紙サイズが使用されていることを示すかどうか。</p>
<p>ドキュメントの付箋。</p></td>
</tr>
<tr class="odd">
<td><p>% GraphicsAsTrueGray</p></td>
<td><p></p>
"False"の"true"</td>
<td><p>PostScript 灰色グレー グラフィックスに変換します。</p>
<p>プリンター付箋。</p></td>
</tr>
<tr class="even">
<td><p>% JobTimeout</p></td>
<td><p>数値 (注 3 をこのテーブルに次を参照してください)</p>
<p>「2147483647」を「0」</p></td>
<td><p>ジョブのタイムアウトを秒単位で指定します。</p>
<p>プリンター付箋。</p></td>
</tr>
<tr class="odd">
<td><p>% MaxFontSizeAsBitmap</p></td>
<td><p>数値 (注 3 を参照してください)</p>
<p>「32767」を「0」</p></td>
<td><p>ビットマップとしてダウンロードするフォントの最大サイズを指定します。</p>
<p>プリンター付箋。</p></td>
</tr>
<tr class="even">
<td><p>% MetafileSpooling</p></td>
<td><p></p>
"False"の"true"</td>
<td><p>EMF スプールを有効にします。 有効にするのにはこの機能を有効にすると、<strong>印刷機能の高度な</strong>UI オプション。 この機能が小冊子の印刷、照合、およびページの順序と対話する制約を持つことに注意してください。 これらの機能のいずれかに対して解決するときにこの機能には最低の優先順位が与えられます。</p>
<p>ドキュメントの付箋。</p></td>
</tr>
<tr class="odd">
<td><p>%MinFontAsOutline</p></td>
<td><p>数値 (注 3 をこのテーブルに次を参照してください)</p>
<p>「32,767」を「0」</p></td>
<td><p>アウトラインとしてダウンロードする必要があります最小のフォント サイズを指定します。</p>
<p>プリンター付箋。</p></td>
</tr>
<tr class="even">
<td><p>% ミラーリング</p></td>
<td><p></p>
"False"の"true"</td>
<td><p>ミラーが水平方向の座標を反転して出力します。</p>
<p>ドキュメントの付箋。</p></td>
</tr>
<tr class="odd">
<td><p>% の負の値</p></td>
<td><p></p>
"False"の"true"</td>
<td><p>印刷ページに黒と白の領域を反転します。</p>
<p>ドキュメントの付箋。</p>
<p>モノクロ プリンター、色ではない必要があります。</p></td>
</tr>
<tr class="even">
<td><p>% の向き</p></td>
<td><p></p>
「Portrait」「Landscape」"RotatedLandscape"</td>
<td><p>出力方向を指定します。 プライベートおよびパブリックの両方を変更するこの手法を使用して、印刷の向きを構成する<a href="https://msdn.microsoft.com/library/windows/hardware/ff552837" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552837)"> <strong>DEVMODEW</strong> </a>で使用する場合、値を構造体、 <strong>IPrintCoreHelperPS</strong>インターフェイスです。 この警告には適用されません、 <strong>IPrintCoreUI2</strong>インターフェイス。</p>
<p>ドキュメントの付箋。</p></td>
</tr>
<tr class="odd">
<td><p>% OutputFormat</p></td>
<td><p></p>
「可搬性」の"EPS"「アーカイブ」の「速度」</td>
<td><p>PostScript 出力形式を指定します。 出力形式の動作は定義されていると同じ<strong>IPrintCoreUI2</strong>します。</p>
<p>ドキュメントの付箋。</p></td>
</tr>
<tr class="even">
<td><p>% OutputProtocol</p></td>
<td><p></p>
"ASCII"、"BCP""TBCP"「バイナリ」</td>
<td><p>プリンターで印刷ジョブに使用するプロトコルを指定します。 BCP と TBCP オプションはサポートされている場合にのみ使用できます。 <strong>EnumOptions</strong>サポートされている値のみが含まれています。 出力のプロトコルは、「プロトコル」グローバル属性をチェックしても確認できます。</p>
<p>プリンター付箋。</p></td>
</tr>
<tr class="odd">
<td><p>% OutputPSLevel</p></td>
<td><p></p>
"1" "2" "3"</td>
<td><p>この印刷ジョブを生成する PostScript 言語レベルを指定します。 使用可能なオプションは、同じか、または"LanguageLevel"グローバル属性で指定されているデバイスの言語レベルよりも小さい値に制限されます。</p>
<p>ドキュメントの付箋。</p>
<p>PostScript レベル 2 またはそれ以降が必要です。 注 1 を次の次の表を参照してください。</p></td>
</tr>
<tr class="even">
<td><p>%PageOrder</p></td>
<td><p></p>
"FrontToBack""BackToFront"</td>
<td><p>ページを印刷する順序を指定します。 EMF スプールが利用できない場合は、この機能は表示されませんを呼び出すときに<strong>EnumFeatures</strong>、読み取りまたはこの機能は E_FAIL を返しますの設定を記述しようとします。 また、BackToFront は %metafilespooling の機能が False に設定されている場合に制限されます。</p>
<p>ドキュメントの付箋。</p></td>
</tr>
<tr class="odd">
<td><p>% PagePerSheet</p></td>
<td><p></p>
「1」、「2」、「4」、「6」、「9」、「16」、「小冊子」</td>
<td><p>小冊子印刷は、二重化が使用可能な場合にのみ使用できます。 「小冊子」オプションを設定するでない場合に既にオンにする二重化します。 双方向がになっている小冊子の印刷が選択されている場合は、オプションは 2 枚に強制されます。 メタファイル スプールを無効にした場合は、小冊子印刷で制約として表されます。 プリント プロセッサが使用されているため、EMF スプールが利用できない場合は、小冊子の印刷は使用できません。 この場合、小冊子の印刷は表示されませんで<strong>EnumOptions</strong>と<strong>SetOptions</strong>呼び出し元は、"%pagepersheet"を要求した場合は E_FAIL を返します「小冊子」に設定されます。</p>
<p>ドキュメントの付箋。</p></td>
</tr>
<tr class="even">
<td><p>% PSErrorHandler</p></td>
<td><p></p>
"False"の"true"</td>
<td><p>PostScript エラー ハンドラーを送信します。</p>
<p>ドキュメントの付箋。</p></td>
</tr>
<tr class="odd">
<td><p>% PSMemory</p></td>
<td><p>数値 (注 3 をこのテーブルに次を参照してください)</p>
<p>レベル 1 の PostScript プリンター の範囲は「2097151」から「172」です。</p>
<p>Postscript レベル 2 または 3 つのプリンターの場合は、範囲は「2097151」から「249」です。</p></td>
<td><p>デバイスで使用できる仮想メモリのキロバイト数を指定します。 キロバイト単位でバイトではなく、値が示されることに注意してください。 また、レベル 1 およびレベル 2 のプリンターの有効な範囲が異なることに注意してください。 これらの範囲外の値を設定しようとは、E_FAIL HRESULT で失敗します。</p>
<p>プリンター付箋。</p></td>
</tr>
<tr class="even">
<td><p>% TextTrueGray</p></td>
<td><p></p>
"False"の"true"</td>
<td><p>PostScript 灰色に灰色のテキストに変換します。</p>
<p>プリンター付箋。</p></td>
</tr>
<tr class="odd">
<td><p>% TTDownloadFormat</p></td>
<td><p></p>
「自動」「説明」"Bitmap""NativeTrueType"</td>
<td><p>形式をダウンロードする TrueType フォントを指定します。 NativeTrueType が使用可能で一覧表示されている<strong>EnumOptions</strong> "TTRasterizer"グローバルな属性"Type42"のサポートを指定する場合にのみです。</p>
<p>ドキュメントの付箋。</p></td>
</tr>
<tr class="even">
<td><p>WaitTimeout %</p></td>
<td><p>数値 (注 3 をこのテーブルに次を参照してください)</p>
<p>「2147483647」を「0」</p></td>
<td><p>秒の待機のタイムアウト値を指定します。</p>
<p>プリンター付箋。</p></td>
</tr>
</tbody>
</table>

 

**注**  機能の要件が満たされていない場合は 1 に、その機能は表示されませんで**EnumFeatures**、により、取得、またはその機能を設定しようと E\_失敗が返されます。 これは、%addeuro、%、負の値、および %outputpslevel に適用されます。

 

**注**   2 (%custompagesize) カスタム ページのサイズの形式は、記載されているのと同じ**IPrintCoreUI2**します。 **EnumOptions**オプションの空のリストを返します。

 

**注**   3 つの数値の値は数字の文字のみが含まれている ANSI 文字列として表されます。 サインを指定することはできません。 たとえば、「300」が有効では、「-20」、「20.5」および"から +300 の整数"はすべて有効です。 これは、%jobtimeout、%maxfontsizeasbitmap、MinFontAsOutline %、%psmemory、および %waittimeout に適用されます。

 

 

 




