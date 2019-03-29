---
title: Pscript でサポートされているエスケープ
description: Pscript でサポートされているエスケープ
ms.assetid: c0133355-fa3b-4117-bd38-b6a8b3898f94
keywords:
- PostScript プリンター ドライバー WDK の印刷、エスケープ
- Pscript WDK の印刷、エスケープ
- WDK Pscript のエスケープ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24b5cb6b6cb2f0bb6e26622921a34fa492e64ca9
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349013"
---
# <a name="pscript-supported-escapes"></a>Pscript でサポートされているエスケープ





Pscript5 のプリンター ドライバーでは、以下のエスケープをサポートします。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Esc キー</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>BEGIN_PATH</p></td>
<td><p>パスを開きます。</p></td>
</tr>
<tr class="even">
<td><p>CHECKJPEGFORMAT</p></td>
<td><p>JPEG イメージをプリンターが処理できるかどうかを決定します。 このエスケープの詳細については、Microsoft Windows sdk で CHECKJPEGFORMAT を参照してください。</p>
<p>このエスケープへの呼び出しの生成、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff556260" data-raw-source="[&lt;strong&gt;DrvQueryDeviceSupport&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556260)"> <strong>DrvQueryDeviceSupport</strong> </a>関数。</p></td>
</tr>
<tr class="odd">
<td><p>CHECKPNGFORMAT</p></td>
<td><p>プリンターが PNG イメージを処理できるかどうかを決定します。 このエスケープの詳細については、Windows sdk で CHECKPNGFORMAT を参照してください。</p>
<p>このエスケープへの呼び出しの生成、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff556260" data-raw-source="[&lt;strong&gt;DrvQueryDeviceSupport&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556260)"> <strong>DrvQueryDeviceSupport</strong> </a>関数。</p></td>
</tr>
<tr class="even">
<td><p>CLIP_TO_PATH</p></td>
<td><p>パスで区切られたクリップ領域を定義します。</p></td>
</tr>
<tr class="odd">
<td><p>DOWNLOADHEADER</p></td>
<td><p>Procsets (つまり、PostScript プロシージャのセット) のすべてをダウンロードします。</p></td>
</tr>
<tr class="even">
<td><p>DRAWPATTERNRECT</p></td>
<td><p>Hewlett Packard LaserJet または LaserJet と互換性のあるプリンターでページ制御言語 (PCL) のパターンとルールの機能を使用して、白、グレースケール、または黒い実線の四角形を作成します。 グレースケールは、白と黒のピクセルの特定の組み合わせを含む灰色パターンです。 このエスケープの詳細については、Windows sdk で DRAWPATTERNRECT を参照してください。</p>
<p>このエスケープは、ドライバーの関連付け<a href="https://msdn.microsoft.com/library/windows/hardware/ff556217" data-raw-source="[&lt;strong&gt;DrvEscape&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556217)"> <strong>DrvEscape</strong> </a>関数。</p></td>
</tr>
<tr class="odd">
<td><p>ENCAPSULATED_POSTSCRIPT</p></td>
<td><p>Encapsulated PostScript (EPS) のデータをプリンターに送信します。</p>
<p>Microsoft Windows NT 4.0 のプリンター ドライバーでは、このエスケープはサポートされていません。</p>
<p>このエスケープは、ドライバーの関連付け<a href="https://msdn.microsoft.com/library/windows/hardware/ff556203" data-raw-source="[&lt;strong&gt;DrvDrawEscape&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556203)"> <strong>DrvDrawEscape</strong> </a>関数。</p></td>
</tr>
<tr class="even">
<td><p>END_PATH</p></td>
<td><p>パスを終了します。</p></td>
</tr>
<tr class="odd">
<td><p>EPSPRINTING</p></td>
<td><p>開始または EPS 印刷の終了を示します。</p>
<p>グラフィックス デバイス インターフェイス (GDI) は、このエスケープをインターセプトし、DrvEscape 以外 DDI 呼び出しに変換します。 プリンター ドライバーでは、このエスケープは受信しません。</p></td>
</tr>
<tr class="even">
<td><p>GET_PS_FEATURESETTING</p></td>
<td><p>PostScript ドライバーの指定した機能の設定に関する情報を取得します。</p>
<p>このエスケープの詳細については、Windows sdk で GET_PS_FEATURESETTING を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>GETTECHNOLOGY</p></td>
<td><p>プリンターの一般的なテクノロジの種類を取得します。 Windows 3.0 の後のバージョンの Windows オペレーティング システム向けに作成されたプリンター ドライバーが、このエスケープをサポートしていません。</p></td>
</tr>
<tr class="even">
<td><p>パススルー</p></td>
<td><p>互換性モードまたは GDI 中心モードでの PostScript プリンター ドライバーに直接データを送信します。 PostScript プリンター ドライバーが PostScript を中心としたモードでは、このエスケープをサポートしていません。</p>
<p>このエスケープの詳細については、Windows sdk でパススルーを参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>POSTSCRIPT_DATA</p></td>
<td><p>プリンター ドライバーに直接データを送信します。 PostScript プリンター ドライバーでは、Windows NT 4.0 互換モードでのみこのエスケープをサポートする点を除いて、このエスケープはパススルー エスケープと同じです。</p>
<p>このエスケープの詳細については、Windows sdk で POSTSCRIPT_DATA を参照してください。</p></td>
</tr>
<tr class="even">
<td><p>POSTSCRIPT_IDENTIFY</p></td>
<td><p>PostScript プリンター ドライバーを GDI 中心、PostScript を中心としたモードに設定します。</p>
<p>このエスケープの詳細については、Windows sdk で POSTSCRIPT_IDENTIFY を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>POSTSCRIPT_IGNORE</p></td>
<td><p>出力を抑制します。</p>
<p>PostScript プリンター ドライバーのみまたは GDI 中心モードで Windows NT 4.0 互換モードでは、このエスケープをサポートします。 PostScript プリンター ドライバーが PostScript を中心としたモードでは、このエスケープをサポートしていません。</p></td>
</tr>
<tr class="even">
<td><p>POSTSCRIPT_INJECTION</p></td>
<td><p>PostScript ジョブのストリームでは、生データのブロックを挿入します。</p>
<p>このエスケープの詳細については、Windows sdk で POSTSCRIPT_INJECTION を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>POSTSCRIPT_PASSTHROUGH</p></td>
<td><p>PostScript プリンター ドライバーが Windows NT 4.0 互換モードまたは PostScript を中心としたモードに直接データを送信します。 PostScript プリンター ドライバーが GDI 中心モードでは、このエスケープをサポートしていません。</p>
<p>このエスケープの詳細については、Windows sdk で POSTSCRIPT_PASSTHROUGH を参照してください。</p></td>
</tr>
<tr class="even">
<td><p>関数</p></td>
<td><p>デバイス ドライバーが特定のエスケープを実装するかどうかを決定します。</p>
<p>このエスケープの詳細については、Windows sdk で関数を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p>SETCOPYCOUNT</p></td>
<td><p>印刷するコピーの数を設定します。</p>
<p>このエスケープはによって置き換えられました、 <strong>DocumentProperties</strong>と<strong>PrinterProperties</strong>関数で、Windows SDK のドキュメントに記載されています。</p>
<p>このエスケープの詳細については、Windows sdk で SETCOPYCOUNT を参照してください。</p></td>
</tr>
<tr class="even">
<td><p>SPCLPASSTHROUGH2</p></td>
<td><p>プライベートのプロシージャおよびドキュメント レベルの保存のコンテキストでは、その他のリソースを含むアプリケーションを有効にします。</p>
<p>このエスケープの詳細については、Windows sdk で SPCLPASSTHROUGH2 を参照してください。</p></td>
</tr>
</tbody>
</table>

 

