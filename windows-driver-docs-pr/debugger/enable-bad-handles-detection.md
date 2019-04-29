---
title: Enable bad handles detection
description: Enable bad handles detection
ms.assetid: beeecb82-a270-416e-8a2a-dd64af3d052e
keywords:
- 無効なハンドルの検出 (グローバル フラグ) を有効にします。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8900ace3d7395e6fac8b4557a756a397bfeb2fb5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323386"
---
# <a name="enable-bad-handles-detection"></a>Enable bad handles detection


## <span id="ddk_enable_bad_handles_detection_dtools"></span><span id="DDK_ENABLE_BAD_HANDLES_DETECTION_DTOOLS"></span>


**不適切なハンドルの検出を有効にする**フラグは、ユーザー モード例外を発生させます (ステータス\_無効な\_処理) たびに、ユーザー モード プロセスは無効なハンドル オブジェクト マネージャーにします。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>省略形</strong></p></td>
<td align="left"><p>bhd</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16 進数の値</strong></p></td>
<td align="left"><p>0x40000000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>シンボリック名</strong></p></td>
<td align="left"><p>FLG_ENABLE_HANDLE_EXCEPTIONS</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Destination (公開先)</strong></p></td>
<td align="left"><p>システム全体のレジストリ エントリ、カーネル フラグ</p></td>
</tr>
</tbody>
</table>

 

 

 





