---
title: WIA\_DIP\_HW\_構成
description: WIA\_DIP\_HW\_構成プロパティがデバイスで使用する接続の種類を示します。 WIA サービスを作成して、このプロパティを保持し、WIA サービスのみが変更できます。
ms.assetid: c79e9651-120c-4f99-83d2-1920f7fccc73
keywords:
- WIA_DIP_HW_CONFIG イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DIP_HW_CONFIG
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe776eac82066be5213adfc4a91f9f96715b3b5c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551383"
---
# <a name="wiadiphwconfig"></a>WIA\_DIP\_HW\_構成


WIA\_DIP\_HW\_構成プロパティがデバイスで使用する接続の種類を示します。 WIA サービスを作成して、このプロパティを保持し、WIA サービスのみが変更できます。

## <span id="ddk_wia_dip_hw_config_si"></span><span id="DDK_WIA_DIP_HW_CONFIG_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

アプリケーションの読み取り、WIA\_DIP\_HW\_デバイスの接続の種類を決定するプロパティを構成します。

次の表では、使用可能な値を示します wia\_DIP\_HW\_構成します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p>汎用 WDM デバイス</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p>SCSI デバイス</p></td>
</tr>
<tr class="odd">
<td><p>4</p></td>
<td><p>USB デバイス</p></td>
</tr>
<tr class="even">
<td><p>8</p></td>
<td><p>シリアル デバイス</p></td>
</tr>
<tr class="odd">
<td><p>16</p></td>
<td><p>並列デバイス</p></td>
</tr>
</tbody>
</table>

 

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

 

 





