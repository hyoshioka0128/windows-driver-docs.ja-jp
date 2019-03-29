---
title: 既定の PCL XL フォントを使用する
description: 既定の PCL XL フォントを使用する
ms.assetid: 8e6abae5-c86f-4cfc-a379-2dd3f8810474
keywords:
- PCL XL ベクター グラフィックス WDK Unidrv、既定のフォント
- 既定の PCL XL フォント
- フォント WDK PCL XL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7db9235d061d8a655c194563bfba89ec2d209c21
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464284"
---
# <a name="using-default-pcl-xl-fonts"></a>既定の PCL XL フォントを使用する





標準の PCL XL フォントを追加するには、標準的なリソース DLL を含める必要があります*pclxl.dll*、cab ファイルの一部であります。 必要がありますが、GPD で表示され、次の行を使用して、 \*ResourceDLL 属性を使用する DLL のリソースを指定します。

```cpp
*ResourceDLL: "pclxl.dll"
```

Unidrv をサポートする既定の PCL XL フォントは、次の表のとおりです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>フォント名</th>
<th>フォント ファイル</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>"Albertus Medium"</p></td>
<td><p>ALBERTR します。UFM</p></td>
</tr>
<tr class="even">
<td><p>「Albertus 余分な太字」</p></td>
<td><p>ALBERTX.UFM</p></td>
</tr>
<tr class="odd">
<td><p>「アンティーク オリーブ」</p></td>
<td><p>AOLIVEB します。UFM</p>
<p>AOLIVEI します。UFM</p>
<p>AOLIVER します。UFM</p></td>
</tr>
<tr class="even">
<td><p>"Arial"</p></td>
<td><p>ARIALB します。UFM</p>
<p>ARIALI します。UFM</p>
<p>ARIALJ します。UFM</p>
<p>ARIALR します。UFM</p></td>
</tr>
<tr class="odd">
<td><p>"ITC Benguiat"</p></td>
<td><p>BENGUATB します。UFM</p>
<p>BBENGUATJ します。UFM</p>
<p>BENGUATJ します。UFM</p>
<p>BENGUATR します。UFM</p></td>
</tr>
<tr class="even">
<td><p>「ITC Bookman デミ」</p></td>
<td><p>BOOKMANB します。UFM</p>
<p>BOOKMANJ します。UFM</p></td>
</tr>
<tr class="odd">
<td><p>"ITC Bookman Light"</p></td>
<td><p>BOOKMANI します。UFM</p>
<p>BOOKMANR します。UFM</p></td>
</tr>
<tr class="even">
<td><p>とり入れ</p></td>
<td><p>BROGHAMB します。UFM</p>
<p>BROGHAMI.UFM</p>
<p>BROGHAMJ します。UFM</p>
<p>BROGHAMR します。UFM</p></td>
</tr>
<tr class="odd">
<td><p>「CG オメガ」</p></td>
<td><p>CGOMEGAB します。UFM</p>
<p>CGOMEGAI します。UFM</p>
<p>CGOMEGAJ します。UFM</p>
<p>CGOMEGAR します。UFM</p></td>
</tr>
<tr class="even">
<td><p>"CG Times"</p></td>
<td><p>CGTIMESB します。UFM</p>
<p>CGTIMESI します。UFM</p>
<p>CGTIMESJ します。UFM</p>
<p>CGTIMESR します。UFM</p></td>
</tr>
<tr class="odd">
<td><p>「Clarendon 狭い」</p></td>
<td><p>CLARCD します。UFM</p></td>
</tr>
<tr class="even">
<td><p>「企業」</p></td>
<td><p>CORONETR します。UFM</p></td>
</tr>
<tr class="odd">
<td><p>"Courier"</p></td>
<td><p>COURIERB します。UFM</p>
<p>COURIERI します。UFM</p>
<p>COURIERJ します。UFM</p>
<p>COURIERR します。UFM</p></td>
</tr>
<tr class="even">
<td><p>"Garamond"</p></td>
<td><p>GARMONDB します。UFM</p>
<p>GARMONDI します。UFM</p>
<p>GARMONDJ.UFM</p>
<p>GARMONDR します。UFM</p></td>
</tr>
<tr class="odd">
<td><p>「文字のゴシック」</p></td>
<td><p>LETGOTHB します。UFM</p>
<p>LETGOTHI します。UFM</p>
<p>LETGOTHR します。UFM</p></td>
</tr>
<tr class="even">
<td><p>"Marigold"</p></td>
<td><p>MARGOLDR します。UFM</p></td>
</tr>
<tr class="odd">
<td><p>"New Roman"時間</p></td>
<td><p>TIMESNRB します。UFM</p>
<p>TIMESNRI します。UFM</p>
<p>TIMESNRJ します。UFM</p>
<p>TIMESNRR します。UFM</p></td>
</tr>
<tr class="even">
<td><p>「Univers 狭い」</p></td>
<td><p>UNIVERCB します。UFM</p>
<p>UNIVERCI します。UFM</p>
<p>UNIVERCJ します。UFM</p>
<p>UNIVERCR します。UFM</p></td>
</tr>
<tr class="odd">
<td><p>"Univers"</p></td>
<td><p>Universa.UFM</p>
<p>UNIVERSB します。UFM</p>
<p>Universc.UFM</p>
<p>Universd.UFM</p>
<p>Universe.UFM</p>
<p>UNIVERSI します。UFM</p>
<p>UNIVERSJ します。UFM</p>
<p>UNIVERSR します。UFM</p>
<p>UNIVERSR します。UFM</p></td>
</tr>
<tr class="even">
<td><p>「W 装飾記号」</p></td>
<td><p>WDINGBAT します。UFM</p></td>
</tr>
<tr class="odd">
<td><p>"Wingdings"</p></td>
<td><p>WINGDING します。UFM</p></td>
</tr>
<tr class="even">
<td><p>"Symbol"</p></td>
<td><p>シンボルです。UFM</p></td>
</tr>
</tbody>
</table>

 

 

 




