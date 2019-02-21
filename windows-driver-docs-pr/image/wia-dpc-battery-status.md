---
title: WIA\_DPC\_バッテリ\_状態
description: WIA\_DPC\_バッテリ\_STATUS プロパティはカメラ デバイスの動作に残されているバッテリの割合を定義します。
ms.assetid: d6e50c77-9c30-4091-9d6e-7215907ba87b
keywords:
- WIA_DPC_BATTERY_STATUS イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPC_BATTERY_STATUS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 677b50e28c9b68acf85a35b15a3431399ac1f524
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552840"
---
# <a name="wiadpcbatterystatus"></a>WIA\_DPC\_バッテリ\_状態


WIA\_DPC\_バッテリ\_STATUS プロパティはカメラ デバイスの動作に残されているバッテリの割合を定義します。

## <span id="ddk_wia_dpc_battery_status_si"></span><span id="DDK_WIA_DPC_BATTERY_STATUS_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

値の WIA\_DPC\_バッテリ\_STATUS プロパティは、0 ~ 100 の整数。 アプリケーションでは、カメラ デバイスのバッテリ残量を確認するには、このプロパティを読み取ります。

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

 

 





