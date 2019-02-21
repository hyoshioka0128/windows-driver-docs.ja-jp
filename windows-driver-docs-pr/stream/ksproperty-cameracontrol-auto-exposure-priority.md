---
title: KSPROPERTY\_CAMERACONTROL\_自動\_露出\_優先順位
description: KSPROPERTY\_CAMERACONTROL\_自動\_露出\_PRIORITY プロパティは、デバイスでフレーム レートを動的に変更できるかどうかを指定します。
ms.assetid: 0e20a4ee-b672-4c9a-9003-c2defd378e7c
keywords:
- KSPROPERTY_CAMERACONTROL_AUTO_EXPOSURE_PRIORITY ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_AUTO_EXPOSURE_PRIORITY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4281db54d2058600cd2c96ade9d4a3edefab852
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550120"
---
# <a name="kspropertycameracontrolautoexposurepriority"></a>KSPROPERTY\_CAMERACONTROL\_自動\_露出\_優先順位


KSPROPERTY\_CAMERACONTROL\_自動\_露出\_PRIORITY プロパティは、デバイスでフレーム レートを動的に変更できるかどうかを指定します。

### <a name="usage-summary-table"></a>使用状況の概要テーブル

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>取得</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>フィルターまたはノード</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564439" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564439)"><strong>KSPROPERTY_CAMERACONTROL_S</strong></a>, <a href="https://msdn.microsoft.com/library/windows/hardware/ff564420" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564420)"><strong>KSPROPERTY_CAMERACONTROL_NODE_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、デバイスでフレーム レートを動的に変化するかどうかを指定する ULONG です。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>フレーム レートは定数である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p>デバイスにより、フレーム レートが動的に変更できます。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

自動露出の優先順位は、カメラで照明条件に応じて、フレーム レートを動的に変更できるかどうかを判断します。

露出度の自動せず、フレーム レートが 30 fps の場合は公開期間を超えることはできません 33 ms。

、優先度が露出度の自動ただし、カメラでした補正光の低フレーム レートが減少します。 たとえば、カメラは 25 fps のために 40 ミリ秒の露出時間を長くフレーム レートを減らすことができます。

KSPROPERTY\_CAMERACONTROL\_自動\_露出\_に優先順位のマップ、**光量不足の補正**USB ビデオ クラスのプロパティ ページ チェック ボックス。

KSPROPERTY を使用するには\_CAMERACONTROL\_自動\_露出\_、優先順位を設定する必要がある[ **KSPROPERTY\_CAMERACONTROL\_露出**](ksproperty-cameracontrol-exposure.md)を auto にします。つまり、カメラは、有効なオプションを使用する優先順位の露出自動モードの露出度の自動モードでなければなりません。

KSPROPERTY の既定値\_CAMERACONTROL\_自動\_露出\_優先順位は 0 です。

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
<td><p>Windows Vista および Windows オペレーティング システムの以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY\_CAMERACONTROL\_S**](https://msdn.microsoft.com/library/windows/hardware/ff564439)

[**KSPROPERTY\_CAMERACONTROL\_ノード\_S**](https://msdn.microsoft.com/library/windows/hardware/ff564420)

 

 






