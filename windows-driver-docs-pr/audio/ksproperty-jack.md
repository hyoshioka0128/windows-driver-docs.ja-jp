---
title: KSPROPERTY\_ジャック列挙型
description: KSPROPERTY\_ジャック列挙は、新しいプロパティのオーディオ ジャック構造体によって使用されている Id を定義します。
ms.assetid: d20a0b08-f20e-43a2-9ff5-eb0b9d1ea54e
keywords:
- KSPROPERTY_JACK 列挙オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_JACK
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a83cc08297fa57ff20ecc4c8a55edb2bc1b58c55
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332692"
---
# <a name="kspropertyjack-enumeration"></a>KSPROPERTY\_ジャック列挙型


`KSPROPERTY_JACK`列挙は、新しいプロパティのオーディオ ジャック構造体によって使用されている Id を定義します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef enum  { 
  KSPROPERTY_JACK_DESCRIPTION   = 1,
  KSPROPERTY_JACK_DESCRIPTION2  = 2,
  KSPROPERTY_JACK_SINK_INFO     = 3,
  KSPROPERTY_JACK_CONTAINERID
} KSPROPERTY_JACK;
```

<a name="constants"></a>定数
---------

<span id="KSPROPERTY_JACK_DESCRIPTION"></span><span id="ksproperty_jack_description"></span>**KSPROPERTY\_ジャック\_の説明**  
ID を指定します、 [ **KSPROPERTY\_ジャック\_説明**](ksproperty-jack-description.md)プロパティ。

<span id="KSPROPERTY_JACK_DESCRIPTION2"></span><span id="ksproperty_jack_description2"></span>**KSPROPERTY\_ジャック\_DESCRIPTION2**  
ID を指定します、 [ **KSPROPERTY\_ジャック\_DESCRIPTION2** ](ksproperty-jack-description2.md)プロパティ。

<span id="KSPROPERTY_JACK_SINK_INFO"></span><span id="ksproperty_jack_sink_info"></span>**KSPROPERTY\_ジャック\_シンク\_情報**  
ID を指定します、 [ **KSPROPERTY\_ジャック\_シンク\_情報**](ksproperty-jack-sink-info.md)プロパティ。

<span id="KSPROPERTY_JACK_CONTAINERID"></span><span id="ksproperty_jack_containerid"></span>**KSPROPERTY\_ジャック\_CONTAINERID**  
ID を指定します、 [ **KSPROPERTY\_ジャック\_CONTAINERID** ](ksproperty-jack-containerid.md)プロパティ。

<a name="remarks"></a>注釈
-------

なし

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
<td align="left"><p>Windows 7 およびそれ以降の Windows オペレーティング システムで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSPROPERTY\_ジャック\_の説明**](ksproperty-jack-description.md)

 

 






