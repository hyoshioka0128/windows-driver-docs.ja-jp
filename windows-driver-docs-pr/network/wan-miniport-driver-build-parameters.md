---
title: WAN ミニポート ドライバーのビルド パラメーター
description: WAN ミニポート ドライバーのビルド パラメーター
ms.assetid: 8e494bd2-c499-48bf-8574-7e8df05be4c8
keywords:
- WAN ミニポート ドライバー WDK ネットワーク、構成
- いる CoNDIS WAN ドライバー WDK ネットワー キング、ビルド
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1994189dcdeda2bb602c3466418e16fccd510302
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529258"
---
# <a name="wan-miniport-driver-build-parameters"></a>WAN ミニポート ドライバーのビルド パラメーター





このトピックでは、NDIS およびいる CoNDIS WAN ミニポート ドライバーのビルド パラメーターの定義に関する情報を説明します。

ミニポート ドライバーとドライバーを識別するために構築する前に、ソース ファイルに次の行を追加します。

```Text
C_DEFINES=/DNDIS_MINIPORT_DRIVER
```

TAPI 経由の接続をサポートする、NDIS WAN ミニポート ドライバーを作成する場合は、ドライバーがサポートする TAPI バージョンを識別するために構築する前に、次の行をソース ファイルに追加する必要があります。

```Text
C_DEFINES=-DNDIS_TAPI_CURRENT_VERSION=0x00010003
```

いる CoNDIS WAN ミニポート ドライバーを作成する場合は統合ミニポート コール マネージャー (MCM) およびいる CoNDIS CO アドレス ファミリ型をサポートする\_アドレス\_ファミリ\_TAPI\_プロキシでは、次のコードを追加する必要がありますドライバーをサポートする TAPI バージョンを識別するためにビルドする前に、ソース ファイルに行です。

```Text
C_DEFINES=-DNDIS_TAPI_CURRENT_VERSION=0x00030000
```

WAN ミニポート ドライバーでは、インクルード パスは Ndiswan.h と Ndis.h を含める必要があります。

WAN ミニポート ドライバーでは、TAPI 経由の接続をサポートする場合、ドライバーは Ndistapi.h も含める必要があります。

 

 





