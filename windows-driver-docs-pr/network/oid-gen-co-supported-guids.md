---
title: OID_GEN_CO_SUPPORTED_GUIDS
description: このトピックでは、OID_GEN_CO_SUPPORTED_GUIDS オブジェクト識別子 (OID) について説明します。
ms.assetid: d82d6ecb-f70b-4fc2-97eb-331aafe1fe57
keywords:
- OID_GEN_CO_SUPPORTED_GUIDS
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06beebe83ccdb92a24ba5a004cdc90aee170f7ad
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824389"
---
# <a name="oid_gen_co_supported_guids"></a>OID_GEN_CO_SUPPORTED_GUIDS

OID_GEN_CO_SUPPORTED_GUIDS OID は、NDIS_GUID 型の構造体の配列を返すようにミニポートドライバーに要求します。 配列内の各構造体は、カスタム識別子 (グローバル一意識別子) からカスタム OID へのマッピング、またはミニポートドライバーが[NdisMCoIndicateStatusEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)経由で送信する NDIS_STATUS へのマッピングを指定します。

NDIS_GUID 構造体は次のように定義されています。

```c++
typedef struct _NDIS_GUID {
    GUID    Guid;
    union {
        NDIS_OID    Oid;
        NDIS_STATUS Status;
    };
    ULONG   Size;
    ULONG   Flags;
} NDIS_GUID, *PNDIS_GUID;
```

この構造体のメンバーには、次の情報が含まれています。

**Guid**  
ミニポートドライバーに対して定義されているカスタム GUID。

**ドーナツ**  
**Guid**がマップされるカスタム OID。

**状態**  
**Guid**が割り当てられている NDIS_STATUS。

**サイズ**  
FNDIS_GUID_ARRAY フラグが設定されている場合、 **size**はミニポートドライバーによって返される配列内の各データ項目のサイズ (バイト単位) を指定します。 FNDIS_GUID_ANSI_STRING または fNDIS_GUID_NDIS_STRING フラグが設定されている場合、 **Size**は-1 に設定されます。 それ以外の場合、 **size**は GUID が表すデータ項目のサイズをバイト単位で指定します。

**示す**  
次のフラグを連結して、GUID が OID または NDIS_STATUS 文字列にマップされているかどうかを示し、GUID に対して指定されたデータの型を示すことができます。 

fNDIS_GUID_TO_OID  
設定すると、NDIS_GUID 構造体が GUID を OID にマップすることを示します。

fNDIS_GUID_TO_STATUS  
設定すると、NDIS_GUID 構造体が GUID を NDIS_STATUS 文字列にマップすることを示します。

fNDIS_GUID_ANSI_STRING  
設定すると、null で終わる ANSI 文字列が GUID に対して指定されていることを示します。

fNDIS_GUID_UNICODE_STRING  
設定すると、GUID に Unicode 文字列が指定されていることを示します。

fNDIS_GUID_ARRAY  
設定した場合、データ項目の配列が GUID に対して指定されていることを示します。 指定されたサイズは、配列内の各データ項目の長さを示します。

fNDIS_GUID_ALLOW_READ  
設定すると、すべてのユーザーがこの GUID のクエリを実行できることを示します。

fNDIS_GUID_ALLOW_WRITE  
設定すると、すべてのユーザーがこの GUID を設定できることを示します。

## <a name="remarks"></a>注釈

> [!NOTE]
> 既定では、ミニポートドライバーによって提供されるカスタム WMI Guid には、管理者特権を持つユーザーのみがアクセスできます。 ミニポートドライバーがその GUID の読み取りまたは書き込み操作をサポートしている場合、管理者特権を持つユーザーは、常にカスタム GUID に対して読み取りまたは書き込みを行うことができます。 FNDIS_GUID_ALLOW_READ フラグと fNDIS_GUID_ALLOW_WRITE フラグを設定して、すべてのユーザーがカスタム GUID にアクセスできるようにします。

ミニポートドライバーによって登録されるすべてのカスタム Guid は、fNDIS_GUID_TO_OID または fNDIS_GUID_TO_STATUS のいずれかを設定する必要があることに注意してください (両方を設定しないでください)。 他のすべてのフラグは、必要に応じて OR 演算子を使用して組み合わせることができます。

次の例では、NDIS_GUID 構造体によって GUID が OID_GEN_CO_RCV_PDUS_NO_BUFFER にマップされます。

```cpp 
NDIS_GUID NdisGuid =  {{0x0a214809, 0xe35f, 0x11d0, 0x96, 0x92, 0x00,
 0xc0, 0x4f, 0xc3, 0x35, 0x8c},
 GUID_NDIS_GEN_CO_RCV_PDUS_NO_BUFFER,
 OID_GEN_CO_RCV_PDUS_NO_BUFFER,
 4,
 fNDIS_GUID_TO_OID};
```
GUID は、情報を取得または設定するために Windows Management Instrumentation (WMI) によって使用される識別子です。 NDIS は、WMI によって NDIS ドライバーに送信された GUID をインターセプトし、その GUID を OID にマップして、OID をドライバーに送信します。 ドライバーは、データ項目を NDIS に返します。これにより、データが WMI に返されます。

また、NDIS は、NIC の状態の変更を WMI によって認識される Guid に変換します。 ミニポートドライバーが[NdisMCoIndicateStatusEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)を使用して NIC の状態の変更を報告すると、ndis はミニポートドライバーによって示される NDIS_STATUS を、NDIS が WMI に送信する GUID に変換します。

接続指向ミニポートドライバーが税関 Guid をサポートしている場合は、OID_GEN_CO_SUPPORTED_GUIDS をサポートしている必要があります。これは、カスタムの Oid のカスタム Oid または NDIS_STATUS 文字列へのマッピングを NDIS に返します。 OID_GEN_CO_SUPPORTED_GUIDS を使用してミニポートドライバーに対してクエリを実行すると、NDIS によってミニポートドライバーのカスタム Guid が WMI に登録されます。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis (Ndis .h を含む) |

