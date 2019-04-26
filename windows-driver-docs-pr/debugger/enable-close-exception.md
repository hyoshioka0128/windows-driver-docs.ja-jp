---
title: Enable close exception
description: Enable close exception
ms.assetid: 4089df14-3204-4a48-b67f-cf6bd53100a5
keywords:
- 閉じる例外 (グローバル フラグ) を有効にします。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47bd62aa61664b6a25b5e15b1badf8e023d03932
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353642"
---
# <a name="enable-close-exception"></a>Enable close exception


## <span id="ddk_enable_close_exception_dtools"></span><span id="DDK_ENABLE_CLOSE_EXCEPTION_DTOOLS"></span>


**閉じる例外を有効にする**に無効なハンドルが渡されるたびに、フラグがユーザー モード例外を発生させる、 **CloseHandle**インターフェイスまたは関連のインターフェイスなど**SetEvent**、引数としてハンドルを受け取る。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>省略形</strong></p></td>
<td align="left"><p>ece</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16 進数の値</strong></p></td>
<td align="left"><p>0x00400000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>シンボリック名</strong></p></td>
<td align="left"><p>FLG_ENABLE_CLOSE_EXCEPTIONS</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Destination (公開先)</strong></p></td>
<td align="left"><p>システム全体のレジストリ エントリ、カーネル フラグ</p></td>
</tr>
</tbody>
</table>

 

**注**  このフラグがまだサポートされていますが、[不適切なハンドルの検出を有効にする](enable-bad-handles-detection.md)ハンドルの使用のより包括的なチェックを実行するには、フラグ (bhd) をお勧めします。

 

 

 





