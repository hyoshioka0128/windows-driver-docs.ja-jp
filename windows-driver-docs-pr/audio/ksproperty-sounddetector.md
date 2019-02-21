---
title: KSPROPERTY\_SOUNDDETECTOR 列挙型
description: KSPROPERTY\_SOUNDDETECTOR 列挙体は、登録、検出機能をサポートするオーディオ キャプチャ デバイス用のフィルターに使用される定数を定義します。
ms.assetid: 6AF98B06-1531-4AC9-9E32-D812E6EA424C
keywords:
- KSPROPERTY_SOUNDDETECTOR 列挙オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_SOUNDDETECTOR
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad03404cf7e171704d610bfea6de6c8b124f5154
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549701"
---
# <a name="kspropertysounddetector-enumeration"></a>KSPROPERTY\_SOUNDDETECTOR 列挙型


**KSPROPERTY\_SOUNDDETECTOR**列挙体は、登録、検出機能をサポートするオーディオ キャプチャ デバイス用のフィルターに使用される定数を定義します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef enum  { 
  KSPROPERTY_SOUNDDETECTOR_SUPPORTEDPATTERNS  = 1,
  KSPROPERTY_SOUNDDETECTOR_PATTERNS,
  KSPROPERTY_SOUNDDETECTOR_ARMED,
  KSPROPERTY_SOUNDDETECTOR_MATCHRESULT
} KSPROPERTY_SOUNDDETECTOR;
```

<a name="constants"></a>定数
---------

<span id="KSPROPERTY_SOUNDDETECTOR_SUPPORTEDPATTERNS"></span><span id="ksproperty_sounddetector_supportedpatterns"></span>**KSPROPERTY\_SOUNDDETECTOR\_SUPPORTEDPATTERNS**  
ID を指定します、 [ **KSPROPERTY\_SOUNDDETECTOR\_SUPPORTEDPATTERNS** ](ksproperty-sounddetector-supportedpatterns.md)プロパティ。

<span id="KSPROPERTY_SOUNDDETECTOR_PATTERNS"></span><span id="ksproperty_sounddetector_patterns"></span>**KSPROPERTY\_SOUNDDETECTOR\_パターン**  
ID を指定します、 [ **KSPROPERTY\_SOUNDDETECTOR\_パターン**](ksproperty-sounddetector-patterns.md)プロパティ。

<span id="KSPROPERTY_SOUNDDETECTOR_ARMED"></span><span id="ksproperty_sounddetector_armed"></span>**KSPROPERTY\_SOUNDDETECTOR\_ARMED**  
ID を指定します、 [ **KSPROPERTY\_SOUNDDETECTOR\_故障**](ksproperty-sounddetector-armed.md)プロパティ。

<span id="KSPROPERTY_SOUNDDETECTOR_MATCHRESULT"></span><span id="ksproperty_sounddetector_matchresult"></span>**KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT**  
ID を指定します、 [ **KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT** ](ksproperty-sounddetector-matchresult.md)プロパティ。

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
<td align="left"><p>Windows 10</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている最小のサーバー</p></td>
<td align="left"><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[KSPROPSETID\_SoundDetector](kspropsetid-sounddetector.md)

[**KSPROPERTY\_SOUNDDETECTOR\_SUPPORTEDPATTERNS**](ksproperty-sounddetector-supportedpatterns.md)

[**KSPROPERTY\_SOUNDDETECTOR\_パターン**](ksproperty-sounddetector-patterns.md)

[**KSPROPERTY\_SOUNDDETECTOR\_故障**](ksproperty-sounddetector-armed.md)

[**KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT**](ksproperty-sounddetector-matchresult.md)

 

 






