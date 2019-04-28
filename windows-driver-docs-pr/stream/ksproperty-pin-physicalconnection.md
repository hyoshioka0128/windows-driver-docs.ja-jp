---
title: KSPROPERTY\_PIN\_PHYSICALCONNECTION
description: オーディオ アダプター ドライバーの使用、KSPROPERTY\_PIN\_ミニポート間の物理接続を示す PHYSICALCONNECTION プロパティ。
ms.assetid: a679ce41-93d2-4b46-a26d-ce05408ec6aa
keywords:
- KSPROPERTY_PIN_PHYSICALCONNECTION ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_PHYSICALCONNECTION
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 703931775a142b58171de66a402dd6680243395c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380808"
---
# <a name="kspropertypinphysicalconnection"></a>KSPROPERTY\_PIN\_PHYSICALCONNECTION


オーディオ アダプター ドライバーの使用、KSPROPERTY\_PIN\_ミニポート間の物理接続を示す PHYSICALCONNECTION プロパティ。

## <span id="ddk_ksproperty_pin_physicalconnection_ks"></span><span id="DDK_KSPROPERTY_PIN_PHYSICALCONNECTION_KS"></span>


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
<td><p>いいえ</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566722" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566722)"><strong>KSP_PIN</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563539" data-raw-source="[&lt;strong&gt;KSPIN_PHYSICALCONNECTION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563539)"><strong>KSPIN_PHYSICALCONNECTION</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSP を使用してこのプロパティを指定\_暗証番号 (pin)、メンバーが、関連する pin ファクトリを指定します。

KSPROPERTY\_PIN\_PHYSICALCONNECTION が型の構造体を返す[ **KSPIN\_PHYSICALCONNECTION**](https://msdn.microsoft.com/library/windows/hardware/ff563539)、接続先を指定する**PinId**と接続されているフィルターのシンボリック リンクの名前。

クラス ドライバーは、このプロパティを処理しませんストリームのミニドライバーは、独自の処理を提供する必要があります。

オーディオのアダプターのドライバーとの接続を登録する[ **PcRegisterPhysicalConnection**](https://msdn.microsoft.com/library/windows/hardware/ff537726)します。

その後、SysAudio システム ドライバー (*sysaudio.sys*) このプロパティのクエリを実行し、それに応じてグラフをビルドします。 SysAudio では、このプロパティを使用して、どのトポロジー フィルター暗証番号 (pin) を wave フィルター ピンの配置の接続を確認します。

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
<td>Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSP\_暗証番号 (PIN)**](https://msdn.microsoft.com/library/windows/hardware/ff566722)

[**KSPIN\_PHYSICALCONNECTION**](https://msdn.microsoft.com/library/windows/hardware/ff563539)

[**PcRegisterPhysicalConnection**](https://msdn.microsoft.com/library/windows/hardware/ff537726)

 

 






