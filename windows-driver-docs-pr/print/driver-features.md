---
title: ドライバー機能
description: ドライバー機能
ms.assetid: 56efebda-970f-4885-9c5f-1eac97aecfdd
ms.date: 01/30/2019
ms.localizationpriority: medium
ms.openlocfilehash: 95b02d3d8d8f1b51ebea6cc41ffc02e0c1b1d461
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387264"
---
# <a name="driver-features"></a>ドライバー機能

ドライバーの機能は非 PPD 機能、ドライバーによって合成されますです (たとえば、 **%outputformat**機能)。 PPD 機能キーワードと名前の競合を避けるためには、すべてのドライバー機能キーワード名は「%」文字で前にします。 ドライバーの機能またはオプションのキーワードも大文字小文字を区別します。

ドライバーがサポートする機能のキーワードをすべてのドライバーの一覧を取得するには、プラグインを呼び出すことができます、EnumFeatures ドライバーの機能と PPD 機能の両方を含む機能キーワードの一覧が返されます。 プラグインし検索できますドライバー機能の一覧を取得する「%」プレフィックスで始まる機能キーワード名。

次の表では、現在サポートされているドライバーの機能を示します。 テーブル内の各行は、ドライバー機能のキーワードの一覧、サポートされているオプションが表示されます、EnumOptions への呼び出しで、機能のオプションを列挙できるかどうかを示す、および簡単な説明をします。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>ドライバーの機能</th>
<th>サポートされているオプション</th>
<th>列挙型のオプションですか。</th>
<th>説明とコメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>%AddEuro</strong></p></td>
<td><p>"True"</p>
<p>"False"</p></td>
<td><p>〇</p></td>
<td><p>デバイス フォントには、ユーロの通貨記号を追加します。</p>
<p>この機能は、レベル 2 + プリンターのみサポートされます。 レベル 1 のプリンター <strong>SetOptions</strong> 、この機能は無視されますと<strong>GetOptions</strong>常に"False"を返します。</p>
<p>プリンター固定</p></td>
</tr>
<tr class="even">
<td><p><strong>% CtrlDAfter</strong></p></td>
<td><p>"True"</p>
<p>"False"</p></td>
<td><p>〇</p></td>
<td><p>ジョブの後に Ctrl-D を送信します。</p>
<p>プリンター固定</p></td>
</tr>
<tr class="odd">
<td><p><strong>% CtrlDBefore</strong></p></td>
<td><p>"True"</p>
<p>"False"</p></td>
<td><p>〇</p></td>
<td><p>各ジョブの前に Ctrl-D を送信します。</p>
<p>プリンター固定</p></td>
</tr>
<tr class="even">
<td><p><strong>%CustomPageSize</strong></p></td>
<td><p>詳細については、下の注 1 を参照してください。</p></td>
<td><p>X</p></td>
<td><p>PostScript カスタム ページのサイズ パラメーターを指定します。</p>
<p>固定ドキュメント</p></td>
</tr>
<tr class="odd">
<td><p><strong>%GraphicsTrueGray</strong></p></td>
<td><p>"True"</p>
<p>"False"</p></td>
<td><p>〇</p></td>
<td><p>PostScript 灰色グレー グラフィックスに変換します。</p>
<p>プリンター固定</p></td>
</tr>
<tr class="even">
<td><p><strong>%JobTimeout</strong></p></td>
<td><p>NULL で終わる ANSI 文字列の 0 ~ 2,147, 483,647 の範囲で、タイムアウトの秒数の符号なし整数を表す 10 進文字を含んでいます。</p>
<p><strong>SetOptions</strong>、余分なタブまたは空白文字の前に、または後の 10 進数字が許可されている場合がの記号は許可されません。</p></td>
<td><p>X</p></td>
<td><p>ジョブのタイムアウト値を指定します。</p>
<p>プリンター固定</p></td>
</tr>
<tr class="odd">
<td><p><strong>% MaxFontSizeAsBitmap</strong></p></td>
<td><p>NULL で終わる ANSI 文字列の 0 ~ 32,767 の範囲内のピクセル数の符号なし整数を表す 10 進文字を含んでいます。</p>
<p><strong>SetOptions</strong>、余分なタブまたは空白文字の前に、または後の 10 進数字が許可されている場合がの記号は許可されません。</p></td>
<td><p>X</p></td>
<td><p>ビットマップとしてダウンロードするフォントの最大サイズを指定します。</p>
<p>プリンター固定</p></td>
</tr>
<tr class="even">
<td><p><strong>%MetafileSpooling</strong></p></td>
<td><p>"True"</p>
<p>"False"</p></td>
<td><p>〇</p></td>
<td><p>高度な印刷機能を有効または無効にします。</p>
<p>固定ドキュメント</p>
<p>詳細については、下の注 2 を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><strong>%MinFontSizeAsOutline</strong></p></td>
<td><p>NULL で終わる ANSI 文字列の 0 ~ 32,767 の範囲内のピクセル数の符号なし整数を表す 10 進文字を含んでいます。</p>
<p><strong>SetOptions</strong>、余分なタブまたは空白文字の前に、または後の 10 進数字が許可されている場合がの記号は許可されません。</p></td>
<td><p>X</p></td>
<td><p>アウトラインとしてダウンロードする最小のフォント サイズを指定します。</p>
<p>プリンター固定</p></td>
</tr>
<tr class="even">
<td><p><strong>% ミラーリング</strong></p></td>
<td><p>"True"</p>
<p>"False"</p></td>
<td><p>〇</p></td>
<td><p>ミラーが水平方向の座標を反転して出力します。</p>
<p>固定ドキュメント</p></td>
</tr>
<tr class="odd">
<td><p><strong>%Negative</strong></p></td>
<td><p>"True"</p>
<p>"False"</p></td>
<td><p>〇</p></td>
<td><p>負の値の出力を生成するには、白と黒の値を反転します。 この機能は、モノクロ プリンターのみサポートされます。 カラー プリンターの<strong>SetOptions</strong> 、この機能を無視し、 <strong>GetOptions</strong>常に"False"を返します。</p>
<p>固定ドキュメント</p></td>
</tr>
<tr class="even">
<td><p><strong>%Orientation</strong></p></td>
<td><p>"Portrait", "Landscape", "RotatedLandscape"</p></td>
<td><p>〇</p></td>
<td><p>出力方向を指定します。</p>
<p>固定ドキュメント</p></td>
</tr>
<tr class="odd">
<td><p><strong>%OutputFormat</strong></p></td>
<td><p>「速度」、「移植性」、"EPS"、「アーカイブ」</p></td>
<td><p>〇</p></td>
<td><p>PostScript 出力形式を指定します。</p>
<p>固定ドキュメント</p>
<p>詳細については、下の注 5 を参照してください。</p></td>
</tr>
<tr class="even">
<td><p><strong>%OutputProtocol</strong></p></td>
<td><p>"ASCII"、"BCP"、"TBCP"、"Binary"</p></td>
<td><p>〇</p></td>
<td><p>プリンターで印刷ジョブを使用するプロトコルを指定します。 PostScript プリンターは、これらのオプションは常に利用するために、"ASCII"、"Binary"をサポートするためと見なされます。 "BCP"と"TBCP"オプションはサポートされている場合にのみ使用できます。 (これを見つけるには、確認、グローバル属性 [プロトコル]。</p>
<p>プリンター固定</p></td>
</tr>
<tr class="odd">
<td><p><strong>%OutputPSLevel</strong></p></td>
<td><p>"1", "2", "3"</p></td>
<td><p>X</p></td>
<td><p>印刷ジョブに使用する PostScript 言語レベルを指定します。 設定は、"LanguageLevel"グローバル属性で指定された値より大きくすることはありませんが。</p>
<p>固定ドキュメント</p></td>
</tr>
<tr class="even">
<td><p><strong>%PageOrder</strong></p></td>
<td><p>"FrontToBack"</p>
<p>"BackToFront"</p></td>
<td><p>〇</p></td>
<td><p>ページの印刷順序を指定します。</p>
<p>固定ドキュメント</p>
<p>詳細については、下の注 3 を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><strong>%PagePerSheet</strong></p></td>
<td><p>"1", "2", "4", "6",</p>
<p>「9」、「16」、「小冊子」</p></td>
<td><p>〇</p></td>
<td><p>物理的なシートごとの論理ページの数を指定します。 この機能は、"n-up"印刷とも呼ばれます。</p>
<p>固定ドキュメント</p>
<p>詳細については、下の注 4 を参照してください。</p></td>
</tr>
<tr class="even">
<td><p><strong>%PSErrorHandler</strong></p></td>
<td><p>"True"</p>
<p>"False"</p></td>
<td><p>〇</p></td>
<td><p>PostScript エラー ハンドラーを送信します。</p>
<p>固定ドキュメント</p></td>
</tr>
<tr class="odd">
<td><p><strong>%PSMemory</strong></p></td>
<td><p>NULL で終わる ANSI 文字列の 0 ~ 2,147, 483,647 の範囲で、PostScript メモリのキロバイト数の符号なし整数を表す 10 進文字を含んでいます。</p>
<p><strong>SetOptions</strong>、余分なタブまたは空白文字の前に、または後の 10 進数字が許可されている場合がの記号は許可されません。</p></td>
<td><p>X</p></td>
<td><p>使用できる PostScript 仮想メモリの量を指定します。</p>
<p>コア ドライバーでは、その処理の PostScript 仮想メモリの使用量が必要です。 場合<strong>%psmemory</strong>設定は、新しい値としてこの最小値を下回って最小の値が使用されます。 現在、最小値は、レベル 1 のプリンター 172 KB とレベル 2 + プリンターは 249 KB です。</p>
<p>プリンター固定</p></td>
</tr>
<tr class="even">
<td><p><strong>%TextTrueGray</strong></p></td>
<td><p>"True"</p>
<p>"False"</p></td>
<td><p>〇</p></td>
<td><p>PostScript 灰色に灰色のテキストに変換します。</p>
<p>プリンター固定</p></td>
</tr>
<tr class="odd">
<td><p><strong>%TTDownloadFormat</strong></p></td>
<td><p>"Automatic", "Outline", "Bitmap", "NativeTrueType"</p></td>
<td><p>〇</p></td>
<td><p>形式をダウンロードする TrueType フォントを指定します。 "TTRasterizer"グローバルな属性"Type42"のサポートを指定する場合にのみ、"NativeTrueType"はサポートされています。</p>
<p>固定ドキュメント</p></td>
</tr>
<tr class="even">
<td><p><strong>%WaitTimeout</strong></p></td>
<td><p>NULL で終わる ANSI 文字列の 0 ~ 2,147, 483,647 の範囲で、タイムアウトの秒数の符号なし整数を表す 10 進文字を含んでいます。</p>
<p><strong>SetOptions</strong>、余分なタブまたは空白文字の前に、または後の 10 進数字が許可されている場合がの記号は許可されません。</p></td>
<td><p>X</p></td>
<td><p>待機のタイムアウト値を指定します。</p>
<p>プリンター固定</p></td>
</tr>
</tbody>
</table>

## <a name="notes-on-driver-feature-keywords"></a>ドライバーの機能のキーワードに関する注意事項

1. **%Custompagesize**ドライバーの機能が 5 つのオプションの値: x、y、WidthOffset、HeightOffset、および FeedDirection します。 5.16」セクションを参照してください、 *PostScript プリンター説明ファイル形式の仕様、バージョン 4.3*、これらのパラメーターの詳細について。

    A **%custompagesize**エントリが含まれる、 **%custompagesize** x、y、WidthOffset、HeightOffset、および FeedDirection オプションの値と共に、キーワード。 最初の項目は、NULL 文字が続く、%custompagesize キーワードです。 X の値、y、WidthOffset、および HeightOffset に従ってこのキーワードは、符号なし 10 進数字の部分文字列として表示されます、PostScript の数を表す各オプションの対応する値のポイントします。 1 つ以上のスペースまたはタブ文字の各数値の値が続きます。 文字列の最後の項目は、FeedDirection で、NULL 文字で終了の値です。 FeedDirection のオプションは、"LongEdge"、"ShortEdge"(0 と 1 の向きに対応する)、および"LongEdgeFlip"、"ShortEdgeFlip"(2 および 3 の向きに対応)。 チェック、  **\*LeadingEdge** PPD 機能キーワードがサポートされているフィードの方向をします。

    **GetOptions**、によって示される出力バッファー *pmszFeatureOptionBuf*は、前の段落で説明します。 次の例では、x の値は 612 y の値は 792、WidthOffset および HeightOffset の値はどちらも 0 と FeedDirection の値は"ShortEdge"。

    ```cpp
    "%CustomPageSize\0612 792 0 0 ShortEdge\0"
    ```

    **SetOptions**、余分なタブまたは空白文字の前に、または後の 10 進数字が許可されている場合がの記号は許可されません。 それ以外の場合、入力バッファーによって示される*pmszFeatureOptionBuf*前述のように構築する必要があります。

2. **%Custompagesize**次の条件の 3 つすべてが満たされた場合にのみ、ドライバーの機能がサポートされます。
    1. PPD ファイルが含まれています、  **\*CustomPageSize**機能します。
    2.  **\*PPD Adobe**キーワード 4.3 の場合、以上の値を持つまたは **\*UseHWMargin**:**False**をロールが取り込まれるデバイスを示すために指定します。
    3.  **\*PageSize** PPD 機能の現在選択されているオプションは CustomPageSize します。

3. この機能は、スプーラー EMF スプールが有効になっている場合にのみサポートします。

    サポートされている場合は、この機能のオプションを EMF に関連する次の機能に変更を"false"に設定。

    1. 場合 **%pagepersheet** 「小冊子」は、「1」に変わります。
    2. Collate は、"True"に設定されている場合 (設定できるいずれかのパブリックの部分で直接、 [ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)構造体または呼び出すことによって**SetOptions**上、  **\*Collate** PPD 機能)、部単位で印刷機能は現在利用できませんは、Collate を"False"に設定されます。
    3. 場合 **%pageorder**プリンターの現在の出力の順序設定の反対 **%pageorder**プリンターの値を元に戻されます。

4. この機能は、スプーラー EMF スプールが有効になっている場合にのみサポートします。

    サポートされているこの機能を設定すると、次のようする場合します。

    1. プリンターの PPD ファイルが含まれている場合、  **\*OutputOrder**機能のキーワード、そのオプションを選択したはの新しい設定が、出力順序が一致するように変更し、 **%pageorder**機能します。 これは、スプーラーが不要なページの順序のシミュレーションを実行することを防ぐために実行されます。
    2. プリンターの PPD ファイルが含まれていない場合、  **\*OutputOrder**機能、および用の新しい設定、 **%pageorder**ドライバー機能は、プリンターの現在の出力の順序設定の反対および **%metafilespooling**ドライバーの機能は"False" **%metafilespooling**は"True"にリセットされます。

5. 「小冊子」オプションは、スプーラー EMF スプールが有効になっており、双方向の機能が利用可能な場合にのみサポートされています。

    「小冊子」オプションがサポートされている場合は、設定、 **%pagepersheet**ドライバー機能「小冊子」を次の変更が発生することができます。

    1. 場合、 **%metafilespooling**ドライバー機能は、"False"、"True"にリセットされます。
    2. 場合、 **\*双方向**PPD 機能が None に設定されている、 **\*双方向**機能は PPD ファイルで定義されている最初の非シンプレックス オプションにリセットされます。

6. "EPS"(PostScript) を除く、形式が指定された、 **%outputformat**ドライバーの機能は、次の 2 つの特性に基づいて分類されます。
    1. 出力は、PostScript コード ページの順序に依存しないでしょうか。
    2. 出力には PostScript コードには、デバイスの管理コマンドが含まれている (通常を使用する、 **setpagedevice**演算子) ですか?

        <table>
        <colgroup>
        <col width="33%" />
        <col width="33%" />
        <col width="33%" />
        </colgroup>
        <thead>
        <tr class="header">
        <th></th>
        <th>ページの順序に依存しません。</th>
        <th>setpagedevice</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td><p>アーカイブ</p></td>
        <td><p>〇</p></td>
        <td><p>X</p></td>
        </tr>
        <tr class="even">
        <td><p>移植性</p></td>
        <td><p>〇</p></td>
        <td><p>〇</p></td>
        </tr>
        <tr class="odd">
        <td><p>速度</p></td>
        <td><p>X</p></td>
        <td><p>〇</p></td>
        </tr>
        </tbody>
        </table>

ときに**GetOptions**要求された機能のキーワードが認識されない場合、または機能のキーワードが認識されましたが、現在ではサポートされていない場合、ドライバー機能のキーワードで呼びます*ドキュメント スティッキー*または*プリンター スティッキー*モード (を参照してください[Replacing Driver-Supplied プロパティ シート ページ](replacing-driver-supplied-property-sheet-pages.md))、機能は、単に無視され、出力バッファーがその機能またはオプションのキーワードのペアが含まれていません。

たとえば、 **GetOptions**メソッドが呼び出されると、および*pmszFeaturesRequested*入力バッファーには、次の文字列が含まれています (マルチで\_SZ 形式)。

```cpp
"Resolution\0%CustomPageSize\0Unknown_Name\0%Orientation\0\0"
```

後**GetOption**から制御が戻る、 *pmszFeatureOptionBuf*出力バッファーは、この文字列を含む可能性があります (複数でも\_SZ 形式)。

```cpp
"Resolution\0300dpi\0%CustomPageSize\0612 792 0 0 ShortEdge\0%Orientation\0RotatedLandscape\0\0"
```

注意不明、\_2 番目の文字列では、Pscript ドライバーによって認識されませんでしたので (これが存在しない)、最初の文字列に表示されている名前機能が表示されません。 その他の機能、解像度、 **%custompagesize**、および **% 向き**、出力文字列に表示される、"300 dpi"である、現在のオプションと組み合わせて、"612 792 0 0 ShortEdge"、および"RotatedLandscape"では、それぞれします。 詳細については、ドライバーの機能を参照してください、 **%custompagesize**オプション。

ときに**SetOptions**要求された機能のキーワードまたは入力バッファー内のオプションのキーワードによって示される場合は、ドライバー機能のキーワードで呼び出さ*pmszFeatureOptionBuf*が認識されない機能は、または認識されましたが、現在の固定ドキュメントまたはプリンター固定モードでサポートされていません (を参照してください[Replacing Driver-Supplied プロパティ シート ページ](replacing-driver-supplied-property-sheet-pages.md))、または機能のキーワードとそのオプションのキーワードの両方が、オプションのキーワードが認識その機能は無効です (などを設定しよう **%ttdownloadformat** Type42 TTRasterizer をサポートしていないプリンターで"NativeTrueType"に)、その機能またはオプションの組み合わせは無視されますし、および現在のオプションその機能を継続して有効にします。

バッファー内の機能/オプション キーワードの組み合わせの順序が指す*pmszFeatureOptionBuf*の結果に影響を与えることができます、 **SetOptions**呼び出します。 たとえば、次の 2 つの異なる順序では、異なる結果があります。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th><em>pmszFeatureOptionBuf</em></th>
<th>% PagePerSheet</th>
<th>% MetafileSpooling</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>"%Metafilespooling\0false\0%pagepersheet\0booklet\0\0"</p></td>
<td><p>「小冊子」</p></td>
<td><p>"True"</p></td>
</tr>
<tr class="even">
<td><p>"%Pagepersheet\0booklet\0%metafilespooling\0false\0\0"</p></td>
<td><p>"1"</p></td>
<td><p>"False"</p></td>
</tr>
</tbody>
</table>

これらの結果が発生する理由の詳細については、注 3 を参照してください。 **% MetafileSpooling**上、します。
