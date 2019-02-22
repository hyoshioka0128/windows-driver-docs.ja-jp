---
title: OID_WWAN_PCO
description: OID_WWAN_PCO では、状態と、モデムが演算子のネットワークから受信した PCO 値のペイロードを報告します。
ms.assetid: BE664B41-3FE7-4E93-8739-12BD2F0AE5B8
keywords:
- OID_WWAN_PCO、PCO OID
ms.date: 08/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5b6d0a71570cb0afa66b2c1181d1a3c6b24edfd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536000"
---
# <a name="oidwwanpco"></a>OID_WWAN_PCO

OID_WWAN_PCO では、状態と、モデムが携帯電話会社ネットワークから受信したプロトコル構成 Optiont (PCO) 値のペイロードを報告します。 モデムから返される PCO 値は、OID 要求の構造でポート番号を示す PDN に対応します。

クエリ要求を処理、モデムまず応答 NDIS_STATUS_INDICATION_REQUIRED でこの OID を受信するとします。 [NDIS_STATUS_WWAN_PCO_STATUS](ndis-status-wwan-pco-status.md)を含む通知が返されます、 [NDIS_WWAN_PCO_STATUS](https://msdn.microsoft.com/library/windows/hardware/C71187C5-74B6-450A-8461-BB9FDF60DB8D)クエリ要求が完了したときに構造体します。 **NDIS_WWAN_PCO_STATUS**、PCO 状態を格納し、 [WWAN_PCO_VALUE](https://msdn.microsoft.com/library/windows/hardware/45A499CE-2C9A-4070-BEF8-880E7673FA8E) PCO 値を表す構造体です。

要求のセットには適用されません。

## <a name="remarks"></a>注釈

新しいをサポートしているホストからのクエリ要求を受信する Microsoft の受信トレイ ミニポート クラス ドライバーを使用するモデム、モデムが提供する必要があります**MBIM_CID_PCO** CID (インデックス = 9) で、 **MBB_UUID_BASIC_CONNECT_EXT_CONSTANT**サービスに応答するとき、 **MBIM_CID_DEVICE_SERVICES**クエリ。 詳細について*MBIM_CID_PCO*を参照してください[MB プロトコルの構成オプション (PCO) 操作](mb-protocol-configuration-options-pco-operations.md)します。

モデムのミニポート ドライバーがサポートしていることをアドバタイズする必要があります選択モデム WWANSVC からクエリ要求を受信する Microsoft の受信トレイ ミニポート クラス ドライバー、使用、 *WWAN_OPTIONAL_SERVICE_CAPS_PCO*応答するときのオプション[OID OID_WWAN_DEVICE_CAPS_EX](oid-wwan-device-caps-ex.md)要求のクエリを実行します。

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows 10 バージョン 1709 |
| Header | Ntddndis.h (include Ndis.h) |

## <a name="see-also"></a>関連項目

[**NDIS_STATUS_WWAN_PCO_STATUS**](ndis-status-wwan-pco-status.md)

[**NDIS_WWAN_PCO_STATUS**](https://msdn.microsoft.com/library/windows/hardware/C71187C5-74B6-450A-8461-BB9FDF60DB8D)

[**WWAN_PCO_VALUE**](https://msdn.microsoft.com/library/windows/hardware/45A499CE-2C9A-4070-BEF8-880E7673FA8E) 

[**OID OID_WWAN_DEVICE_CAPS_EX**](oid-wwan-device-caps-ex.md)

[MB プロトコルの構成オプション (PCO) 操作](mb-protocol-configuration-options-pco-operations.md)
