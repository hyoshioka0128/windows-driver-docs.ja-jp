---
title: OID_GEN_CO_SUPPORTED_GUIDS
description: このトピックでは、OID_GEN_CO_SUPPORTED_GUIDS オブジェクト識別子 (OID) について説明します。
ms.assetid: d82d6ecb-f70b-4fc2-97eb-331aafe1fe57
keywords:
- OID_GEN_CO_SUPPORTED_GUIDS
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: bea1973c4261a10a61ceb2c16bd489bd1c894c08
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386219"
---
# <a name="oidgencosupportedguids"></a>OID_GEN_CO_SUPPORTED_GUIDS

OID_GEN_CO_SUPPORTED_GUIDS OID NDIS_GUID 型の構造体の配列を返すミニポート ドライバーを要求します。 配列内の各構造は、カスタム GUID (グローバル一意識別子) にカスタム OID がいずれかまたはミニポート ドライバー経由で送信される、NDIS_STATUS のマッピングを指定します[NdisMCoIndicateStatusEx](https://msdn.microsoft.com/library/windows/hardware/ff563562)します。

NDIS_GUID 構造体の定義は次のとおりです。

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

この構造体のメンバーには、次の情報が含まれます。

**guid**  
ミニポート ドライバーに定義されているカスタムの GUID。

**Oid**  
カスタム OID **Guid**マップされます。

**ステータス**  
NDIS_STATUS **Guid**マップされます。

**サイズ**  
FNDIS_GUID_ARRAY フラグが設定されている場合**サイズ**ミニポート ドライバーによって返される配列内の各データ項目のバイト単位のサイズを指定します。 FNDIS_GUID_ANSI_STRING または fNDIS_GUID_NDIS_STRING フラグが設定されている場合**サイズ**が-1 に設定します。 それ以外の場合、**サイズ**GUID を表すデータ項目のバイト単位のサイズを指定します。

**フラグ**  
次のフラグは、OID または NDIS_STATUS 文字列 GUID にマップするかどうかを指定して、GUID を指定したデータの種類を示す論理和を指定できます。 

fNDIS_GUID_TO_OID  
設定すると、NDIS_GUID 構造体は、GUID を OID に対応していることを示します。

fNDIS_GUID_TO_STATUS  
設定すると、NDIS_GUID 構造体は、GUID を NDIS_STATUS 文字列に対応していることを示します。

fNDIS_GUID_ANSI_STRING  
設定すると、GUID の null で終わる ANSI 文字列を提供することを示します。

fNDIS_GUID_UNICODE_STRING  
設定すると、GUID の Unicode 文字列を提供することを示します。

fNDIS_GUID_ARRAY  
設定すると、GUID のデータ項目の配列を提供することを示します。 指定したサイズでは、配列内の各データ項目の長さを示します。

fNDIS_GUID_ALLOW_READ  
設定すると、すべてのユーザーがこの GUID を照会できることを示します。

fNDIS_GUID_ALLOW_WRITE  
設定すると、すべてのユーザーがこの GUID を設定できることを示します。

## <a name="remarks"></a>注釈

> [!NOTE]
> 既定では、ミニポート ドライバーによって提供されるカスタムの WMI Guid では管理者特権を持つユーザーがアクセスできるのみです。 管理者特権を持つユーザーできます常に読み取りまたはミニポート ドライバーが、読み取りをサポートしている場合、カスタム GUID への書き込みまたは書き込み操作の GUID。 すべてのユーザーにカスタムの GUID へのアクセスを許可する fNDIS_GUID_ALLOW_READ と fNDIS_GUID_ALLOW_WRITE フラグを設定します。

ミニポート ドライバーですべてのカスタム Guid が登録されているので注意が fNDIS_GUID_TO_OID または fNDIS_GUID_TO_STATUS のいずれかに設定する必要があります (決して両方設定)。 その他のすべてのフラグは、該当する場合、OR 演算子を使用して組み合わせることができます。

次の例では、NDIS_GUID 構造体は、GUID を OID_GEN_CO_RCV_PDUS_NO_BUFFER にマッピングされます。

```cpp 
NDIS_GUID NdisGuid =  {{0x0a214809, 0xe35f, 0x11d0, 0x96, 0x92, 0x00,
 0xc0, 0x4f, 0xc3, 0x35, 0x8c},
 GUID_NDIS_GEN_CO_RCV_PDUS_NO_BUFFER,
 OID_GEN_CO_RCV_PDUS_NO_BUFFER,
 4,
 fNDIS_GUID_TO_OID};
```
GUID は、Windows Management Instrumentation (WMI) で入手するか、情報を設定するために使用する識別子です。 NDIS は、WMI によって、NDIS ドライバーに送信された GUID は、インターセプト、oid に GUID をマップし、OID をドライバーに送信します。 ドライバーは、NDIS で、WMI にデータを取得するデータ項目を返します。

NDIS は、NIC の状態の変化を WMI で認識される Guid も変換します。 ミニポート ドライバーでの NIC の状態の変更を報告するときに[NdisMCoIndicateStatusEx](https://msdn.microsoft.com/library/windows/hardware/ff563562)、NDIS ミニポート ドライバーで NDIS が WMI に送信する GUID に示される NDIS_STATUS を変換します。

接続指向のミニポート ドライバーでは、関税 Guid をサポートする場合、カスタム Guid カスタム Oid または NDIS_STATUS 文字列へのマッピングを NDIS へ返す OID_GEN_CO_SUPPORTED_GUIDS をサポートしてする必要があります。 OID_GEN_CO_SUPPORTED_GUIDS ミニポート ドライバーのクエリを実行するには後、は、NDIS は、ミニポート ドライバーのカスタム Guid を WMI に登録します。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

