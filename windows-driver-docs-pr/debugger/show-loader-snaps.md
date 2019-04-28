---
title: Show loader snaps
description: Show loader snaps
ms.assetid: fb3843fe-451f-444c-a690-862253df944e
keywords:
- ローダー (グローバル フラグ) のスナップを表示します。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 565841af185edf5ca38827643f8f3820a04354df
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368117"
---
# <a name="show-loader-snaps"></a>Show loader snaps


## <span id="ddk_show_loader_snaps_dtools"></span><span id="DDK_SHOW_LOADER_SNAPS_DTOOLS"></span>


**ローダーのスナップを表示する**フラグは、読み込みと実行可能イメージおよびそのサポート ライブラリ モジュールをアンロードに関する詳細情報をキャプチャし、カーネル デバッガーのコンソールで、データが表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>省略形</strong></p></td>
<td align="left"><p>sls</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16 進数の値</strong></p></td>
<td align="left"><p>0x2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>シンボリック名</strong></p></td>
<td align="left"><p>FLG_SHOW_LDR_SNAPS</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Destination (公開先)</strong></p></td>
<td align="left"><p>システム全体のレジストリ エントリ、カーネルのフラグ、イメージ ファイルのレジストリ エントリ</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

システム全体の (レジストリまたはカーネル フラグ)、このフラグはドライバーの読み込みとアンロードの操作に関する情報が表示されます。

プロセスごとの (イメージ ファイル) では、このフラグは、Dll の読み込みとアンロードの情報を表示します。

 

 





