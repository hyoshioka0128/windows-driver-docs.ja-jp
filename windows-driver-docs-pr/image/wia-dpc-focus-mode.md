---
title: WIA\_DPC\_フォーカス\_モード
description: WIA\_DPC\_フォーカス\_モード プロパティは、カメラ デバイスの現在のフォーカス モードの設定を定義します。
ms.assetid: d651c9f7-97ca-4fa5-bc52-2af1f7c2e241
keywords:
- WIA_DPC_FOCUS_MODE イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPC_FOCUS_MODE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdbc16569ea16224d43678f9b3418421099343eb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535424"
---
# <a name="wiadpcfocusmode"></a>WIA\_DPC\_フォーカス\_モード


WIA\_DPC\_フォーカス\_モード プロパティは、カメラ デバイスの現在のフォーカス モードの設定を定義します。

## <span id="ddk_wia_dpc_focus_mode_si"></span><span id="DDK_WIA_DPC_FOCUS_MODE_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

デバイス ドライバー、WIA のサポートされている値を列挙する\_DPC\_フォーカス\_モード プロパティ、およびアプリケーションは、カメラ デバイス用のフォーカス モードを設定するには、このプロパティを書き込みます。

次の表は、WIA で有効な定数\_DPC\_フォーカス\_モード プロパティです。

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
<td><p>FOCUSMODE_AUTO</p></td>
<td><p>カメラのデバイスは、フォーカスに自動的に構成されます。</p></td>
</tr>
<tr class="even">
<td><p>FOCUSMODE_MACROAUTO</p></td>
<td><p>カメラ デバイスを短距離マクロの設定を使用して自動的に焦点を構成します。</p></td>
</tr>
<tr class="odd">
<td><p>FOCUSMODE_MANUAL</p></td>
<td><p>カメラ デバイスは、フォーカスにユーザーの許可を手動で構成されます。</p></td>
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

 

 





