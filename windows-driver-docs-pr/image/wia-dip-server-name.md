---
title: WIA\_DIP\_SERVER\_名
description: WIA\_DIP\_SERVER\_NAME プロパティには、WIA ミニドライバーがで実行されているサーバーの名前が含まれています。
ms.assetid: 93fec2b1-dc41-48cf-990b-f6aa99133835
keywords:
- WIA_DIP_SERVER_NAME イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DIP_SERVER_NAME
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8588167c9e7d0c22808f2329bc22b3925d3b27e6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373002"
---
# <a name="wiadipservername"></a>WIA\_DIP\_SERVER\_名


WIA\_DIP\_SERVER\_NAME プロパティには、WIA ミニドライバーがで実行されているサーバーの名前が含まれています。

## <span id="ddk_wia_dip_server_name_si"></span><span id="DDK_WIA_DIP_SERVER_NAME_SI"></span>


プロパティの種類:VT\_BSTR

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

WIA の既定値\_DIP\_SERVER\_名が"local"です。 このプロパティは、アプリケーションが同じコンピューター上のデバイスに接続されているときに、"local"の文字列を含める必要があります。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Microsoft Windows XP およびそれ以降のオペレーティング システムの省略可能。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

 

 





