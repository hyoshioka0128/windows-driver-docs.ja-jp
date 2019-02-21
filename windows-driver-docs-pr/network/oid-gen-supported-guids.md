---
title: OID_GEN_SUPPORTED_GUIDS
description: クエリとしては、OID_GEN_SUPPORTED_GUIDS OID は NDIS_GUID 型の構造体の配列を返すミニポート ドライバーを要求します。
ms.assetid: 6985727e-50f8-4dbf-b8cd-ce31d49e8294
ms.date: 08/08/2017
keywords: -OID_GEN_SUPPORTED_GUIDS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 5019d616ab3821d511e391d8d2e5e510d8419084
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537204"
---
# <a name="oidgensupportedguids"></a>OID\_GEN\_サポートされている\_GUID


クエリ、OID として\_GEN\_サポートされている\_GUID OID 要求 NDIS 型の構造体の配列を返すミニポート ドライバー\_GUID。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista および Windows の以降のバージョン  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 とそれ以降のミニポート ドライバー  
(省略可能)。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
(省略可能)。

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-miniport-drivers"></a>5.1 の NDIS ミニポート ドライバー  
(省略可能)。

<a name="remarks"></a>注釈
-------

配列内の各構造は、カスタム GUID (グローバル一意識別子) のいずれかのカスタム OID または、NDIS のマッピングを指定します\_ミニポート ドライバー経由で送信の状態、 [ **NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)関数。

NDIS\_GUID 構造は次のように定義されます。

```C++
typedef struct _NDIS_GUID {
    GUID             Guid;
    union {
        NDIS_OID     Oid;
        NDIS_STATUS  Status;
    };
    ULONG            Size;
    ULONG            Flags;
} NDIS_GUID, *PNDIS_GUID;
```

この構造体のメンバーには、次の情報が含まれます。

<a href="" id="guid"></a>**guid**  
ミニポート ドライバーに定義されているカスタム GUID を指定します。

<a href="" id="oid"></a>**Oid**  
カスタム OID を指定します**Guid**マップされます。

<a href="" id="status"></a>**状態**  
NDIS を指定します\_状態**Guid**マップされます。

<a href="" id="size"></a>**サイズ**  
ミニポート ドライバーによって返される配列内の各データ項目のバイト単位のサイズを指定します。 場合、fNDIS\_GUID\_ANSI\_文字列または fNDIS\_GUID\_NDIS\_文字列フラグを設定すると、**サイズ**が-1 に設定します。 それ以外の場合、**サイズ**GUID を表すデータ項目のバイト単位のサイズを指定します。 このメンバーが指定された場合にのみ、fNDIS\_GUID\_配列フラグを設定します。

<a href="" id="flags"></a>**フラグ**  
次のフラグは、OID または、NDIS GUID をマップするかどうかを示すために OR 演算子で結合できます\_ステータス文字列と GUID が指定されているデータの種類を示します。

<a href="" id="fndis-guid-to-oid"></a>fNDIS\_GUID\_TO\_OID  
示します、NDIS\_GUID 構造体には、OID に GUID がマップされます。

<a href="" id="fndis-guid-to-status"></a>fNDIS\_GUID\_TO\_状態  
示します、NDIS\_GUID 構造体は、NDIS に GUID をマップ\_ステータス文字列。

<a href="" id="fndis-guid-ansi-string"></a>fNDIS\_GUID\_ANSI\_文字列  
GUID の null で終わる ANSI 文字列を提供することを示します。

<a href="" id="fndis-guid-unicode-string"></a>fNDIS\_GUID\_UNICODE\_文字列  
GUID の Unicode 文字列を提供することを示します。

<a href="" id="fndis-guid-array"></a>fNDIS\_GUID\_配列  
GUID のデータ項目の配列を提供することを示します。 指定した**サイズ**配列内の各データ項目の長さを示します。

<a href="" id="fndis-guid-allow-read"></a>fNDIS\_GUID\_許可\_読み取り  
設定すると、すべてのユーザーがこの GUID を使用して情報を取得できることを示します。

<a href="" id="fndis-guid-allow-write"></a>fNDIS\_GUID\_許可\_書き込み  
設定すると、この GUID を使用して情報を設定するすべてのユーザーが許可されていることを示します。

**注**  既定では、ミニポート ドライバーによって提供されるカスタムの WMI Guid は管理者特権を持つユーザーがアクセスできるのみです。 管理者特権を持つユーザーできます常に読み取りまたはミニポート ドライバーが、読み取りをサポートしている場合、カスタム GUID への書き込みまたは書き込み操作の GUID。 設定、fNDIS\_GUID\_許可\_読み取りおよび fNDIS\_GUID\_許可\_カスタム GUID にアクセスするすべてのユーザーを許可するフラグを書き込み。

 

ミニポート ドライバーで登録されているすべてのカスタム Guid 注か fNDIS を設定する必要があります\_GUID\_TO\_OID または fNDIS\_GUID\_TO\_状態 (決して両方設定)。 その他のすべてのフラグは、該当する場合、OR 演算子を使用して組み合わせることができます。

次の例は、NDIS\_GUID 構造体は、OID に GUID をマップ\_802\_3\_マルチキャスト\_一覧。

```C++
NDIS_GUID    NdisGuid = {{0x44795701, 0xa61b, 0x11d0, 0x8d, 0xd4,
                          0x00, 0xc0, 0x4f, 0xc3,
                          0x35, 0x8c},
                          OID_802_3_MULTICAST_LIST,
                          6,
                          fNDIS_GUID_TO_OID | fNDIS_GUID_ARRAY};
```

GUID は、Windows Management Instrumentation (WMI) で入手するか、情報を設定するために使用する識別子です。 NDIS は、NDIS ドライバーに WMI によって送信された GUID をインターセプト、OID、GUID にマップし、OID をドライバーに送信します。 ドライバーは、NDIS で、WMI にデータを取得するデータ項目を返します。

NDIS は、NIC の状態の変化を WMI で認識される Guid も変換します。 ミニポート ドライバーが NIC の状態を使用して変更を報告すると、 [ **NdisMIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563600)関数、NDIS 変換、NDIS\_に GUID を NDIS ミニポート ドライバーによって示される状態WMI を送信します。

OID をサポートする必要があります、ミニポート ドライバーでは、関税 Guid をサポートする場合\_GEN\_サポートされている\_GUID。 この OID の NDIS にカスタム Oid または NDIS するカスタムの Guid のマッピングを返します\_状態を示す文字列。 OID を使用して、ミニポート ドライバーを照会した\_GEN\_サポートされている\_wmi の GUID、NDIS 登録、ミニポート ドライバーのカスタムの Guid。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)

 

 




