---
title: ポート状態のクエリ
description: ポート状態のクエリ
ms.assetid: 3659d99b-1bbd-453c-8a56-b968d1748c1f
keywords:
- ポートの状態が WDK NDIS
- NDIS ポートの状態のクエリを実行します。
- WDK の NDIS OID 要求をポートします。
- NDIS ポート WDK、OID 要求
- OID 要求 WDK NDIS ポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c52ab66d44bf1fbc231531525f8cca387fb2b1de
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571426"
---
# <a name="querying-the-port-state"></a>ポート状態のクエリ





ドライバーのスライドを発行できます、 [OID\_GEN\_ポート\_状態](https://msdn.microsoft.com/library/windows/hardware/ff569624)OID のクエリ要求で指定されているポートの現在の状態を取得する、 **PortNumber**メンバー[ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体。 NDIS が、この OID を処理し、ミニポート ドライバーには、この OID クエリは受け取りません。 NDIS 受信ポートの状態情報で、 [ **NDIS\_ポート\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff566791)構造体。

OID\_GEN\_ポート\_状態 OID が NDIS 6.0 以降でサポートされています。

OID を使用しないようにドライバーを重なって\_GEN\_ポート\_可能な場合の状態にあり、代わりに依存する必要があります、 [ **NDIS\_状態\_ポート\_状態** ](https://msdn.microsoft.com/library/windows/hardware/ff567415)状態を示す値。 ポートに関連する状態インジケーターの詳細については、次を参照してください。 [NDIS ポートの状態インジケーターの処理](handling-ndis-ports-status-indications.md)します。

場合、OID\_GEN\_ポート\_状態クエリが成功すると、NDIS には、ポートの状態情報が返されます、 [ **NDIS\_ポート\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff566800)構造体。

 

 





