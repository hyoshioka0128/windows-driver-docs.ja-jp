---
title: WIA\_DPC\_露出\_コンポジション
description: WIA\_DPC\_露出\_COMP プロパティでは、デジタル カメラの自動露出の調整のポイントの設定を調整することができます。
ms.assetid: 4b3cb013-d5fa-4f9f-9d7b-43136fab0e30
keywords:
- WIA_DPC_EXPOSURE_COMP イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPC_EXPOSURE_COMP
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21c8a9b340f2c1d318ab253dbbf0d0acbff81965
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558512"
---
# <a name="wiadpcexposurecomp"></a>WIA\_DPC\_露出\_コンポジション


WIA\_DPC\_露出\_COMP プロパティでは、デジタル カメラの自動露出の調整のポイントの設定を調整することができます。

## <span id="ddk_wia_dpc_exposure_comp_si"></span><span id="DDK_WIA_DPC_EXPOSURE_COMP_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_範囲または WIA\_PROP\_一覧

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

WIA を使用する\_DPC\_露出\_COMP プロパティのデジタル カメラの露出度の自動管理ポイントの設定を調整します。 WIA を設定\_DPC\_露出\_COMP 0 には、出荷時設定の自動公開レベルは変わりません。

WIA 単位\_DPC\_露出\_COMP は値の小数部の停止のために、1000 倍でスケーリングが「停止」します。 WIA を設定\_DPC\_露出\_COMP を 2000年に対応する 2 つが停止 (センサーでは 4 倍以上にエネルギー) 公開のためのイメージは明るいになります。 WIA を設定\_DPC\_露出\_少ない露出 (30 分、エネルギー、センサー)、1 つの停止に対応して −1000 に COMP のためイメージが暗くなります。

設定値は、加法システムの写真の露出 (頂点) 単位でです。

このプロパティは、一覧または値の範囲のいずれかとして表される可能性があります。 デバイスがある場合のみ、このプロパティは通常使用、 [ **WIA\_DPC\_露出\_モード**](wia-dpc-exposure-mode.md) EXPOSUREMODE に設定するプロパティ\_手動です。

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


[**WIA\_DPC\_露出\_モード**](wia-dpc-exposure-mode.md)

 

 






