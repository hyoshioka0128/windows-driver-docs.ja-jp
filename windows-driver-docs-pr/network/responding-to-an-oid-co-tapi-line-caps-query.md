---
title: OID_CO_TAPI_LINE_CAPS クエリへの応答
description: OID_CO_TAPI_LINE_CAPS クエリへの応答
ms.assetid: b1ca65c6-ecce-4d2c-b7ca-03b6a334f97b
keywords:
- 音声ストリーミング WDK のネットワーク、サポート仕様
- OID_CO_TAPI_LINE_CAPS
- ulMediaModes
- ulAddressTypes
- UlGenerateDigitModes
- UlMonitorDigitModes
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ef500476811f8950e8c03f40de3c5b9fe8e85fe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384701"
---
# <a name="responding-to-an-oidcotapilinecaps-query"></a>OID に応答して\_CO\_TAPI\_行\_CAP クエリ





応答、 [OID\_CO\_TAPI\_行\_CAP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-co-tapi-line-caps)クエリ、コール マネージャーまたは MCM 返します CO\_TAPI\_行\_CAPS 構造体行を格納している\_DEV\_CAPS 構造体。 音声のストリーミングをサポートするコール マネージャーまたは MCM する必要があります、次の値で指定します線\_DEV\_CAPS 構造体。

-   **ulMediaModes**

    このフィールドは LINEMEDIAMODE を含める必要があります\_TAPIMEDIAMODE にマップする、AUTOMATEDVOICE\_TAPI 3.0 でオーディオです。

-   **ulAddressTypes**

    このフィールド適切に入力する必要があります。 有効な値については、の説明を参照してください。 **dwAddressTypes** 、Microsoft Windows SDK ドキュメント。 このフィールドを 0 にする必要がありますはできません。

-   **ulGenerateDigitModes**

    このフィールドは、LINEDIGITMODE のビットごとの OR を使用して入力する必要があります\_行に生成できる数字のモードを指定する定数。 LINEDIGITMODE の説明については\_、定数の説明を参照して**dwGenerateDigitModes** Windows SDK のドキュメント。

-   **ulMonitorDigitModes**

    このフィールドは、LINEDIGITMODE のビットごとの OR を使用して入力する必要があります\_この行で検出できるよりも桁モードを指定する定数。 LINEDIGITMODE の説明については\_定数の説明を参照して**dwMonitorDigitModes** Windows SDK のドキュメント。

 

 





