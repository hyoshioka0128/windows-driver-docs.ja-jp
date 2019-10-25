---
title: プリント プロセッサで GDI 関数を使用する
description: プリント プロセッサで GDI 関数を使用する
ms.assetid: 2ad62308-ab42-4475-ac42-f753d5091251
keywords:
- EMF レコード再生の WDK プリントプロセッサ
- GDI 関数 WDK プリントプロセッサ
- NT EMF WDK プリントプロセッサ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2992d80e77bf58cc57a76d4678e6e049a9dde1c5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844198"
---
# <a name="using-gdi-functions-in-print-processors"></a>プリント プロセッサで GDI 関数を使用する





ユーザーモードの GDI 関数のセットは、Gdi32 によってエクスポートされます。これは、NT ベースのオペレーティングシステム EMF を入力形式として処理するプリントプロセッサによって使用されます。 次の表に、提供されている関数の一覧を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>関数名</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdideletespoolfilehandle" data-raw-source="[&lt;strong&gt;GdiDeleteSpoolFileHandle&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdideletespoolfilehandle)"><strong>GdiDeleteSpoolFileHandle</strong></a></p></td>
<td><p>スプールファイルハンドルを解放します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdienddocemf" data-raw-source="[&lt;strong&gt;GdiEndDocEMF&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdienddocemf)"><strong>GdiEndDocEMF</strong></a></p></td>
<td><p>印刷ジョブドキュメントに対して EMF 再生操作を完了します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdiendpageemf" data-raw-source="[&lt;strong&gt;GdiEndPageEMF&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdiendpageemf)"><strong>GdiEndPageEMF</strong></a></p></td>
<td><p>物理ページに対して EMF 再生操作を完了し、プリンターからページを排出します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetdc" data-raw-source="[&lt;strong&gt;GdiGetDC&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetdc)"><strong>GdiGetDC</strong></a></p></td>
<td><p>プリンターのデバイスコンテキストを示すハンドルを返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetdevmodeforpage" data-raw-source="[&lt;strong&gt;GdiGetDevmodeForPage&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetdevmodeforpage)"><strong>GdiGetDevmodeForPage</strong></a></p></td>
<td><p>ドキュメントページの<a href="https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)"><strong>Devmodew</strong></a>構造体を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetpagecount" data-raw-source="[&lt;strong&gt;GdiGetPageCount&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetpagecount)"><strong>GdiGetPageCount</strong></a></p></td>
<td><p>ドキュメントページの数を返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetpagehandle" data-raw-source="[&lt;strong&gt;GdiGetPageHandle&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetpagehandle)"><strong>GdiGetPageHandle</strong></a></p></td>
<td><p>ドキュメントページへのハンドルを返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetspoolfilehandle" data-raw-source="[&lt;strong&gt;GdiGetSpoolFileHandle&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetspoolfilehandle)"><strong>GdiGetSpoolFileHandle</strong></a></p></td>
<td><p>他の GDI 関数への入力として必要なスプールファイルハンドルを返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdiplaypageemf" data-raw-source="[&lt;strong&gt;GdiPlayPageEMF&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdiplaypageemf)"><strong>GdiPlayPageEMF</strong></a></p></td>
<td><p>ドキュメントページに関連付けられている EMF レコードを再生します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdiresetdcemf" data-raw-source="[&lt;strong&gt;GdiResetDCEMF&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdiresetdcemf)"><strong>GdiResetDCEMF</strong></a></p></td>
<td><p>プリンターのデバイスコンテキストをリセットします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdistartdocemf" data-raw-source="[&lt;strong&gt;GdiStartDocEMF&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdistartdocemf)"><strong>GdiStartDocEMF</strong></a></p></td>
<td><p>印刷ジョブドキュメントの初期化操作を実行します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdistartpageemf" data-raw-source="[&lt;strong&gt;GdiStartPageEMF&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdistartpageemf)"><strong>GdiStartPageEMF</strong></a></p></td>
<td><p>物理ページの初期化操作を実行します。</p></td>
</tr>
</tbody>
</table>

 

EMF プリントプロセッサの[**Printdocumentonprintprocessor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-printdocumentonprintprocessor)は、スプールファイルハンドルを取得するために[**GdiGetSpoolFileHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetspoolfilehandle)を呼び出し、プリンターのデバイスコンテキストハンドルを取得するために[**GdiGetDC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetdc)を呼び出す必要があります。 その後、次の手順を実行できます。

-   各印刷ジョブドキュメントに対して、EMF レコードを再生する前に[**GdiStartDocEMF**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdistartdocemf)を呼び出す必要があります。また、最後の emf レコードが再生された後に[**GdiEndDocEMF**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdienddocemf)を呼び出す必要があります。

-   印刷する各物理ページに対して、ページ上にドキュメントページを描画する前に[**GdiStartPageEMF**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdistartpageemf)を呼び出す必要があります。また、物理ページに最後のドキュメントページが描画された後に[**GdiEndPageEMF**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdiendpageemf)を呼び出す必要があります。

-   各ドキュメントページを物理ページに描画するには、 [**GdiGetDevmodeForPage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetdevmodeforpage)を呼び出して、最後のドキュメントページの描画後に DEVMODE 構造体の内容が変更されたかどうかを確認する必要があります。 DEVMODE が変更された場合は、 [**GdiEndPageEMF**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdiendpageemf)と[**GdiStartPageEMF**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdistartpageemf)を呼び出すことによって新しい物理ページを起動し、 [**GdiResetDCEMF**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdiresetdcemf)を呼び出してプリンターのデバイスコンテキストを更新する必要があります。 ドキュメントページを物理ページに描画するには、まず[**GdiGetPageHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetpagehandle)を呼び出してドキュメントページハンドルを取得し、次に[**GdiPlayPageEMF**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdiplaypageemf)を呼び出してページを描画します。

ジョブが完全に描画された後、プリントプロセッサは[**GdiDeleteSpoolFileHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdideletespoolfilehandle)を呼び出す必要があります。

印刷プロセッサがページの印刷を開始する前に合計ページ数が必要な場合 (逆の順序でページを印刷する場合など) は、 [**GdiGetPageCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winppi/nf-winppi-gdigetpagecount)を呼び出すことができますが、この関数は、スプールが終了して印刷機能を無効にするまでは戻りません。スプール.

プリントプロセッサがこれらの GDI 関数を使用する場合、 [**Enumprintprocessordatatypes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winspool/nf-winspool-enumprintprocessordatatypesa)データ型関数は、一般的な Windows 2000 以降の EMF 形式を表すサポートされるデータ型として "NT EMF" を返す必要があります。 プリントプロセッサでは、EMF レコードを変更できません。

 

 




