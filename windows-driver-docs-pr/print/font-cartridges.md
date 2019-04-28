---
title: フォント カートリッジ
description: フォント カートリッジ
ms.assetid: bc92e2eb-ea75-4f0f-85b7-1433d57401f3
keywords:
- WDK Unidrv、カートリッジ プリンターのフォントの記述
- フォントのカートリッジ WDK Unidrv
- カートリッジ フォント WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f64d4221595535ea98167d82b1ef55a4a062178
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372109"
---
# <a name="font-cartridges"></a>フォント カートリッジ





カートリッジによって記述可能プリンターがフォント カートリッジを受け入れる場合\* **FontCartridge** GPD ファイルのエントリ。 このエントリの形式です。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>* FontCartridge:<em>CartridgeName</em> {<em>FontCartidgeAttributes</em>}</p></td>
</tr>
</tbody>
</table>

 

場所*CartridgeName*カートリッジの名前を表すテキスト文字列と*FontCartridgeAttributes*は 1 つまたは複数のセットです[フォント カートリッジ属性](font-cartridge-attributes.md)します。

使用してフォント カートリッジによって提供されるフォントを指定できますまた、 [Unidrv フォント形式ファイル](customized-font-management.md#ddk-unidrv-font-format-files-gg)(.uff ファイル)。 通常、少ない一般的に使用されるカートリッジは .uff ファイルで指定 GPD ファイルで最も一般的に指定されたフォントのカートリッジは説明します。

 

 




