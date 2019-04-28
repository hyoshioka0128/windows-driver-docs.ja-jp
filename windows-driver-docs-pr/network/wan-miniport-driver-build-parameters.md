---
title: WAN ミニポート ドライバー ビルド パラメーター
description: WAN ミニポート ドライバー ビルド パラメーター
ms.assetid: 8e494bd2-c499-48bf-8574-7e8df05be4c8
keywords:
- WAN ミニポート ドライバー WDK ネットワーク、構成
- いる CoNDIS WAN ドライバー WDK ネットワー キング、ビルド
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1994189dcdeda2bb602c3466418e16fccd510302
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380572"
---
# <a name="wan-miniport-driver-build-parameters"></a>WAN ミニポート ドライバー ビルド パラメーター





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

 

 





