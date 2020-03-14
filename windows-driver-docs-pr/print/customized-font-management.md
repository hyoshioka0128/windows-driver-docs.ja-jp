---
title: カスタマイズされたフォント管理
description: カスタマイズされたフォント管理
ms.assetid: 6e643703-ace1-4660-990c-3a9ca735829d
keywords:
- Unidrv、fonts
- フォント管理 WDK Unidrv
- カスタマイズされたフォント管理 WDK Unidrv
- ufm ファイル
- UFM ファイル
- . gtt ファイル
- GTT ファイル
- uff ファイル
- UFF ファイル
- デバイスフォント WDK Unidrv
- カートリッジフォント WDK Unidrv
- ダウンロード可能な PCL ソフトフォント WDK Unidrv
- PCL ソフトフォント WDK Unidrv
- Unidrv WDK 印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53ecde093b173c6b0833bc4c5929cf478359a0ae
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242883"
---
# <a name="customized-font-management"></a>カスタマイズされたフォント管理





*PCL*プリンターの場合、Unidrv はビットマップまたは TrueType のアウトラインとしてソフトフォントをダウンロードすることをサポートしています。 デバイスフォントの場合、Unidrv は PCL、CAPSL、および PPDS プリンターのコマンド形式をサポートします。 その他の形式については、カスタマイズされたフォント管理コードをレンダリングプラグインで提供する必要があります。 次の一連の IPrintOemUni メソッドを実装できます。

<a href="" id="iprintoemuni--downloadfontheader"></a>[**IPrintOemUni::D ownloadFontHeader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-downloadfontheader)  
Unidrv からソフトフォントのヘッダー情報を取得し、その情報をプリンターにダウンロードするために使用されます。

<a href="" id="iprintoemuni--downloadcharglyph"></a>[**IPrintOemUni::D ownloadCharGlyph**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-downloadcharglyph)  
ソフトフォントの文字グリフをプリンターにダウンロードするために使用します。

<a href="" id="iprintoemuni--outputcharstr"></a>[**IPrintOemUni:: OutputCharStr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-outputcharstr)  
文字の印刷を制御するために使用します。

<a href="" id="iprintoemuni--sendfontcmd"></a>[**IPrintOemUni:: SendFontCmd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-sendfontcmd)  
プリンターのデバイスフォント選択コマンドを変更するために使用され、必要に応じてプリンターに送信します。

<a href="" id="iprintoemuni--textoutasbitmap"></a>[**IPrintOemUni:: TextOutAsBitmap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-textoutasbitmap)  
テキスト文字列のビットマップイメージを作成するために使用します。

<a href="" id="iprintoemuni--ttdownloadmethod"></a>[**IPrintOemUni:: TTDownloadMethod**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-ttdownloadmethod)  
指定したソフトフォントをプリンターに送信するときに、Unidrv が使用するグリフ形式を指定するために使用します。

Unidrv は、 [*UNIFONTOBJ\_GetInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/printoem/nc-printoem-pfngetinfo)のコールバック関数を提供します。レンダリングプラグインは、を呼び出して、フォントやグリフの情報を取得できます。

デバイスフォントについては、「 **Unidrv font metrics files** 」セクションと「**グリフ変換テーブルファイル**」セクションで説明されているように、フォントの説明を入力する必要があります。

カートリッジフォントの場合、フォントの説明はリソース Dll で提供され、フォントカートリッジファイルを使用して指定できます。 フォントの説明は、Unidrv フォントフォーマットファイルの形式で指定することもできます。

ダウンロード可能な PCL ソフトフォントについては、「 **Unidrv フォントフォーマットファイル**」セクションで説明されているように、フォントの説明を指定する必要があります。

### <a href="" id="ddk-unidrv-font-metrics-files-gg"></a>Unidrv フォントメトリックファイル

プリンターでサポートされている各デバイスフォントは、Unidrv フォントメトリック (ufm) ファイルで表現する必要があります。 Ufm ファイルは、 [Unidrv フォントメトリック構造](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)体で記述された構造体を使用して構築されるバイナリファイルです。 Ufm ファイルの最初の構造は[**unifm\_HDR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prntfont/ns-prntfont-_unifm_hdr)です。これには、ファイルのその他の構造体へのオフセットが含まれます。 次の図は、Unidrv フォントメトリックファイルのレイアウトを示しています。

![unidrv フォントメトリックファイルのレイアウトを示す図](images/ufm.png)

Unidrv は、Windows NT 4.0 用に作成されたフォントメトリックファイルである、ifi ファイルもサポートしています。

### <a href="" id="ddk-glyph-translation-table-files-gg"></a>グリフ変換テーブルファイル

プリンターでサポートされている各デバイスフォントは、グリフ変換テーブル (gtt) ファイルによって表される必要があります。 Gtt ファイルは、「 [Unidrv グリフ変換テーブル構造](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)」で説明されている構造を使用して構築されたバイナリファイルです。 Gtt ファイルの最初の構造は、 [**UNI\_GLYPHSETDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prntfont/ns-prntfont-_uni_glyphsetdata)構造体であり、ファイルのその他の構造体へのオフセットが含まれています。

