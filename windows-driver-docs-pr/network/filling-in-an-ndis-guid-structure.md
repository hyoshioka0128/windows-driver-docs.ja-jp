---
title: NDIS_GUID 構造の入力
description: NDIS_GUID 構造の入力
ms.assetid: 971f6f25-fd2b-4a1e-9378-6270a094f4ff
keywords:
- NDIS_GUID
- WMI の WDK にネットワーク接続、Guid
- Oid WDK ネットワー キング、WMI
- Guid の WDK ネットワーク
- Windows Management Instrumentation の WDK ネットワー キング、Guid
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdfb61c2baae1535debcc5e7095b914fa6157c56
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380152"
---
# <a name="filling-in-an-ndisguid-structure"></a>入力、NDIS\_GUID 構造体





NDIS\_GUID 構造は次のように定義されます。

```C++
typedef struct _NDIS_GUID {
  GUID  Guid;
  union {
    NDIS_OID  Oid;
    NDIS_STATUS  Status;
  };
  ULONG  Size;
  ULONG  Flags;
} NDIS_GUID, *PNDIS_GUID;
```

GUID を取得、 **Guid**構造体のメンバー、Uuidgen.exe アプリケーションを実行することができます。 このアプリケーションに関する詳細については、Microsoft Windows SDK のドキュメントを参照してください。

**Oid**または**状態**メンバーが、OID コードである ULONG。 NDIS 6.0 では、カスタムの状態インジケーターは WMI の Guid にマップしません。

場合、NDIS\_GUID 構造体にマップ データの項目の配列を返す OID、**サイズ**メンバーが、配列内の各データ項目のバイト単位のサイズを指定します。 データが、配列でない場合、**サイズ**メンバーは、データのサイズを指定します。 データ項目のサイズが変数である場合、または OID は、データを返さない場合、**サイズ**メンバーが-1 にする必要があります。

次の値のビットごとの OR、**フラグ**メンバーは、GUID に関連付けられているデータの種類を示します。

<a href="" id="fndis-guid-to-oid"></a>fNDIS\_GUID\_TO\_OID  
このフラグ設定されている場合、NDIS\_GUID 構造体には、OID に GUID がマップされます。

<a href="" id="fndis-guid-to-status"></a>fNDIS\_GUID\_TO\_状態  
NDIS 用に予約されています。 ミニポート ドライバーでは、このフラグを使用する必要があります。

<a href="" id="fndis-guid-ansi-string"></a>fNDIS\_GUID\_ANSI\_文字列  
このフラグが設定されている場合、GUID null で終わる ANSI 文字列が指定されています。

<a href="" id="fndis-guid-unicode-string"></a>fNDIS\_GUID\_UNICODE\_文字列  
このフラグが設定されている場合、GUID Unicode 文字列が指定されています。

<a href="" id="fndis-guid-array"></a>fNDIS\_GUID\_配列  
このフラグが設定されている場合、GUID データ項目の配列が指定されています。 指定した**サイズ**値は、配列内の各データ項目の長さを示します。

<a href="" id="fndis-guid-allow-read"></a>fNDIS\_GUID\_許可\_読み取り  
このフラグが設定されている場合、この GUID を使用して情報を取得するすべてのユーザーが許可されています。

<a href="" id="fndis-guid-allow-write"></a>fNDIS\_GUID\_許可\_書き込み  
このフラグが設定されている場合は、この GUID を使用して情報を設定するすべてのユーザーが許可されています。

**注**  既定では、ミニポート ドライバーを提供するカスタムの WMI Guid は、管理者特権を持つユーザーのみにアクセスします。 管理者特権を持つユーザーできます常に読み取りまたはミニポート ドライバーが、読み取りをサポートしている場合、カスタム GUID への書き込みまたは書き込み操作の GUID。 FNDIS を設定することができます\_GUID\_許可\_読み取りおよび fNDIS\_GUID\_許可\_カスタム GUID にアクセスするすべてのユーザーを許可する書き込みフラグ。

 

ドライバーを登録するすべてのカスタム guid、ドライバー設定あります fNDIS\_GUID\_TO\_OID。 ミニポート ドライバーが fNDIS を設定する必要がありますしない\_GUID\_TO\_状態。 すべての他のフラグは、ビットごとの OR 演算を使用して結合できます。

 

 





