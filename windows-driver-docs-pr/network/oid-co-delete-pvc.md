---
title: OID_CO_DELETE_PVC
description: このトピックでは、OID_CO_DELETE_PVC オブジェクト識別子 (OID) について説明します。
ms.assetid: 02da08d0-9d08-4a91-b851-50e3c3b065d6
keywords:
- OID_CO_DELETE_PVC
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a97b7e8faa3781c48b36281b8bfe7e327fdd13e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384385"
---
# <a name="oidcodeletepvc"></a>OID_CO_DELETE_PVC

OID_CO_DELETE_PVC OID は、構成されている Pvc のコール マネージャーの一覧から永続的な接続 (PVC) を削除する、クライアントが、コール マネージャーに送信されます。 PVC 形式は次のように定義されている CO_PVC 構造体としてです。

```c++
typedef struct _CO_PVC {
    NDIS_HANDLE             NdisAfHandle;
    CO_SPECIFIC_PARAMETERS  PvcParameters;
} CO_PVC, *PCO_PVC;
``` 

この構造体のメンバーには、次の情報が含まれます。

**NdisAfHandle**  
によって返される NDIS が指定したハンドルを指定します[NdisClOpenAddressFamilyEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclopenaddressfamilyex)します。

**PvcParameters**  
書式設定された[CO_SPECIFIC_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclopenaddressfamilyex)構造体。 この構造体には、PVC を記述するプロトコル固有のパラメーターが含まれています。

PVC は、管理者によって手動で削除されます。 このようなアクティビティを監視するクライアントでは、この OID をコール マネージャーに送信することによって削除された PVC のコール マネージャーに通知します。

## <a name="requirements"></a>必要条件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

