---
title: OID_CO_TAPI_LINE_CAPS
description: このトピックでは、OID_CO_TAPI_LINE_CAPS オブジェクト識別子 (OID) について説明します。
ms.assetid: 82c2bcb4-fb58-4e14-b1d4-2bcc0c4fcd1d
keywords:
- OID_CO_TAPI_LINE_CAPS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01cea4126ec7f85cd84e6ac215af06a0f28dae9e
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917524"
---
# <a name="oid_co_tapi_line_caps"></a>OID_CO_TAPI_LINE_CAPS

OID_CO_TAPI_LINE_CAPS OID は、指定された回線のテレフォニー機能を返すために、呼び出しマネージャーまたは統合ミニポート呼び出しマネージャー (MCM) ドライバーを要求します。 また、この OID は、この行のアドレスが異なるテレフォニー機能を持つかどうかを示すために、呼び出しマネージャーまたは MCM ドライバーに要求します。

この要求では、次のように定義された CO_TAPI_LINE_CAPS 構造を使用して、指定された行のテレフォニー機能を照会します。

```c++
typedef struct _CO_TAPI_LINE_CAPS {
    IN  ULONG           ulLineID;
    OUT ULONG           ulFlags;
    OUT LINE_DEV_CAPS   LineDevCaps;
} CO_TAPI_LINE_CAPS, *PCO_TAPI_LINE_CAPS;
``` 

この構造体のメンバーには、次の情報が含まれています。

**ulLineID**  
テレフォニー機能を返す回線を指定します。 **ulLineID**は、0から始まる識別子です。

**ulFlags**  
回線が異なるテレフォニー機能を持つ複数のアドレスをサポートしている場合、呼び出しマネージャーまたは MCM ドライバーは、ulFlags に CO_TAPI_FLAG_PER_ADDRESS_CAPS ビットを設定します。それ以外の場合、呼び出しマネージャーまたは MCM ドライバーはこのビットをクリアします。 未定義のビットはすべて予約されており、0に設定する必要があります。

**LineDevCaps**  
LINE_DEV_CAPS 構造体として書式設定された、線のテレフォニー機能を指定します。 この構造体の詳細については、Microsoft Windows SDK と ndistapi .h のヘッダーファイルを参照してください。

## <a name="remarks"></a>注釈

[OID_CO_TAPI_CM_CAPS](oid-co-tapi-cm-caps.md)を使用して通話マネージャーまたは mcm ドライバーのデバイスのテレフォニー機能に対してクエリを実行すると、接続指向クライアントは、デバイスでサポートされている回線のテレフォニー機能に対してクエリを実行します。

- デバイスでサポートされているすべての行の回線機能が同じで、これらの行のすべてのアドレスが同じアドレス機能を持っている場合、クライアントは一度 OID_CO_TAPI_LINE_CAPS クエリを実行し、デバイスの回線機能を取得します。 この場合、呼び出しマネージャーまたは MCM ドライバーによって返される行機能は、デバイスでサポートされているすべての行に適用されます。
- ただし、デバイスが異なる機能を持つ複数の行をサポートしている場合、または、これらの行のアドレスが異なるアドレス機能を持つ場合、クライアントは、デバイスでサポートされている行ごとに1回 OID_CO_TAPI_LINE_CAPS を照会し、各行の機能を取得します。

**Ulflags**設定は、クライアントが行のアドレスの機能に対してクエリを実行する回数を決定します。

- 回線でサポートされているアドレスが1つだけの場合、または同じアドレス機能を持つ複数のアドレスが回線でサポートされている場合、クライアントは一度 OID_CO_TAPI_ADDRESS_CAPS クエリを実行します。
- 機能が異なる複数のアドレスが回線でサポートされている場合、クライアントは、行の各アドレスに対して1回 OID_CO_TAPI_ADDRESS_CAPS を照会する必要があります。

## <a name="requirements"></a>要件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)

