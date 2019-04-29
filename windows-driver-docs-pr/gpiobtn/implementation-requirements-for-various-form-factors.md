---
title: さまざまなフォーム ファクターの実装要件
description: このトピックでは、さまざまなフォーム ファクターの実装要件について説明します。
ms.assetid: F14E9811-B432-409B-B7AD-262C2DD76C25
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5258792f41cd95ad657126de2226c193a78b4f20
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323282"
---
# <a name="implementation-requirements-for-various-form-factors"></a>さまざまなフォーム ファクターの実装要件


このトピックでは、さまざまなフォーム ファクターの実装要件について説明します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"></th>
<th align="left">フォーム ファクター</th>
<th align="left">定義</th>
<th align="left">GPIO インジケーターの実装要件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><img src="images/slate.jpg" alt="Slate" /></p></td>
<td align="left">スレート</td>
<td align="left">アタッチ可能なキーボードがないとタブレット フォーム ファクター</td>
<td align="left">静止ドッキング アクセサリが利用できる場合は、ドッキング インジケーターを実装しなければなりません。</td>
</tr>
<tr class="even">
<td align="left"><p><img src="images/laptop.jpg" alt="Laptop" /></p></td>
<td align="left">ノート PC</td>
<td align="left">入力可能な常に完全に接続されているキーボード。</td>
<td align="left">静的にラップトップ モードを設定します。</td>
</tr>
<tr class="odd">
<td align="left"><p><img src="images/convertible.jpg" alt="Convertible" /></p></td>
<td align="left">Convertible</td>
<td align="left">スレート型またはタブレットのいずれかとして使用できるシステム。 キーボードは、デタッチ、反転、または swivelled ことができます。</td>
<td align="left"><p>ラップトップ/スレート インジケーターを実装します。</p>
<p>静止ドッキング アクセサリを使用できる場合、ドッキング インジケーターも実装する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><img src="images/allinone.jpg" alt="All-in-One" /></p></td>
<td align="left">すべて 1 つ</td>
<td align="left">中規模デスクトップ/半 portable システム アクセサリとして添付されているキーボードです。</td>
<td align="left">キーボードがオプションの付属品であるために必要な実装はありません。</td>
</tr>
</tbody>
</table>

 

 

 




