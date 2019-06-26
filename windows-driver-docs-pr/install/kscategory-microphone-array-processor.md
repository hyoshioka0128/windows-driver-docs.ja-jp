---
title: KSCATEGORY_MICROPHONE_ARRAY_PROCESSOR
description: KSCATEGORY_MICROPHONE_ARRAY_PROCESSOR
ms.assetid: 812a9ec8-3b9e-4cf8-bf69-3b849ff6402a
keywords:
- KSCATEGORY_MICROPHONE_ARRAY_PROCESSOR デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_MICROPHONE_ARRAY_PROCESSOR
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9b98c362419475bc1f3b886e2da75f8bf88f0546
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387019"
---
# <a name="kscategorymicrophonearrayprocessor"></a>KSCATEGORY_MICROPHONE_ARRAY_PROCESSOR


KSCATEGORY_MICROPHONE_ARRAY_PROCESSOR[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)が定義されている、[カーネル ストリーミング](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)(KS) 機能のカテゴリを処理するマイク配列から入力します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
<th align="left">設定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>識別子</p></td>
<td align="left"><p>KSCATEGORY_MICROPHONE_ARRAY_PROCESSOR</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{830A44F2-A32D-476B-BE97-42845673B35A}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KS デバイス用のドライバーでは、オペレーティング システムに、デバイスが KSCATEGORY_MICROPHONE_ARRAY_PROCESSOR 機能カテゴリをサポートすることを示す KSCATEGORY_MICROPHONE_ARRAY_PROCESSOR のインスタンスを登録します。

オーディオ デバイスの機能のカテゴリの詳細については、次を参照してください[オーディオのアダプターのデバイスのインターフェイスをインストールする](https://docs.microsoft.com/windows-hardware/drivers/audio/installing-device-interfaces-for-an-audio-adapter)と[ **KSPROPERTY_TOPOLOGY_CATEGORIES** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-topology-categories) .

Windows Vista のマイク配列を処理する方法の詳細についてを参照してください、 [Windows Vista でのマイク配列サポート](https://go.microsoft.com/fwlink/p/?linkid=120592)と[方法の構築および Windows Vista のマイク配列を使用して](https://go.microsoft.com/fwlink/p/?linkid=120593)ホワイト ペーパー。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows Vista、Windows Server 2003、Windows XP、および以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY_TOPOLOGY_CATEGORIES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-topology-categories)

 

 






