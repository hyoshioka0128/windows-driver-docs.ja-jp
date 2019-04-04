---
title: KSMFT_CATEGORY_MULTIPLEXER
description: KSMFT_CATEGORY_MULTIPLEXER
ms.assetid: 79849eeb-7e5d-45bb-a0e4-cd6f413aa3dc
keywords:
- KSMFT_CATEGORY_MULTIPLEXER デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSMFT_CATEGORY_MULTIPLEXER
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 731e17f7619a9028b2abafb28960585defe48b2c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557551"
---
# <a name="ksmftcategorymultiplexer"></a>KSMFT_CATEGORY_MULTIPLEXER


KSMFT_CATEGORY_MULTIPLEXER[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている、[カーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff560842)(KS) 機能を組み合わせたデバイス カテゴリ (*多重化*)メディア ストリーム。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
<th align="left">設定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>識別子</p></td>
<td align="left"><p>KSMFT_CATEGORY_MULTIPLEXER</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{059c561e-05ae-4b61-b69d-55b61ee54a7b}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

MFT コーデックがサポートしている AVStream ドライバーは、デバイスが KSMFT_CATEGORY_MULTIPLEXER 機能カテゴリをサポートするオペレーティング システムに示すためにこのデバイスのインターフェイス クラスのインスタンスを登録します。

ハードウェアのコーデック サポート AVStream デバイスのデバイスのインターフェイス クラスの詳細については、[AVStream のコーデック サポートはハードウェアの概要](https://msdn.microsoft.com/library/windows/hardware/gg299325)を参照してください。

INF ファイルでこの機能のカテゴリを登録する方法の詳細については、次を参照してください、 *Hiddigi.inf*に含まれているファイルを、 *src\\入力\\hiddigi*サンプル。ドライバー WDK に含まれています。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

 

 





