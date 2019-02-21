---
title: WIA\_DPC\_THUMB\_幅
description: WIA\_DPC\_THUMB\_WIDTH プロパティ (ピクセル単位)、新しくキャプチャしたイメージを使用するサムネイル イメージの幅を定義します。
ms.assetid: 01136695-9bef-4d47-89df-fb1d14465bef
keywords:
- WIA_DPC_THUMB_WIDTH イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPC_THUMB_WIDTH
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: de4278fc0413aa89186e43482d2c6684b40bea25
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527813"
---
# <a name="wiadpcthumbwidth"></a>WIA\_DPC\_THUMB\_幅


WIA\_DPC\_THUMB\_WIDTH プロパティ (ピクセル単位)、新しくキャプチャしたイメージを使用するサムネイル イメージの幅を定義します。

## <span id="ddk_wia_dpc_thumb_width_si"></span><span id="DDK_WIA_DPC_THUMB_WIDTH_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_NONE の場合、または WIA\_PROP\_一覧

アクセス権:読み取り専用または読み取り/書き込み

<a name="remarks"></a>注釈
-------

アプリケーションの読み取り、WIA\_DPC\_THUMB\_ユーザー インターフェイスでサムネイル画像を表示するための推定サイズを取得する幅の値。

場合、値または WIA\_DPC\_THUMB\_幅が WIA\_PROP\_、アクセス権があります読み取り専用。 値は、WIA 場合\_PROP\_一覧で、アクセス権は読み取り/書き込みである必要があります。

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

## <a name="see-also"></a>関連項目


[**WIA\_DPC\_THUMB\_高さ**](wia-dpc-thumb-height.md)

 

 






