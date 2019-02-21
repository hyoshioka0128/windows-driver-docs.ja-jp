---
title: WIA\_DPC\_露出\_インデックス
description: WIA\_DPC\_露出\_インデックスのプロパティでは、デジタル カメラのフィルム速度の設定をエミュレートすることができます。
ms.assetid: 805efbf0-b81f-49fd-82be-536d471d255e
keywords:
- WIA_DPC_EXPOSURE_INDEX イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPC_EXPOSURE_INDEX
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c62e9f1a6c8663cc9b9a6e06df370825e48a4dbb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549530"
---
# <a name="wiadpcexposureindex"></a>WIA\_DPC\_露出\_インデックス


WIA\_DPC\_露出\_インデックスのプロパティでは、デジタル カメラのフィルム速度の設定をエミュレートすることができます。

## <span id="ddk_wia_dpc_exposure_index_si"></span><span id="DDK_WIA_DPC_EXPOSURE_INDEX_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_リストまたは WIA\_PROP\_範囲

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

フィルム速度の設定は、ISO の指定 (ASA/DIN) に対応します。 通常、デバイスは、不連続の列挙値をサポートしていますが、値の範囲に継続的に制御が可能。 値が 0 xffff は、WIA の\_DPC\_露出\_インデックス プロパティは、自動の ISO 設定に対応します。

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
<td><p>Windows Vista 以降のオペレーティング システムで古いものであり使用できなくする必要があります。 ただし、アプリケーションやデバイス向けの Windows Server 2003、Windows XP、および Windows の以前のバージョンと互換性のこのプロパティが現在も Windows Vista で定義します。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

 

 





