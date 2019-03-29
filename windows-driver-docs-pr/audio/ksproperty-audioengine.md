---
title: KSPROPERTY\_AUDIOENGINE 列挙型
description: 含まれる、KSPROPSETID プロパティ\_AudioEngine プロパティ セットは、この列挙体によって定義され、KSNODETYPE でサポートする必要\_オーディオ\_エンジン ノード。
ms.assetid: F20C05A3-C8A0-4061-93B9-03FD19D37C82
keywords:
- KSPROPERTY_AUDIOENGINE 列挙オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOENGINE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a893fe02c06fdb02d1c54f6d7487724def732f9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581754"
---
# <a name="kspropertyaudioengine-enumeration"></a>KSPROPERTY\_AUDIOENGINE 列挙型


含まれるプロパティ、 [KSPROPSETID\_AudioEngine](kspropsetid-audioengine.md)プロパティ セットは、この列挙体によって定義されでサポートする必要を[ **KSNODETYPE\_オーディオ\_エンジン**](ksnodetype-audio-engine.md)ノード。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef enum  { 
  KSPROPERTY_AUDIOENGINE_LFXENABLE               = 0,
  KSPROPERTY_AUDIOENGINE_GFXENABLE               = 1,
  KSPROPERTY_AUDIOENGINE_MIXFORMAT               = 2,
  KSPROPERTY_AUDIOENGINE_DEVICEFORMAT            = 4,
  KSPROPERTY_AUDIOENGINE_SUPPORTEDDEVICEFORMATS  = 5,
  KSPROPERTY_AUDIOENGINE_DESCRIPTOR              = 6,
  KSPROPERTY_AUDIOENGINE_BUFFER_SIZE_RANGE       = 7,
  KSPROPERTY_AUDIOENGINE_LOOPBACK_PROTECTION     = 8,
  KSPROPERTY_AUDIOENGINE_VOLUMELEVEL             = 9
} KSPROPERTY_AUDIOENGINE;
```

<a name="constants"></a>定数
---------

<span id="KSPROPERTY_AUDIOENGINE_LFXENABLE"></span><span id="ksproperty_audioengine_lfxenable"></span>**KSPROPERTY\_AUDIOENGINE\_LFXENABLE**  
ID を指定します、 [ **KSPROPERTY\_AUDIOENGINE\_LFXENABLE** ](ksproperty-audioengine-lfx-enable.md)プロパティ。

<span id="KSPROPERTY_AUDIOENGINE_GFXENABLE"></span><span id="ksproperty_audioengine_gfxenable"></span>**KSPROPERTY\_AUDIOENGINE\_GFXENABLE**  
ID を指定します、 [ **KSPROPERTY\_AUDIOENGINE\_GFXENABLE** ](ksproperty-audioengine-gfx-enable.md)プロパティ。

<span id="KSPROPERTY_AUDIOENGINE_MIXFORMAT"></span><span id="ksproperty_audioengine_mixformat"></span>**KSPROPERTY\_AUDIOENGINE\_MIXFORMAT**  
ID を指定します、 [ **KSPROPERTY\_AUDIOENGINE\_MIXFORMAT** ](ksproperty-audioengine-mixformat.md)プロパティ。

<span id="KSPROPERTY_AUDIOENGINE_DEVICEFORMAT"></span><span id="ksproperty_audioengine_deviceformat"></span>**KSPROPERTY\_AUDIOENGINE\_DEVICEFORMAT**  
ID を指定します、 [ **KSPROPERTY\_AUDIOENGINE\_DEVICEFORMAT** ](ksproperty-audioengine-deviceformat.md)プロパティ。

<span id="KSPROPERTY_AUDIOENGINE_SUPPORTEDDEVICEFORMATS"></span><span id="ksproperty_audioengine_supporteddeviceformats"></span>**KSPROPERTY\_AUDIOENGINE\_SUPPORTEDDEVICEFORMATS**  
ID を指定します、 [ **KSPROPERTY\_AUDIOENGINE\_SUPPORTEDDEVICEFORMATS** ](ksproperty-audioengine-supporteddeviceformats.md)プロパティ。

<span id="KSPROPERTY_AUDIOENGINE_DESCRIPTOR"></span><span id="ksproperty_audioengine_descriptor"></span>**KSPROPERTY\_AUDIOENGINE\_記述子**  
ID を指定します、 [ **KSPROPERTY\_AUDIOENGINE\_記述子**](ksproperty-audioengine-descriptor.md)プロパティ。

<span id="KSPROPERTY_AUDIOENGINE_BUFFER_SIZE_RANGE"></span><span id="ksproperty_audioengine_buffer_size_range"></span>**KSPROPERTY\_AUDIOENGINE\_バッファー\_サイズ\_範囲**  
ID を指定します、 [ **KSPROPERTY\_AUDIOENGINE\_バッファー\_サイズ\_範囲**](ksproperty-audioengine-buffer-size-limits.md)プロパティ。

<span id="KSPROPERTY_AUDIOENGINE_LOOPBACK_PROTECTION"></span><span id="ksproperty_audioengine_loopback_protection"></span>**KSPROPERTY\_AUDIOENGINE\_LOOPBACK\_PROTECTION**  
ID を指定します、 [ **KSPROPERTY\_AUDIOENGINE\_ループバック\_保護**](ksproperty-audioengine-loopback-protection.md)プロパティ。

<span id="KSPROPERTY_AUDIOENGINE_VOLUMELEVEL"></span><span id="ksproperty_audioengine_volumelevel"></span>**KSPROPERTY\_AUDIOENGINE\_VOLUMELEVEL**  
ID を指定します、 [ **KSPROPERTY\_AUDIOENGINE\_VOLUMELEVEL** ](ksproperty-audioengine-volumelevel.md)プロパティ。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>サポートされている最小のクライアント</p></td>
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている最小のサーバー</p></td>
<td align="left"><p>Windows Server 2012</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSNODETYPE\_AUDIO\_ENGINE**](ksnodetype-audio-engine.md)

[KSPROPSETID\_AudioEngine](kspropsetid-audioengine.md)

 

 






