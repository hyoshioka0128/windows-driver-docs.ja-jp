---
title: WIA\_DPC\_露出\_モード
description: WIA\_DPC\_露出\_モード プロパティは、カメラの現在の露出モードを示します。
ms.assetid: 30587d4f-5836-4030-9501-7612aaff58ae
keywords:
- WIA_DPC_EXPOSURE_MODE イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPC_EXPOSURE_MODE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69b533ecdd1c4be9efe7a0576e7c0d45dce6a205
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530072"
---
# <a name="wiadpcexposuremode"></a>WIA\_DPC\_露出\_モード


WIA\_DPC\_露出\_モード プロパティは、カメラの現在の露出モードを示します。

## <span id="ddk_wia_dpc_exposure_mode_si"></span><span id="DDK_WIA_DPC_EXPOSURE_MODE_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

アプリケーションの変更、WIA\_DPC\_露出\_モード プロパティは、カメラ デバイスの露出モードを制御するためです。

次の表に、WIA で有効な定数\_DPC\_露出\_モード。

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
<td><p>EXPOSUREMODE_APERTURE_PRIORITY</p></td>
<td><p>ユーザーが手動で絞りを設定し、カメラのデバイスがシャッター スピードを自動的に設定します。</p></td>
</tr>
<tr class="even">
<td><p>EXPOSUREMODE_AUTO</p></td>
<td><p>カメラ デバイスでは、開口部とシャッター スピードが自動的に設定します。</p></td>
</tr>
<tr class="odd">
<td><p>EXPOSUREMODE_MANUAL</p></td>
<td><p>ユーザーは、開口部とシャッター スピードを手動で設定します。</p></td>
</tr>
<tr class="even">
<td><p>EXPOSUREMODE_PROGRAM_ACTION</p></td>
<td><p>カメラのデバイスが自動的に絞りとシャッター スピードを設定し、主題 (つまり、速い動きを含むシーン) を移動するために最適化します。</p></td>
</tr>
<tr class="odd">
<td><p>EXPOSUREMODE_PROGRAM_CREATIVE</p></td>
<td><p>カメラのデバイスが自動的に絞りとシャッター スピードを設定しの主題ではまだそれらを最適化します。</p></td>
</tr>
<tr class="even">
<td><p>EXPOSUREMODE_PORTRAIT</p></td>
<td><p>カメラ デバイスが自動的に絞りとシャッター スピードを設定し、それらが縦の写真を最適化します。</p></td>
</tr>
<tr class="odd">
<td><p>EXPOSUREMODE_SHUTTER_PRIORITY</p></td>
<td><p>ユーザーはシャッター スピード、手動で設定し、カメラのデバイスが自動的の開口部を設定します。</p></td>
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

 

 





