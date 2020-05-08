---
title: KSJACK\_DESCRIPTION2 構造体
description: KSJACK\_DESCRIPTION2 構造体は、ジャックのプレゼンス検出をサポートするジャックの機能と現在の状態を指定します。
ms.assetid: 0db29870-20d0-459b-a531-3dea5d073183
keywords:
- KSJACK_DESCRIPTION2 構造のオーディオデバイス
- PKSJACK_DESCRIPTION2 構造体ポインターオーディオデバイス
topic_type:
- apiref
api_name:
- KSJACK_DESCRIPTION2
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0dee72cbc15d6cb28cb384aa644143c283b0c7f2
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925551"
---
# <a name="ksjack_description2-structure"></a>KSJACK\_DESCRIPTION2 構造体


構造`KSJACK_DESCRIPTION2`体は、ジャックのプレゼンス検出をサポートするジャックの機能と現在の状態を指定します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _tagKSJACK_DESCRIPTION2 {
  DWORD DeviceStateInfo;
  DWORD JackCapabilities;
} KSJACK_DESCRIPTION2, *PKSJACK_DESCRIPTION2;
```

<a name="members"></a>メンバー
-------

**DeviceStateInfo**  
DWORD パラメーターの下位16ビットを指定します。 このパラメーターは、ジャックが現在アクティブ、ストリーミング、アイドル、またはハードウェアの準備ができていないかどうかを示します。

**JackCapabilities**  
DWORD パラメーターの下位16ビットを指定します。 このパラメーターはフラグで、ジャックの機能を示します。 このフラグは、次の表のいずれかの値に設定できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>フラグ</strong></p></td>
<td align="left"><p><strong>意味</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>JACKDESC2_PRESENCE_DETECT_CAPABILITY (0x00000001)</p></td>
<td align="left"><p>ジャックは、ジャックのプレゼンス検出をサポートしています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>JACKDESC2_DYNAMIC_FORMAT_CHANGE_CAPABILITY (0x00000002)</p></td>
<td align="left"><p>ジャックは、動的な形式変更をサポートしています。</p></td>
</tr>
</tbody>
</table>

 

動的な形式の変更の詳細については、「[動的形式の変更](https://docs.microsoft.com/windows-hardware/drivers/audio/dynamic-format-change)」を参照してください。

<a name="remarks"></a>解説
-------

オーディオデバイスにジャックの存在が検出されない場合は、 [**Ksk ジャック\_記述**](ksjack-description.md)構造体の**IsConnected**メンバーを常に**TRUE**に設定する必要があります。 **IsConnected**の**真**の値のこの2つの意味によって得られるあいまいさを解消するために、クライアントアプリケーションは[IKsJackDescription2:: GetJackDescription2](https://docs.microsoft.com/windows/win32/api/devicetopology/nf-devicetopology-iksjackdescription2-getjackdescription2)を`KSJACK_DESCRIPTION2`呼び出して構造体の**JackCapabilities**フラグを読み取ることができます。 このフラグに JACKDESC2\_プレゼンス\_検出\_機能ビットが設定されている場合は、エンドポイントが、実際にはジャックのプレゼンス検出をサポートしていることを示します。 その場合は、 **IsConnected**メンバーの戻り値を、ジャックの挿入状態を正確に反映するように解釈できます。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 7 以降の Windows オペレーティングシステムで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ヘッダー</p></td>
<td align="left">Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSK ジャック\_の説明**](ksjack-description.md)

[IKsJackDescription2::GetJackDescription2](https://docs.microsoft.com/windows/win32/api/devicetopology/nf-devicetopology-iksjackdescription2-getjackdescription2)

 

 