以下のエスケープは、Windows NT 4.0 で追加されたが、現在サポートされていません。

-   ADDMSTT

-   IGNORESTARTPAGE

-   NOFIRSTSAVE

以下のエスケープは廃止されました 16 ビットのバージョンの Windows オペレーティング システムとの互換性のためだけに提供します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Esc キー</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ABORTDOC</p></td>
<td><p>このエスケープはによって置き換えられました、 <strong>AbortDoc</strong>関数は、Windows SDK のドキュメントで説明します。</p></td>
</tr>
<tr class="even">
<td><p>ENDDOC</p></td>
<td><p>このエスケープはによって置き換えられました、 <strong>EndDoc</strong>関数は、Windows SDK のドキュメントで説明します。</p></td>
</tr>
<tr class="odd">
<td><p>GETPHYSPAGESIZE</p></td>
<td><p>このエスケープはで、PHYSICALWIDTH と PHYSICALHEIGHT 値によって置き換えられました、<strong>調べるため</strong>関数は、Windows SDK のドキュメントで説明します。</p></td>
</tr>
<tr class="even">
<td><p>GETPRINTINGOFFSET</p></td>
<td><p>このエスケープはで、PHYSICALOFFSETX と PHYSICALOFFSETY 値によって置き換えられました、<strong>調べるため</strong>関数は、Windows SDK のドキュメントで説明します。</p></td>
</tr>
<tr class="odd">
<td><p>GETSCALINGFACTOR</p></td>
<td><p>このエスケープはで、SCALINGFACTORX と SCALINGFACTORY 値によって置き換えられました、<strong>調べるため</strong>関数は、Windows SDK のドキュメントで説明します。</p></td>
</tr>
<tr class="even">
<td><p>NEWFRAME</p></td>
<td><p>このエスケープはによって置き換えられました、 <strong>EndPage</strong>関数で、ページを終了します。 NEWFRAME とは異なり<strong>EndPage</strong>はページの印刷後に必ず呼び出されます。 <strong>EndPage</strong>については、Windows SDK のドキュメントで説明します。</p></td>
</tr>
<tr class="odd">
<td><p>NEXTBAND</p></td>
<td><p>バンド情報は使用されなくなりました。</p></td>
</tr>
<tr class="even">
<td><p>SETABORTPROC</p></td>
<td><p>このエスケープはによって置き換えられました、 <strong>SetAbortProc</strong>関数は、Windows SDK のドキュメントで説明します。</p></td>
</tr>
<tr class="odd">
<td><p>SETCOPYCOUNT</p></td>
<td><p>このエスケープはによって置き換えられました、 <strong>DocumentProperties</strong>と<strong>PrinterProperties</strong>関数で、Windows SDK のドキュメントに記載されています。</p></td>
</tr>
<tr class="even">
<td><p>STARTDOC</p></td>
<td><p>このエスケープはによって置き換えられました、 <strong>StartDoc</strong>関数は、Windows SDK のドキュメントで説明します。</p></td>
</tr>
</tbody>
</table>

 

 

 