次の図は、グリフ変換テーブルファイルのレイアウトを示しています。

![グリフ変換テーブルファイルのレイアウトを示す図](images/gtt.png)

上の図では、UNI\_GLYPHSETDATA 構造体に、ファイルの先頭から最初の[**GLYPHRUN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prntfont/ns-prntfont-_glyphrun)構造体、最初の[**UNI\_CODEPAGEINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prntfont/ns-prntfont-_uni_codepageinfo)構造体、および[**maptable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prntfont/ns-prntfont-_maptable)構造体へのオフセットが含まれています。

また、Unidrv では、Windows NT 4.0 用に作成されたグリフ変換ファイルもサポートしています。これは、実行時のエンコード (RLE) 圧縮を使用していて、拡張子は rle です。

### <a href="" id="ddk-unidrv-font-format-files-gg"></a>Unidrv フォントフォーマットファイル

フォントカートリッジを使用して指定されていないカートリッジフォントの場合、ソフトフォントは、uff ファイルを使用して指定する必要があります。

Uff ファイルは、次の構造のセットを使用して構築されるバイナリファイルです。

-   、Uff ファイルの内容と構造を定義する、 [Unidrv フォント形式の構造体](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)。

-   各フォントのメトリックを定義する[Unidrv フォントメトリック構造](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)。

-   フォントで使用されるグリフセットを定義する[Unidrv グリフ変換テーブル構造](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)。

次の図は、Unidrv フォントフォーマットファイルのレイアウトを示しています。

![unidrv フォントフォーマットファイルのレイアウトを示す図](images/uff.png)

Unidrv フォントフォーマットファイルは、 [**uff\_FILEHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prntfont/ns-prntfont-_uff_fileheader)構造体と、1つ以上の[**UFF\_fontdirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prntfont/ns-prntfont-_uff_fontdirectory)と[**データ\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prntfont/ns-prntfont-_data_header)構造体のペアで構成されます。 各データ\_ヘッダー構造体は、フォントデータのブロックに関連付けられています。 UFF\_FILEHEADER 構造体には、ファイルの先頭から最初の UFF\_FONTDIRECTORY 構造体までのオフセットが含まれます。 各 UFF\_FONTDRECTORY 構造体には、ファイルの先頭から、フォントデータを格納するデータ\_ヘッダー構造へのオフセットが含まれています。

また、 *PCL*ソフトフォントをダウンロードできるように、ダウンロードするバイナリデータは、uff ファイルに格納されています。

uff ファイルの作成は、ベンダーが提供するフォントインストールソフトウェアの役割です。 Unidrv は、プリンターの uff ファイルを読み取り、フォントとグリフの情報を取得します。 フォントが追加または削除されると、フォントのインストーラーによってファイルの内容が変更されます。 フォントインストーラーの作成の詳細については、「 [Unidrv のフォントインストーラーをカスタマイズ](customized-font-installers-for-unidrv.md)する」を参照してください。

すべての uff ファイルは、% SystemRoot%\\System32\\Spool\\Drivers\\Unifont ディレクトリに保存されている必要があります。 個々の uff ファイルを特定のプリンターと関連付けるには、インストールソフトウェアで Setprinter Data 関数 (Windows SDK のドキュメントで説明されています) を呼び出して、各プリンターのレジストリキーの下にレジストリ値を作成する必要があります。 次の表は、使用する必要があるレジストリ値の名前と、それぞれの値の保守の可能性を示しています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>レジストリ値の名前と種類</th>
<th>値の定義</th>
<th>テナ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>"ExternalFontFile"</p>
<p>REG_SZ</p></td>
<td><p>現在インストールされているフォントを指定する、uff ファイルのファイル名。 フォントは、ダウンロードしたり、カートリッジに含めたりすることができます。</p></td>
<td><p>フォントインストーラー</p></td>
</tr>
<tr class="even">
<td><p>"ExtFontCartFile"</p>
<p>REG_SZ</p></td>
<td><p>"ExtFontCartNames" について一覧表示されているすべてのフォントカートリッジに含まれるすべてのフォントを指定する、uff ファイルのファイル名。</p></td>
<td><p>フォントインストーラー</p></td>
</tr>
<tr class="odd">
<td><p>"ExtFontCartNames"</p>
<p>REG_MULTI_SZ</p></td>
<td><p>プリンターにインストールできる可能性のあるすべてのフォントカートリッジの名前。</p></td>
<td><p>フォントインストーラー</p></td>
</tr>
<tr class="even">
<td><p>"FontCart"</p>
<p>REG_MULTI_SZ</p></td>
<td><p>プリンターに現在インストールされているすべてのフォントカートリッジの名前。</p></td>
<td><p>Unidrv ユーザーインターフェイス</p></td>
</tr>
</tbody>
</table>

 

プリンターにフォントカートリッジを追加した後、システム管理者はフォントインストーラーを実行する必要があります。これは、"ExtFontCartFile" によって指定された uff ファイルから、"ExternalFontFile" によって指定された uff ファイルにフォントの説明をコピーします。 同様に、フォントインストーラーでは、カートリッジが削除されたときに、"ExtFontCartFile" で指定された uff ファイルからフォントの説明を削除する必要があります。

 

 




