---
title: KSJACK\_DESCRIPTION2 構造体
description: KSJACK\_DESCRIPTION2 構造は、機能とサポートがプレゼンスの検出を jack jack の現在の状態を指定します。
ms.assetid: 0db29870-20d0-459b-a531-3dea5d073183
keywords:
- KSJACK_DESCRIPTION2 構造オーディオ デバイス
- PKSJACK_DESCRIPTION2 構造体ポインター オーディオ デバイス
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
ms.openlocfilehash: 283100a9053b80de46afa42697bf8fe84f947d9e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574782"
---
# <a name="ksjackdescription2-structure"></a>KSJACK\_DESCRIPTION2 構造体


`KSJACK_DESCRIPTION2`構造体は、機能とサポートがプレゼンスの検出を jack jack の現在の状態を指定します。

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
下位 16 ビットの DWORD パラメーターを指定します。 このパラメーターは、ジャックは、現在アクティブなストリーミング、アイドル状態かどうか、またはハードウェアの準備ができていませんを示します。

**JackCapabilities**  
下位 16 ビットの DWORD パラメーターを指定します。 このパラメーターは、フラグとジャックの機能を示します。 このフラグは、次の表に、値のいずれかに設定できます。

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
<td align="left"><p>回線のモジュラー ジャック サポート ジャック プレゼンスの検出。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>JACKDESC2_DYNAMIC_FORMAT_CHANGE_CAPABILITY (0x00000002)</p></td>
<td align="left"><p>回線のモジュラー ジャックには、動的形式の変更がサポートされています。</p></td>
</tr>
</tbody>
</table>

 

動的な形式の変更の詳細については、次を参照してください。[動的形式変更](https://msdn.microsoft.com/library/windows/hardware/ff536371)します。

<a name="remarks"></a>コメント
-------

オーディオ デバイスがありませんジャック プレゼンスの検出場合、 **IsConnected**のメンバー、 [ **KSJACK\_説明**](ksjack-description.md)構造体は、に常に設定する必要があります**TRUE**します。 この 2 つの意味に起因するあいまいさを削除する、 **TRUE**値**IsConnected**、クライアント アプリケーションが呼び出す[IKsJackDescription2::GetJackDescription2](https://go.microsoft.com/fwlink/p/?linkid=143698)を読み取る、 **JackCapabilities**のフラグ、`KSJACK_DESCRIPTION2`構造体。 このフラグは、JACKDESC2 場合\_プレゼンス\_検出\_機能ビットが設定、エンドポイントは実際にはジャック プレゼンスの検出にサポートを示します。 その場合、戻り値の**IsConnected**メンバーは、ジャックのカーソルの状態を正確に反映するように解釈できます。

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
<td align="left"><p>Windows 7 およびそれ以降の Windows オペレーティング システムで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSJACK\_の説明**](ksjack-description.md)

[IKsJackDescription2::GetJackDescription2](https://go.microsoft.com/fwlink/p/?linkid=143698)

 

 






