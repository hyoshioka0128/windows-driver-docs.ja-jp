---
title: OID_CO_ADD_PVC
description: このトピックでは、OID_CO_ADD_PVC オブジェクト識別子 (OID) について説明します。
ms.assetid: 182d5bdb-9cfe-4e9c-a2cf-4d5440bfdb76
keywords:
- OID_CO_ADD_PVC
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a2fe14f72eda2e3da9533e3af7a07068e135bfe
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916926"
---
# <a name="oid_co_add_pvc"></a>OID_CO_ADD_PVC

OID_CO_ADD_PVC OID は、クライアントから呼び出しマネージャーに送信され、永続的な仮想接続 (PVC) が、構成された Pvc の呼び出しマネージャーの一覧に追加されます。 PVC は、次のように定義された CO_PVC 構造として書式設定されます。

```c++
typedef struct _CO_PVC {
    NDIS_HANDLE             NdisAfHandle;
    CO_SPECIFIC_PARAMETERS  PvcParameters;
} CO_PVC, *PCO_PVC;
```

この構造体のメンバーには、次の情報が含まれています。

**NdisAfHandle**  
[NdisClOpenAddressFamilyEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclopenaddressfamilyex)によって返される NDIS 提供のハンドルを指定します。

**PvcParameters**  
書式設定された[CO_SPECIFIC_PARAMETERS](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545396(v=vs.85))構造体。 この構造体には、PVC を説明するプロトコル固有のパラメーターが含まれています。

PVC は、管理者によって手動で構成されます。 このようなアクティビティを監視するクライアントは、この OID を呼び出しマネージャーに送信することで、新しく構成された PVC の呼び出しマネージャーに通知します。 その他のクライアントは、新しく構成された PVC を使用できます。

## <a name="requirements"></a>要件

**バージョン**: Windows Vista 以降の**ヘッダー**: Ntddndis (Ndis .h を含む)

