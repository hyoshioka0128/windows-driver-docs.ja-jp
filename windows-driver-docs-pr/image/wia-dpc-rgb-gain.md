---
title: WIA\_DPC\_RGB\_を得る
description: WIA\_DPC\_RGB\_ゲイン プロパティが null で終わる Unicode 文字列それぞれ、赤、緑、および青の向上を表すイメージ データに適用されているにはが含まれています。
ms.assetid: 26448818-0885-4084-a0f3-c9e25d15dbf2
keywords:
- WIA_DPC_RGB_GAIN イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPC_RGB_GAIN
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88a3536a8f14dd75103352bfb170d1f471603b54
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392560"
---
# <a name="wiadpcrgbgain"></a>WIA\_DPC\_RGB\_を得る


WIA\_DPC\_RGB\_ゲイン プロパティが null で終わる Unicode 文字列それぞれ、赤、緑、および青の向上を表すイメージ データに適用されているにはが含まれています。 たとえば、"4: 25:50"4 の赤のゲイン、緑のゲイン 25、50 の青のゲインを表します。

## <span id="ddk_wia_dpc_rgb_gain_si"></span><span id="DDK_WIA_DPC_RGB_GAIN_SI"></span>


プロパティの種類:VT\_BSTR

有効な値 :WIA\_PROP\_NONE または WIA\_PROP\_一覧

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

WIA\_DPC\_RGB\_ゲイン プロパティは次のように解析されます。*R*:*G*:*B*します。 *R*赤のゲインを表す*G*緑のゲインを表すと*B*青のゲインを表します。 たとえば、赤の RGB 比率 = 4、緑 = 2, 青 = 3、「4:2:3」または「2000:1000:1500」RGB 文字列になります。 これらの値では、相互に比較しました。 追加の粒度のより多くを使用できますが、色を赤、緑、および青の比率が変わらない場合も同じになります。 このプロパティの値の文字列のパーサーは uint16 型の整数をサポートする必要があります*R*、 *G*、および*B*します。

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

 

 





