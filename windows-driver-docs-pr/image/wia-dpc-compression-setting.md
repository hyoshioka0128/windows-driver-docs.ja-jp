---
title: WIA\_DPC\_圧縮\_設定
description: WIA\_DPC\_圧縮\_プロパティ設定にはでは、範囲または見かけ上のイメージ品質を表す整数のリストのいずれかが含まれています。
ms.assetid: dfe22ff2-f613-49a5-8c55-38ba851e7ebd
keywords:
- WIA_DPC_COMPRESSION_SETTING イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPC_COMPRESSION_SETTING
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22a065d99a0c19f47d8a516a6f636a88a073cb4c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578523"
---
# <a name="wiadpccompressionsetting"></a>WIA\_DPC\_圧縮\_設定


WIA\_DPC\_圧縮\_プロパティ設定にはでは、範囲または見かけ上のイメージ品質を表す整数のリストのいずれかが含まれています。

## <span id="ddk_wia_dpc_compression_setting_si"></span><span id="DDK_WIA_DPC_COMPRESSION_SETTING_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_リストまたは WIA\_PROP\_範囲

アクセス権:読み取り/書き込み

<a name="remarks"></a>コメント
-------

WIA\_DPC\_圧縮\_約シーンのコンテンツの広範な範囲に見かけ上のイメージ品質を直線的に記述するプロパティの設定が対象としています。 小さい整数は低い画質 (つまり、最大圧縮) を表しより大きな整数が高品質 (つまり、最小限の圧縮) を表します。 デバイス上の任意の使用可能な設定は、そのデバイスにのみ相対デバイスに固有であるためです。

<a name="requirements"></a>必要条件
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

 

 





