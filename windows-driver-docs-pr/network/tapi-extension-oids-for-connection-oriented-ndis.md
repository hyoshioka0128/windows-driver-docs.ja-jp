---
title: 接続指向の NDIS の TAPI 拡張 OID
description: このトピックでは、接続指向の NDIS TAPI 拡張機能の Oid をについて説明します。
ms.assetid: 06f7e2d0-b890-468e-8177-d3c28d0e9cd0
keywords:
- TAPI 拡張機能の Oid 接続指向の NDIS
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4696cec3aa91953fc254becc8ce2dc8fe2342fce
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384705"
---
# <a name="tapi-extension-oids-for-connection-oriented-ndis"></a>接続指向の NDIS の TAPI 拡張 OID

次の表では、接続指向のメディアを介したに TAPI 呼び出しを許可する Oid をまとめたものです。 クライアントの接続指向では、(MCM) ドライバー マネージャーまたは統合ミニポート コール マネージャーを呼び出す Oid これら送信します。

次の表では、M は、OID は必須では、O は、これは省略可能なことを示しますを示します。

| 長さ | クエリ | Set | 名前 |
| --- | --- | --- | --- |
| 不定 | O |   | [OID_CO_TAPI_ADDRESS_CAPS](oid-co-tapi-address-caps.md) |
| Sizeof(CO_TAPI_CM_CAPS) | O |   | [OID_CO_TAPI_CM_CAPS](oid-co-tapi-cm-caps.md) |
| 不定 | O |   | [OID_CO_TAPI_GET_CALL_DIAGNOSTICS](oid-co-tapi-get-call-diagnostics.md) |
| 不定 | O |   | [OID_CO_TAPI_LINE_CAPS](oid-co-tapi-line-caps.md) |
| 不定 | O |   | [OID_CO_TAPI_TRANSLATE_NDIS_CALLPARAMS](oid-co-tapi-translate-ndis-callparams.md) |
| 不定 | O |   | [OID_CO_TAPI_TRANSLATE_TAPI_CALLPARAMS](oid-co-tapi-translate-tapi-callparams.md) |
| 不定 | O |   | [OID_CO_TAPI_TRANSLATE_TAPI_SAP](oid-co-tapi-translate-tapi-sap.md) |

呼び出しで[NdisCoRequest](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff551877(v=vs.85))、TAPI の拡張機能の Oid のいずれかのクエリを実行するクライアントを指定する必要があります、 *NdisAfHandle*要求を適用するアドレス ファミリを識別します。 クライアントを指定できます、 *NdisVcHandle*要求が適用される仮想接続 (VC) を識別します。 コール マネージャーまたは MCM のドライバーがこの VC ハンドルからは、特定の行と、要求を適用するアドレスなどを派生させることができます。

