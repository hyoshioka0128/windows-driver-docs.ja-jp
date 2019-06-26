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
ms.openlocfilehash: 680bbb344db406625982b6c5a6891ea96d9fbbc1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361076"
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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kspin_physicalconnection" data-raw-source="[&lt;strong&gt;KSPIN_PHYSICALCONNECTION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kspin_physicalconnection)"><strong>KSPIN_PHYSICALCONNECTION</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSP を使用してこのプロパティを指定\_暗証番号 (pin)、メンバーが、関連する pin ファクトリを指定します。

KSPROPERTY\_PIN\_PHYSICALCONNECTION が型の構造体を返す[ **KSPIN\_PHYSICALCONNECTION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kspin_physicalconnection)、接続先を指定する**PinId**と接続されているフィルターのシンボリック リンクの名前。

クラス ドライバーは、このプロパティを処理しませんストリームのミニドライバーは、独自の処理を提供する必要があります。

オーディオのアダプターのドライバーとの接続を登録する[ **PcRegisterPhysicalConnection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcregisterphysicalconnection)します。

その後、SysAudio システム ドライバー (*sysaudio.sys*) このプロパティのクエリを実行し、それに応じてグラフをビルドします。 SysAudio では、このプロパティを使用して、どのトポロジー フィルター暗証番号 (pin) を wave フィルター ピンの配置の接続を確認します。

<a name="requirements"></a>必要条件
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


[**KSP\_暗証番号 (PIN)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin)

[**KSPIN\_PHYSICALCONNECTION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kspin_physicalconnection)

[**PcRegisterPhysicalConnection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcregisterphysicalconnection)

 

 






