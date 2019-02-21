---
title: OID_CO_ADD_PVC
description: このトピックでは、OID_CO_ADD_PVC オブジェクト識別子 (OID) について説明します。
ms.assetid: 182d5bdb-9cfe-4e9c-a2cf-4d5440bfdb76
keywords:
- OID_CO_ADD_PVC
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 149fe8425be3eef925c9d6b4e75e1eb0d1b23f05
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551107"
---
# <a name="oidcoaddpvc"></a>OID_CO_ADD_PVC

OID_CO_ADD_PVC OID は、構成されている Pvc のコール マネージャーのリストに永続的な接続 (PVC) を追加する、クライアントが、コール マネージャーに送信されます。 PVC 形式は次のように定義されている CO_PVC 構造体としてです。

```c++
typedef struct _CO_PVC {
    NDIS_HANDLE             NdisAfHandle;
    CO_SPECIFIC_PARAMETERS  PvcParameters;
} CO_PVC, *PCO_PVC;
```

この構造体のメンバーには、次の情報が含まれます。

**NdisAfHandle**  
によって返される NDIS が指定したハンドルを指定します[NdisClOpenAddressFamilyEx](https://msdn.microsoft.com/library/windows/hardware/ff561639)します。

**PvcParameters**  
書式設定された[CO_SPECIFIC_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff545396)構造体。 この構造体には、PVC を記述するプロトコル固有のパラメーターが含まれています。

PVC は、管理者によって手動で構成されます。 このようなアクティビティを監視するクライアントでは、この OID をコール マネージャーに送信することによって、新しく構成した PVC のコール マネージャーに通知します。 その他のクライアントは、新しく構成された PVC を使用できます。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

