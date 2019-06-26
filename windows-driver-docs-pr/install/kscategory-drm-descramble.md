---
title: KSCATEGORY_DRM_DESCRAMBLE
description: KSCATEGORY_DRM_DESCRAMBLE
ms.assetid: 3bb6887f-4fc9-452e-bceb-35fe26844ac5
keywords:
- KSCATEGORY_DRM_DESCRAMBLE デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_DRM_DESCRAMBLE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4f019caa5dae00c4ca4a4f9b1fe8e589bad91492
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387030"
---
# <a name="kscategorydrmdescramble"></a>KSCATEGORY_DRM_DESCRAMBLE


KSCATEGORY_DRM_DESCRAMBLE[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)が定義されている、[カーネル ストリーミング](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)wave の DRM で保護されたストリームを解読 (KS) 機能のカテゴリ。

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
<td align="left"><p>KSCATEGORY_DRM_DESCRAMBLE</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{FFBB6E3F-CCFE-4D84-90D9-421418B03A8E}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KS デバイス用のドライバーでは、オペレーティング システムに、デバイスが KSCATEGORY_DRM_DESCRAMBLE 機能カテゴリをサポートすることを示す KSCATEGORY_DRM_DESCRAMBLE のインスタンスを登録します。

この機能のカテゴリの詳細については、次を参照してください。[オーディオ アダプターのデバイスのインターフェイスをインストールする](https://docs.microsoft.com/windows-hardware/drivers/audio/installing-device-interfaces-for-an-audio-adapter)します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows Vista、Windows Server 2003、Windows XP、および以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

 

 





