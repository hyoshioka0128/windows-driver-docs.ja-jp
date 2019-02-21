---
title: WIA を一般的なユーティリティ関数
description: WIA を一般的なユーティリティ関数
ms.assetid: 235c07a1-4903-4df6-b29f-0ecc342782b4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6ffaaeb0e6fc1ae22cb7db396663ebb908269f4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539663"
---
# <a name="general-wia-utility-functions"></a>WIA を一般的なユーティリティ関数





ドライバーのコンテキスト アイテムを取得、システム レジストリから情報を取得、文字列のコピーを次の関数を使用できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>関数</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550166" data-raw-source="[&lt;strong&gt;wiauGetDrvItemContext&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550166)"><strong>wiauGetDrvItemContext</strong></a></p></td>
<td><p>ドライバーのコンテキスト アイテムと、必要に応じて、ドライバーの項目を取得します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550169" data-raw-source="[&lt;strong&gt;wiauGetResourceString&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550169)"><strong>wiauGetResourceString</strong></a></p></td>
<td><p>格納することとして、リソース文字列を取得、 <strong>BSTR</strong>します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550170" data-raw-source="[&lt;strong&gt;wiauGetValidFormats&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550170)"><strong>wiauGetValidFormats</strong></a></p></td>
<td><p>呼び出し、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff543986" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvGetWiaFormatInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543986)"> <strong>IWiaMiniDrv::drvGetWiaFormatInfo</strong> </a>メソッドし、指定したフラグの値を使用して、有効な形式の一覧を作成します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550171" data-raw-source="[&lt;strong&gt;wiauPropInPropSpec&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550171)"><strong>wiauPropInPropSpec</strong></a></p></td>
<td><p>このような値の配列で指定したプロパティの指定の識別子 (ID) が含まれているかどうかを判断します。 関数は、必要に応じてインデックスを取得しますプロパティ仕様 ID が見つかりました。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550173" data-raw-source="[&lt;strong&gt;wiauPropsInPropSpec&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550173)"><strong>wiauPropsInPropSpec</strong></a></p></td>
<td><p>プロパティで指定の Id の一覧のいずれかがこのような値の配列内に含まれるかどうかを判断します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550176" data-raw-source="[&lt;strong&gt;wiauRegGetDword&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550176)"><strong>wiauRegGetDword</strong></a></p></td>
<td><p>取得、 <strong>DWORD</strong>値から、 <strong>DeviceData</strong>レジストリのセクション。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550178" data-raw-source="[&lt;strong&gt;wiauRegGetStr&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550178)"><strong>wiauRegGetStr</strong></a></p></td>
<td><p>文字列値を取得、 <strong>DeviceData</strong>レジストリのセクション。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550179" data-raw-source="[&lt;strong&gt;wiauRegOpenData&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550179)"><strong>wiauRegOpenData</strong></a></p></td>
<td><p>開く、 <strong>DeviceData</strong>レジストリ キー。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550181" data-raw-source="[&lt;strong&gt;wiauSetImageItemSize&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550181)"><strong>wiauSetImageItemSize</strong></a></p></td>
<td><p>(Microsoft Windows SDK のドキュメントで定義されている) 現在の WIA_IPA_FORMAT 設定に基づいて、イメージのバイト単位の幅とサイズを計算し、適切なプロパティに新しい値を書き込みます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550183" data-raw-source="[&lt;strong&gt;wiauStrC2C&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550183)"><strong>wiauStrC2C</strong></a></p></td>
<td><p>ANSI コピーは文字を ANSI 文字の文字列を別の文字列です。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550186" data-raw-source="[&lt;strong&gt;wiauStrC2W&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550186)"><strong>wiauStrC2W</strong></a></p></td>
<td><p>ANSI 文字の文字列を Unicode 文字列に変換します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550187" data-raw-source="[&lt;strong&gt;wiauStrW2C&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550187)"><strong>wiauStrW2C</strong></a></p></td>
<td><p>Unicode 文字列を ANSI 文字の文字列に変換します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550189" data-raw-source="[&lt;strong&gt;wiauStrW2W&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550189)"><strong>wiauStrW2W</strong></a></p></td>
<td><p>Unicode のコピーは、他の Unicode 文字列に文字列です。</p></td>
</tr>
</tbody>
</table>

 

 

 




