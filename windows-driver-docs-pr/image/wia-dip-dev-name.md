---
title: WIA\_DIP\_DEV\_名
description: WIA\_DIP\_DEV\_NAME プロパティには、デバイスの名前が含まれています。 WIA サービスは、作成し、このプロパティを保持します。
ms.assetid: 9e1bdc00-b46f-4c20-bcc4-f3caa4820983
keywords:
- WIA_DIP_DEV_NAME イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DIP_DEV_NAME
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 209c46de89254fe0c83d27d162374ee52016db64
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365919"
---
# <a name="wiadipdevname"></a>WIA\_DIP\_DEV\_名


WIA\_DIP\_DEV\_NAME プロパティには、デバイスの名前が含まれています。 WIA サービスは、作成し、このプロパティを保持します。

## <span id="ddk_wia_dip_dev_name_si"></span><span id="DDK_WIA_DIP_DEV_NAME_SI"></span>


プロパティの種類:VT\_BSTR

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

デバイス名に含まれる、WIA\_DIP\_DEV\_NAME プロパティは、ドライバーの INF ファイルから取得されます。 アプリケーションでは、デバイスの名前を取得するには、このプロパティを読み取ります。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

 

 





