---
title: KSPROPERTY\_AUDIOMODULE 列挙型
description: KSPROPERTY\_AUDIOMODULE 列挙型は、オーディオ ドライバーによって通信パートナーに関する情報は、オーディオのモジュールを定義するために使用される定数を定義します。
ms.assetid: 94873A4A-A40F-40A7-B7A2-B693A5253714
keywords:
- KSPROPERTY_AUDIOMODULE 列挙オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOMODULE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6eb2abca346f8b6d4419ac83a66d57a7a28dd6aa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358817"
---
# <a name="kspropertyaudiomodule-enumeration"></a>KSPROPERTY\_AUDIOMODULE 列挙型


KSPROPERTY\_AUDIOMODULE 列挙型は、オーディオ ドライバーによって通信パートナーに関する情報は、オーディオのモジュールを定義するために使用される定数を定義します。

オーディオのモジュールの詳細については、次を参照してください。[オーディオ モジュールの検出を実装する](https://docs.microsoft.com/windows-hardware/drivers/audio/implementing-audio-module-communication)します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef enum  { 
  KSPROPERTY_AUDIOMODULE_DESCRIPTORS             = 1,
  KSPROPERTY_AUDIOMODULE_COMMAND                 = 2,
  KSPROPERTY_AUDIOMODULE_NOTIFICATION_DEVICE_ID  = 3
} KSPROPERTY_AUDIOMODULE;
```

<a name="constants"></a>定数
---------

<span id="KSPROPERTY_AUDIOMODULE_DESCRIPTORS__"></span><span id="ksproperty_audiomodule_descriptors__"></span>**KSPROPERTY\_AUDIOMODULE\_記述子**   
ID を指定します、 [ **KSPROPERTY\_AUDIOMODULE\_記述子**](ksproperty-audiomodule-descriptors.md)プロパティ。

<span id="KSPROPERTY_AUDIOMODULE_COMMAND"></span><span id="ksproperty_audiomodule_command"></span>**KSPROPERTY\_AUDIOMODULE\_コマンド**  
ID を指定します、 [ **KSPROPERTY\_AUDIOMODULE\_コマンド**](ksproperty-audiomodule-command.md)プロパティ。

<span id="KSPROPERTY_AUDIOMODULE_NOTIFICATION_DEVICE_ID"></span><span id="ksproperty_audiomodule_notification_device_id"></span>**KSPROPERTY\_AUDIOMODULE\_通知\_デバイス\_ID**  
ID を指定します、 [ **KSPROPERTY\_AUDIOMODULE\_通知\_デバイス\_ID** ](ksproperty-audiomodule-notification-device-id.md)プロパティ。

<a name="remarks"></a>注釈
-------

KS プロパティのすべての呼び出しする必要がありますが非ブロッキング ハードウェア効果が処理チェーンの一部であるため、待機する必要があります。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>サポートされている最小のクライアント</p></td>
<td align="left"><p>Windows 10 バージョン 1703</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている最小のサーバー</p></td>
<td align="left"><p>サポートなし</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[KSPROPSETID\_AudioModule](kspropsetid-audiomodule.md)

 

 






