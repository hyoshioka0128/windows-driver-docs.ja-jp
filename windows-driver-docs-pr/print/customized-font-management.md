---
title: カスタマイズされたフォント管理
description: カスタマイズされたフォント管理
ms.assetid: 6e643703-ace1-4660-990c-3a9ca735829d
keywords:
- Unidrv、フォント
- WDK Unidrv フォントの管理
- カスタマイズしたフォント管理 WDK Unidrv
- .ufm ファイル
- UFM ファイル
- .gtt ファイル
- GTT ファイル
- .uff ファイル
- UFF ファイル
- デバイス フォント WDK Unidrv
- カートリッジ フォント WDK Unidrv
- ダウンロード可能な PCL ソフト フォント WDK Unidrv
- PCL ソフト フォント WDK Unidrv
- Unidrv WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0316bf0a365cf18eb7e7cbf2a68afc73712c36d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365584"
---
# <a name="customized-font-management"></a>カスタマイズされたフォント管理





*PCL*ソフト フォントをビットマップとしてダウンロード プリンター、Unidrv サポートまたは TrueType 概要を説明します。 デバイス フォントの PPDS プリンター コマンド形式を Unidrv が、PCL、CAPSL をサポートします。 その他の形式では、プラグインの表示で管理コードをカスタマイズしたフォントを提供する必要があります。 次の一連の IPrintOemUni メソッドを実装することができます。

