---
title: GUID_DEVINTERFACE_IMAGE
description: GUID_DEVINTERFACE_IMAGE
ms.assetid: 2768f0ef-3765-4a66-b480-0f75a7c49c3c
keywords:
- GUID_DEVINTERFACE_IMAGE デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_IMAGE
api_location:
- Wiaintfc.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 356480f1c4ce98332ad69428e4c9512d68892f52
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529168"
---
# <a name="guiddevinterfaceimage"></a>GUID_DEVINTERFACE_IMAGE


GUID_DEVINTERFACE_IMAGE[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている[WIA デバイスとデバイスのイメージ (まだ STI)](https://msdn.microsoft.com/library/windows/hardware/ff542729)デジタル カメラやスキャナーなど、します。

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
<td align="left"><p>GUID_DEVINTERFACE_IMAGE</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{6BDD1FC6-810F-11D0-BEC7-08002BE2092F}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

WIA デバイス用のシステム提供のカーネル モード ドライバーでは、オペレーティング システムと WIA デバイスの存在をアプリケーションに通知するこのデバイスのインターフェイス クラスのインスタンスを登録します。

WIA ドライバーと STI ドライバーについては、[Windows Image Acquisition ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff553346)を参照してください。

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
<td align="left"><p>Windows XP および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Wiaintfc.h (Wiaintfc.h を含む)</td>
</tr>
</tbody>
</table>

 

 





