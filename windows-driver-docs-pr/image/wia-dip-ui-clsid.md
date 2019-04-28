---
title: WIA\_DIP\_UI\_CLSID
description: WIA\_DIP\_UI\_CLSID プロパティには、WIA ミニドライバーがインストールされているユーザー インターフェイス (UI) 拡張機能の COM オブジェクトのクラスのベンダーから提供された id (CLSID) が含まれています。 WIA サービスは、作成し、このプロパティを保持します。
ms.assetid: 05b2bda0-d53d-44f9-89c0-e0f6f1fc2b48
keywords:
- WIA_DIP_UI_CLSID イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DIP_UI_CLSID
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2aeb57f2888f488882a9d2f5f5012b4670d90dff
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372993"
---
# <a name="wiadipuiclsid"></a>WIA\_DIP\_UI\_CLSID


WIA\_DIP\_UI\_CLSID プロパティには、WIA ミニドライバーがインストールされているユーザー インターフェイス (UI) 拡張機能の COM オブジェクトのクラスのベンダーから提供された id (CLSID) が含まれています。 WIA サービスは、作成し、このプロパティを保持します。

## <span id="ddk_wia_dip_ui_clsid_si"></span><span id="DDK_WIA_DIP_UI_CLSID_SI"></span>


プロパティの種類:VT\_BSTR

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

UI の CLSID 値に含まれる、WIA\_DIP\_UI\_CLSID プロパティは、ドライバーの INF ファイルから取得されます。 UI の CLSID を指定しない場合、WIA サービスは、既定値を提供します。 このプロパティが内部でのみ使用される UI が表示されている、WIA サービス。

<a name="requirements"></a>要件
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

 

 





