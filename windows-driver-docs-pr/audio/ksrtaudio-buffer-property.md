---
title: KSRTAUDIO\_バッファー\_プロパティ構造体
description: KSRTAUDIO\_バッファー\_プロパティ構造 KSPROPERTY 構造体をバッファーのベース アドレスと要求されたバッファー サイズを追加します。 この構造は KSPROPERTY 経由でオーディオのバッファーの割り当てを要求するクライアントによって使用される\_RTAUDIO\_バッファー。
ms.assetid: 6fc33d5d-5d7e-4d04-a9b0-864cba961077
keywords:
- KSRTAUDIO_BUFFER_PROPERTY 構造オーディオ デバイス
- PKSRTAUDIO_BUFFER_PROPERTY 構造体ポインター オーディオ デバイス
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
ms.openlocfilehash: b26129dcbbdafe2b09690ae682e42975c3954d2f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360474"
---
# <a name="ksrtaudiobufferproperty-structure"></a>KSRTAUDIO\_バッファー\_プロパティ構造体


KSRTAUDIO\_バッファー\_プロパティ構造は、バッファーの基本アドレスを要求したバッファーのサイズを追加します、 [ **KSPROPERTY** ](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))構造体。 この構造を使用してオーディオ バッファーの割り当てを要求するクライアントによって使用される[ **KSPROPERTY\_RTAUDIO\_バッファー**](ksproperty-rtaudio-buffer.md)します。

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

**プロパティ**  
呼び出し元 KSPROPERTY する前に、クライアントが適切を初期化する KSPROPERTY 構造\_RTAUDIO\_バッファー。

**BaseAddress**  
必要なバッファーのベース アドレスを指定します。 このパラメーターに設定されているクライアントは、ベース アドレスを指定しない限り、 **NULL**します。

**RequestedBufferSize**  
(バイト単位) には、必要なバッファー サイズを指定します。 ドライバーが割り当てられるバッファーの実際のサイズを返します、 [ **KSRTAUDIO\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksrtaudio_buffer)から返される構造体。

<a name="remarks"></a>注釈
-------

KSPROPERTY\_RTAUDIO\_バッファー要求は、KSRTAUDIO\_バッファー\_クライアントが要求する循環バッファーを記述するプロパティ構造体。 ドライバーは、KSRTAUDIO を返します\_バッファーの構造体は、実際に割り当てられたバッファーについて説明します。

値はクライアントに書き込む、 **RequestedBufferSize**メンバーは、ドライバーではバインドされません。 ただし、ドライバーは、ドライバー自体にバッファー サイズの制約を考慮して、要求されたサイズにできるだけ近いバッファー サイズを指定する必要があります。 ドライバーは、ハードウェアが、要求されたサイズを処理できないか、システムがメモリ不足を異なるサイズのバッファーを割り当てます。 たとえば、ドライバーでは、メモリ ページよりも小さくバッファーを割り当てます。 または全体のサンプルの次のブロックまでバッファー サイズを丸めます。 また、システムがメモリ不足している場合、ドライバーは、要求されたサイズより小さいバッファーを割り当てます。

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
<td align="left"><p>Windows Vista 以降の Windows オペレーティング システムで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

 

 





