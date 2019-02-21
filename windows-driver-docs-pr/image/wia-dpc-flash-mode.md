---
title: WIA\_DPC\_FLASH\_モード
description: WIA\_DPC\_FLASH\_モード プロパティは、カメラ デバイスの現在のフラッシュ モード設定を定義します。 デバイス ドライバーが、このプロパティのサポートされている値を列挙し、アプリケーションがデバイスのカメラのフラッシュ モードを設定するには、このプロパティを書き込みます。
ms.assetid: 04c58111-09a7-4cd0-b60b-a65197c0931d
keywords:
- WIA_DPC_FLASH_MODE イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPC_FLASH_MODE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 540a507e05defd8be5fc72e385815bbf6824a7a4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529536"
---
# <a name="wiadpcflashmode"></a>WIA\_DPC\_FLASH\_モード


WIA\_DPC\_FLASH\_モード プロパティは、カメラ デバイスの現在のフラッシュ モード設定を定義します。 デバイス ドライバーが、このプロパティのサポートされている値を列挙し、アプリケーションがデバイスのカメラのフラッシュ モードを設定するには、このプロパティを書き込みます。

## <span id="ddk_wia_dpc_flash_mode_si"></span><span id="DDK_WIA_DPC_FLASH_MODE_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

次の表では、このプロパティを持つ有効な 6 つについて説明します。

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
<td><p>FLASHMODE_AUTO</p></td>
<td><p>カメラのデバイスは、フラッシュの適切な設定を決定します。</p></td>
</tr>
<tr class="even">
<td><p>FLASHMODE_EXTERNALSYNC</p></td>
<td><p>カメラのデバイスは、外部の flash ユニットとの同期に構成されます。</p></td>
</tr>
<tr class="odd">
<td><p>FLASHMODE_FILL</p></td>
<td><p>カメラのデバイスは、現在の照明条件に関係なく flash に構成されます。</p></td>
</tr>
<tr class="even">
<td><p>FLASHMODE_OFF</p></td>
<td><p>カメラ デバイスの構成が<em>いない</em>を撮影した画像を任意のフラッシュします。</p></td>
</tr>
<tr class="odd">
<td><p>FLASHMODE_REDEYE_AUTO</p></td>
<td><p>カメラ デバイスは、現在の照明条件に関係なく、赤目の削減を使用して、フラッシュの適切な設定を決定します。</p></td>
</tr>
<tr class="even">
<td><p>FLASHMODE_REDEYE_FILL</p></td>
<td><p>赤目減少を使用して、現在の照明条件に関係なく flash カメラ デバイスを構成します。</p></td>
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
<td><p>バージョン</p></td>
<td><p>Windows Vista 以降のオペレーティング システムで古いものであり使用できなくする必要があります。 ただし、アプリケーションやデバイス向けの Windows Server 2003、Windows XP、および Windows の以前のバージョンと互換性のこのプロパティが現在も Windows Vista で定義します。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

 

 





