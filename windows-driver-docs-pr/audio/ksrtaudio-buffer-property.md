---
title: KSRTAUDIO\_バッファー\_プロパティ構造
description: KSRTAUDIO\_BUFFER\_プロパティ構造体は、バッファーのベースアドレスと要求されたバッファーサイズを KSK プロパティ構造に追加します。 この構造体は、KSK プロパティ\_RTAUDIO\_BUFFER を介してオーディオバッファーの割り当てを要求するために、クライアントによって使用されます。
ms.assetid: 6fc33d5d-5d7e-4d04-a9b0-864cba961077
keywords:
- KSRTAUDIO_BUFFER_PROPERTY structure のオーディオデバイス
- PKSRTAUDIO_BUFFER_PROPERTY 構造体ポインターオーディオデバイス
topic_type:
- apiref
api_name:
- KSRTAUDIO_BUFFER_PROPERTY
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bcb79849c699e0f29b3f4a3eedede5b1312982f3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832665"
---
# <a name="ksrtaudio_buffer_property-structure"></a>KSRTAUDIO\_バッファー\_プロパティ構造


KSRTAUDIO\_BUFFER\_プロパティ構造体は、バッファーのベースアドレスと要求されたバッファーサイズを[**Ksk プロパティ**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))構造に追加します。 この構造体は、 [**Ksk プロパティ\_rtaudio\_buffer**](ksproperty-rtaudio-buffer.md)を介してオーディオバッファーの割り当てを要求するために、クライアントによって使用されます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct {
  KSPROPERTY Property;
  PVOID      BaseAddress;
  ULONG      RequestedBufferSize;
} KSRTAUDIO_BUFFER_PROPERTY, *PKSRTAUDIO_BUFFER_PROPERTY;
```

<a name="members"></a>Members
-------

**"**  
RTAUDIO\_BUFFER\_、KSK プロパティを呼び出す前に、クライアントが適切に初期化する KSK プロパティ構造体。

**BaseAddress**  
目的のバッファーのベースアドレスを指定します。 クライアントがベースアドレスを指定していない限り、このパラメーターは**NULL**に設定されます。

**RequestedBufferSize**  
必要なバッファーサイズをバイト単位で指定します。 ドライバーは、返される[**Ksrtaudio\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_buffer)構造に割り当てられたバッファーの実際のサイズを返します。

<a name="remarks"></a>注釈
-------

RTAUDIO\_バッファー要求\_は、KSRTAUDIO\_BUFFER\_プロパティ構造を使用して、クライアントが要求する循環バッファーを記述します。 ドライバーは KSRTAUDIO\_バッファー構造を返し、実際に割り当てられたバッファーを記述します。

クライアントが**Requestedbuffersize**メンバーに書き込む値は、ドライバーでバインドされていません。 ただし、ドライバーでは、ドライバー自体のバッファーサイズの制約を考慮して、要求されたサイズにできるだけ近いバッファーサイズを指定する必要があります。 ハードウェアが要求されたサイズを処理できない場合や、システムのメモリが不足している場合、ドライバーは異なるサイズのバッファーを割り当てます。 たとえば、ドライバーは、メモリページよりも小さいバッファーを割り当てます。または、バッファーサイズを次のサンプルブロック全体に丸めます。 また、システムでメモリが不足している場合、ドライバーは要求されたサイズより小さいバッファーを割り当てます。

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
<td align="left"><p>Windows Vista 以降の Windows オペレーティングシステムで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

 

 