<a href="" id="iprintoemuni--downloadfontheader"></a>[**IPrintOemUni::DownloadFontHeader**](https://msdn.microsoft.com/library/windows/hardware/ff554242)  
Unidrv からソフト フォントのヘッダー情報を取得し、プリンターに情報をダウンロードするために使用します。

<a href="" id="iprintoemuni--downloadcharglyph"></a>[**IPrintOemUni::DownloadCharGlyph**](https://msdn.microsoft.com/library/windows/hardware/ff554241)  
ソフト フォントの文字のグリフをプリンターにダウンロードするために使用します。

<a href="" id="iprintoemuni--outputcharstr"></a>[**IPrintOemUni::OutputCharStr**](https://msdn.microsoft.com/library/windows/hardware/ff554267)  
文字の印刷を制御するために使用します。

<a href="" id="iprintoemuni--sendfontcmd"></a>[**IPrintOemUni::SendFontCmd**](https://msdn.microsoft.com/library/windows/hardware/ff554274)  
プリンターのデバイス フォントの選択範囲のコマンドを変更し、必要に応じて、プリンターに送信するために使用します。

<a href="" id="iprintoemuni--textoutasbitmap"></a>[**IPrintOemUni::TextOutAsBitmap**](https://msdn.microsoft.com/library/windows/hardware/ff554277)  
テキスト文字列のビットマップ イメージを作成するために使用します。

<a href="" id="iprintoemuni--ttdownloadmethod"></a>[**IPrintOemUni::TTDownloadMethod**](https://msdn.microsoft.com/library/windows/hardware/ff554279)  
指定ソフト フォントをプリンターに送信されるときに使用、Unidrv グリフ形式を指定するために使用します。

Unidrv、コールバック関数を提供する[ *UNIFONTOBJ\_GetInfo*](https://msdn.microsoft.com/library/windows/hardware/ff563594)プラグインの表示がフォントまたはグリフの情報を取得する呼び出すことができます。

説明するようデバイス フォントのフォントの説明を指定する必要があります、 **Unidrv フォント メトリック ファイル**セクションおよび**グリフの翻訳テーブル ファイル**セクション。

カートリッジのフォントのフォントの記述はリソース Dll を指定することができ、フォントのカートリッジ ファイルを使用して指定します。 フォントの説明については、Unidrv フォント形式のファイルの形式でも指定できます。

説明したようのダウンロード可能な PCL ソフト フォント、フォントの説明を指定する必要があります、 **Unidrv フォント形式ファイル**セクション。

### <a href="" id="ddk-unidrv-font-metrics-files-gg"></a>Unidrv フォント メトリック ファイル

Unidrv フォント メトリック (.ufm) ファイルでは、プリンターがサポートする各デバイス フォントを表す必要があります。 .Ufm ファイルはバイナリ ファイルで説明されている構造体を使用して構築される[Unidrv フォント メトリック構造](https://msdn.microsoft.com/library/windows/hardware/ff563547)します。 .Ufm ファイル内の最初の構造体は[ **UNIFM\_HDR**](https://msdn.microsoft.com/library/windows/hardware/ff563587)、その他の構造でのファイルへのオフセットが含まれています。 次の図は、Unidrv フォント メトリック ファイルのレイアウトを示します。

![unidrv フォント メトリック ファイルのレイアウトを示す図](images/ufm.png)

Unidrv には、.ifi ファイル、Windows NT 4.0 用に作成されたフォント メトリック ファイルもサポートしています。

### <a href="" id="ddk-glyph-translation-table-files-gg"></a>グリフの翻訳テーブル ファイル

グリフ変換テーブル (.gtt) ファイルでは、プリンターがサポートする各デバイス フォントを表す必要があります。 .Gtt ファイルはバイナリ ファイルで説明されている構造体を使用して構築される[Unidrv グリフ翻訳テーブル構造](https://msdn.microsoft.com/library/windows/hardware/ff563549)します。 .Gtt ファイル内の最初の構造体は、 [ **UNI\_GLYPHSETDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff563597)ファイルへのオフセットを含む構造体の他の構造体。

次の図は、グリフの翻訳テーブル ファイルのレイアウトを示します。

![グリフの翻訳テーブル ファイルのレイアウトを示す図](images/gtt.png)

前の図は、単に\_GLYPHSETDATA 構造体には、最初に、ファイルの先頭からのオフセットが含まれています[ **GLYPHRUN** ](https://msdn.microsoft.com/library/windows/hardware/ff550544)構造体の場合は、最初に、 [ 。**UNI\_CODEPAGEINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff563596)構造体、および、 [ **MAPTABLE** ](https://msdn.microsoft.com/library/windows/hardware/ff556509)構造体。

Unidrv には、グリフ翻訳ファイル Windows NT 4.0 では、作成された実行可変長エンコーディング (RLE) 圧縮を使用して、グラフィックスの拡張機能もサポートしています。

### <a href="" id="ddk-unidrv-font-format-files-gg"></a>Unidrv フォント形式のファイル

カートリッジのフォントのフォントのカートリッジを使用して指定されていない .uff ファイルを使用してソフト フォントを指定する必要があります。

.Uff ファイルは、次の構造体のセットを使用して構築されるバイナリ ファイルです。

-   [Unidrv フォント形式構造](https://msdn.microsoft.com/library/windows/hardware/ff562892)、.uff ファイルの構造と内容を定義します。

-   [Unidrv フォント メトリック構造](https://msdn.microsoft.com/library/windows/hardware/ff563547)、各フォントのメトリックを定義します。

-   [Unidrv グリフ翻訳テーブル構造](https://msdn.microsoft.com/library/windows/hardware/ff563549)フォントで使用されるグリフのセットを定義します。

次の図は、Unidrv フォント形式のファイルのレイアウトを示します。

![unidrv フォント形式のファイルのレイアウトを示す図](images/uff.png)

Unidrv フォント形式のファイルから成る、 [ **UFF\_fileheader です**](https://msdn.microsoft.com/library/windows/hardware/ff562862)構造、および 1 つまたは複数[ **UFF\_ディレクトリ**](https://msdn.microsoft.com/library/windows/hardware/ff562866)と[**データ\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff547364)のペアを構造体します。 各データ\_ヘッダー構造がフォント データのブロックに関連付けられています。 UFF\_fileheader です構造体には、最初の UFF ファイルの先頭からのオフセットが含まれています。\_ディレクトリ構造体。 各 UFF\_FONTDRECTORY 構造には、データ ファイルの先頭からのオフセットが含まれる\_フォント データが含まれるヘッダーの構造体。

さらに、ダウンロード可能な*PCL*ソフト フォントは、バイナリ データをダウンロードするが .uff ファイルに格納されます。

.uff ファイルの作成では、ベンダーから提供されたフォントのインストール ソフトウェアの役割です。 Unidrv は、フォントとグリフの情報を取得するプリンターの .uff ファイルを読み取ります。 フォントのインストーラーは、フォントを追加または削除されたとき、.uff ファイルの内容を変更する必要があります。 フォントのインストーラーを作成する方法の詳細については、次を参照してください。 [Unidrv のフォントのカスタマイズされたインストーラー](customized-font-installers-for-unidrv.md)します。

%Systemroot% .uff のすべてのファイルを格納する必要があります\\System32\\スプール\\ドライバー\\Unifont ディレクトリ。 特定のプリンターで関連付ける個々 .uff ファイルには、インストール ソフトウェアが、各プリンターのレジストリ キーの下のレジストリ値を作成する (Windows SDK のドキュメントで説明) SetPrinterData 関数を呼び出す必要があります。 次の表を使用する必要があり、各値のメンテナンス ツールを示すレジストリ値の名前を一覧表示します。

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
<th>メンテナンス ツール</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>"ExternalFontFile"</p>
<p>REG_SZ</p></td>
<td><p>現在インストールされているフォントを指定する .uff ファイルのファイル名。 フォントには、ダウンロード可能なまたはカートリッジに格納されているを指定できます。</p></td>
<td><p>フォントのインストーラー</p></td>
</tr>
<tr class="even">
<td><p>"ExtFontCartFile"</p>
<p>REG_SZ</p></td>
<td><p>"ExtFontCartNames"のすべてのフォントのカートリッジで含まれているすべてのフォントを指定する .uff ファイルのファイル名。</p></td>
<td><p>フォントのインストーラー</p></td>
</tr>
<tr class="odd">
<td><p>"ExtFontCartNames"</p>
<p>REG_MULTI_SZ</p></td>
<td><p>プリンターにインストールできる可能性があるすべてのフォント カートリッジの名前です。</p></td>
<td><p>フォントのインストーラー</p></td>
</tr>
<tr class="even">
<td><p>"FontCart"</p>
<p>REG_MULTI_SZ</p></td>
<td><p>プリンターの現在インストールされているすべてのフォントのカートリッジの名前です。</p></td>
<td><p>Unidrv ユーザー インターフェイス</p></td>
</tr>
</tbody>
</table>

 

フォント カートリッジをプリンターを追加した後、システム管理者は"ExtFontCartFile"で指定された"ExternalFontFile".uff ファイルに指定された .uff ファイルからのフォントの記述をコピーする責任は、フォント インストーラーで実行する必要があります。 同様に、フォントのインストーラーは、カートリッジが削除されたときに、"ExtFontCartFile"によって指定された .uff ファイルからのフォントの記述を削除する必要があります。

 

 




