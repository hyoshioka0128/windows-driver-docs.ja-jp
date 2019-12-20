---
title: Create kernel mode stack trace database
description: Create kernel mode stack trace database
ms.assetid: 0c1f94c0-ebc7-4e3c-8101-ba3cf830e7f8
keywords:
- カーネルモードスタックトレースデータベースの作成 (グローバルフラグ)
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ffd8b0741010cdf1737d3026d455d55b7e6ad11
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209310"
---
# <a name="create-kernel-mode-stack-trace-database"></a>Create kernel mode stack trace database


## <span id="ddk_create_kernel_mode_stack_trace_database_dtools"></span><span id="DDK_CREATE_KERNEL_MODE_STACK_TRACE_DATABASE_DTOOLS"></span>


"**カーネルモードスタックトレースデータベースの作成**" フラグは、リソースオブジェクトやオブジェクト管理操作などのカーネル操作の実行時スタックトレースデータベースを作成し、Windows のチェックされたビルドを使用する場合にのみ機能します。 チェックされたビルドは、Windows 10 バージョン1803より前の以前のバージョンの Windows で使用できました。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>省略形</strong></p></td>
<td align="left"><p>kst</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16進数値</strong></p></td>
<td align="left"><p>0x2000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>シンボリック名</strong></p></td>
<td align="left"><p>FLG_KERNEL_STACK_TRACE_DB</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Destination (公開先)</strong></p></td>
<td align="left"><p>システム全体のレジストリエントリ</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>Comments

GFlags は、このフラグをカーネルフラグ設定として表示しますが、カーネルが既に起動しているため、実行時には有効ではありません。

 

 





