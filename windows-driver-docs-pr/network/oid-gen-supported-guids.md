---
title: OID_GEN_SUPPORTED_GUIDS
description: クエリとして、OID_GEN_SUPPORTED_GUIDS OID は、NDIS_GUID 型の構造体の配列を返すようにミニポートドライバーに要求します。
ms.assetid: 6985727e-50f8-4dbf-b8cd-ce31d49e8294
ms.date: 08/08/2017
keywords: -Windows Vista 以降の OID_GEN_SUPPORTED_GUIDS ネットワークドライバー
ms.localizationpriority: medium
ms.openlocfilehash: d3c119c128f511a4c749aa374a9ef6d85279006d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844601"
---
# <a name="oid_gen_supported_guids"></a>OID\_GEN\_サポートされる\_GUID


クエリとして、OID\_GEN\_サポートされている\_GUID OID は、ミニポートドライバーに対して、型 NDIS\_GUID の構造体の配列を返すように要求します。

**バージョン情報**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 以降のバージョンの Windows  
サポートされています。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 以降のミニポートドライバー  
(省略可能)。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 ミニポートドライバー  
(省略可能)。

<a href="" id="windows-xp"></a>Windows XP  
サポートされています。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 ミニポートドライバー  
(省略可能)。

<a name="remarks"></a>注釈
-------

配列内の各構造体はカスタムの GUID (グローバル一意識別子) からカスタム OID へのマッピング、またはミニポートドライバーが[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)関数を介して送信する NDIS\_ステータスへのマッピングを指定します。

NDIS\_GUID 構造体は、次のように定義されています。

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

この構造体のメンバーには、次の情報が含まれています。

<a href="" id="guid"></a>**Guid**  
ミニポートドライバーに対して定義されているカスタム GUID を指定します。

<a href="" id="oid"></a>**ドーナツ**  
**Guid**がマップされるカスタム OID を指定します。

<a href="" id="status"></a>**オンライン**  
**Guid**がマップされる NDIS\_の状態を指定します。

<a href="" id="size"></a>**幅**  
ミニポートドライバーによって返される配列内の各データ項目のサイズ (バイト単位) を指定します。 FNDIS\_GUID\_ANSI\_STRING または fNDIS\_GUID\_NDIS\_STRING フラグが設定されている場合、 **Size**は-1 に設定されます。 それ以外の場合、 **size**は GUID が表すデータ項目のサイズをバイト単位で指定します。 このメンバーは、fNDIS\_GUID\_配列フラグが設定されている場合にのみ指定されます。

<a href="" id="flags"></a>**示す**  
次のフラグを OR 演算子で結合すると、GUID が OID または NDIS\_のステータス文字列にマップされているかどうか、および GUID に対して指定されているデータの型を示すかどうかを示すことができます。

<a href="" id="fndis-guid-to-oid"></a>fNDIS\_GUID\_\_OID  
NDIS\_GUID 構造体が、GUID を OID にマップすることを示します。

<a href="" id="fndis-guid-to-status"></a>fNDIS\_GUID\_\_の状態  
NDIS\_GUID 構造体が、GUID を NDIS\_ステータス文字列にマップすることを示します。

<a href="" id="fndis-guid-ansi-string"></a>fNDIS\_GUID\_ANSI\_文字列  
Null で終わる ANSI 文字列が GUID に指定されていることを示します。

<a href="" id="fndis-guid-unicode-string"></a>fNDIS\_GUID\_UNICODE\_文字列  
GUID に Unicode 文字列が指定されていることを示します。

<a href="" id="fndis-guid-array"></a>fNDIS\_GUID\_配列  
GUID にデータ項目の配列が指定されていることを示します。 指定された**サイズ**は、配列内の各データ項目の長さを示します。

<a href="" id="fndis-guid-allow-read"></a>fNDIS\_GUID\_\_読み取ることができます  
設定すると、すべてのユーザーがこの GUID を使用して情報を取得できることを示します。

<a href="" id="fndis-guid-allow-write"></a>fNDIS\_GUID\_\_書き込みを許可します  
設定すると、すべてのユーザーがこの GUID を使用して情報を設定できることを示します。

**注**   既定では、ミニポートドライバーによって提供されるカスタム WMI guid には、管理者特権を持つユーザーのみがアクセスできます。 ミニポートドライバーがその GUID の読み取りまたは書き込み操作をサポートしている場合、管理者特権を持つユーザーは、常にカスタム GUID に対して読み取りまたは書き込みを行うことができます。 FNDIS\_GUID を設定し\_\_READ および fNDIS\_GUID\_許可し、すべてのユーザーがカスタム GUID にアクセスできるように\_書き込みフラグを許可します。

 

ミニポートドライバーによって登録されるすべてのカスタム Guid では、fNDIS\_GUID\_を\_OID または fNDIS\_GUID\_に設定して\_状態にする必要があることに注意してください (両方を設定しないでください)。 他のすべてのフラグは、必要に応じて OR 演算子を使用して組み合わせることができます。

次の例では、NDIS\_GUID 構造体は、GUID を OID\_802\_3\_マルチキャスト\_リストにマップします。

```C++
NDIS_GUID    NdisGuid = {{0x44795701, 0xa61b, 0x11d0, 0x8d, 0xd4,
                          0x00, 0xc0, 0x4f, 0xc3,
                          0x35, 0x8c},
                          OID_802_3_MULTICAST_LIST,
                          6,
                          fNDIS_GUID_TO_OID | fNDIS_GUID_ARRAY};
```

GUID は、情報を取得または設定するために Windows Management Instrumentation (WMI) によって使用される識別子です。 NDIS は、WMI によって NDIS ドライバーに送信された GUID をインターセプトし、その GUID を OID にマップして、OID をドライバーに送信します。 ドライバーは、データ項目を NDIS に返します。これにより、データが WMI に返されます。

また、NDIS は、NIC の状態の変更を WMI によって認識される Guid に変換します。 [**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)機能を使用して、ミニポートドライバーが NIC の状態の変更を報告すると、ndis は、ミニポートドライバーによって示される ndis\_の状態を、NDIS が WMI に送信する GUID に変換します。

ミニポートドライバーが税関 Guid をサポートする場合、サポートされている\_GUID\_OID\_GEN をサポートする必要があります。 この OID により、カスタム Guid をカスタム Oid または NDIS\_ステータス文字列にマッピングするための NDIS に戻ります。 OID\_GEN\_サポートされている\_GUID を使用してミニポートドライバーを照会した後、NDIS はミニポートドライバーのカスタム Guid を WMI に登録します。

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
<td>Ntddndis (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)

 

 




