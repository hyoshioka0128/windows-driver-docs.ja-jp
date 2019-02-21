---
title: WIA\_DPC\_デジタル\_ズーム
description: WIA\_DPC\_デジタル\_ズーム プロパティには 10 倍でスケーリングのデジタル カメラの買収したイメージの有効なズームの比率が含まれています。
ms.assetid: 5f1ec791-fd51-4397-ac7d-5012c020ef0a
keywords:
- WIA_DPC_DIGITAL_ZOOM イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPC_DIGITAL_ZOOM
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72220258d68750b6fb2c9e06d53bf51ab79e6767
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558502"
---
# <a name="wiadpcdigitalzoom"></a>WIA\_DPC\_デジタル\_ズーム


WIA\_DPC\_デジタル\_ズーム プロパティには 10 倍でスケーリングのデジタル カメラの買収したイメージの有効なズームの比率が含まれています。

## <span id="ddk_wia_dpc_digital_zoom_si"></span><span id="DDK_WIA_DPC_DIGITAL_ZOOM_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_リストまたは WIA\_PROP\_範囲

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

WIA\_DPC\_デジタル\_ズーム値は 10 ですが、カメラをキャプチャする標準のシーンのサイズは、デジタル ズーム (1 X) がない場合に対応します。 20 の値は、カメラがシーンの標準サイズの 4 分の 1 をキャプチャ、2 X ズームに対応します。

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

 

 





