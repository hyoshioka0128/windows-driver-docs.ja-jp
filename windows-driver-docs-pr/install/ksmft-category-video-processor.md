---
title: KSMFT_CATEGORY_VIDEO_PROCESSOR
description: KSMFT_CATEGORY_VIDEO_PROCESSOR
ms.assetid: 9d27cea3-0d4f-4812-9e87-0b2295c99a5f
keywords:
- KSMFT_CATEGORY_VIDEO_PROCESSOR デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSMFT_CATEGORY_VIDEO_PROCESSOR
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1f73e8632684c573b7659da11f3211f81e94d733
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365827"
---
# <a name="ksmftcategoryvideoprocessor"></a>KSMFT_CATEGORY_VIDEO_PROCESSOR


KSMFT_CATEGORY_VIDEO_PROCESSOR[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)が定義されている、[カーネル ストリーミング](https://docs.microsoft.com/windows-hardware/drivers/stream/kernel-streaming)ビデオ デバイスの機能のカテゴリ (KS)。

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
<td align="left"><p>KSMFT_CATEGORY_VIDEO_PROCESSOR</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{302ea3fc-aa5f-47f9-9f7a-c2188bb16302}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

MFT コーデックがサポートしている AVStream ドライバーは、デバイスが KSMFT_CATEGORY_VIDEO_PROCESSOR 機能カテゴリをサポートするオペレーティング システムに示すためにこのデバイスのインターフェイス クラスのインスタンスを登録します。

ハードウェアのコーデック サポート AVStream デバイスのデバイスのインターフェイス クラスの詳細については、次を参照してください。 [AVStream のコーデック サポートはハードウェアの概要](https://docs.microsoft.com/windows-hardware/drivers/stream/getting-started-with-hardware-codec-support-in-avstream)します。

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

 

 





