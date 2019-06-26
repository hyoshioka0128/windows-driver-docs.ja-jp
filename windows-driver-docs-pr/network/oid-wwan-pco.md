---
title: OID_WWAN_PCO
description: OID_WWAN_PCO では、状態と、モデムが演算子のネットワークから受信した PCO 値のペイロードを報告します。
ms.assetid: BE664B41-3FE7-4E93-8739-12BD2F0AE5B8
keywords:
- OID_WWAN_PCO、PCO OID
ms.date: 08/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8eeec5c7afe4ae3762233bfc8f65a78a28175793
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360777"
---
# <a name="oidwwanpco"></a>OID_WWAN_PCO

OID_WWAN_PCO では、状態と、モデムが携帯電話会社ネットワークから受信したプロトコル構成 Optiont (PCO) 値のペイロードを報告します。 モデムから返される PCO 値は、OID 要求の構造でポート番号を示す PDN に対応します。

クエリ要求を処理、モデムまず応答 NDIS_STATUS_INDICATION_REQUIRED でこの OID を受信するとします。 [NDIS_STATUS_WWAN_PCO_STATUS](ndis-status-wwan-pco-status.md)を含む通知が返されます、 [NDIS_WWAN_PCO_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_pco_status)クエリ要求が完了したときに構造体します。 **NDIS_WWAN_PCO_STATUS**、PCO 状態を格納し、 [WWAN_PCO_VALUE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_pco_value) PCO 値を表す構造体です。

要求のセットには適用されません。

## <a name="remarks"></a>注釈

新しいをサポートしているホストからのクエリ要求を受信する Microsoft の受信トレイ ミニポート クラス ドライバーを使用するモデム、モデムが提供する必要があります**MBIM_CID_PCO** CID (インデックス = 9) で、 **MBB_UUID_BASIC_CONNECT_EXT_CONSTANT**サービスに応答するとき、 **MBIM_CID_DEVICE_SERVICES**クエリ。 詳細について*MBIM_CID_PCO*を参照してください[MB プロトコルの構成オプション (PCO) 操作](mb-protocol-configuration-options-pco-operations.md)します。

モデムのミニポート ドライバーがサポートしていることをアドバタイズする必要があります選択モデム WWANSVC からクエリ要求を受信する Microsoft の受信トレイ ミニポート クラス ドライバー、使用、 *WWAN_OPTIONAL_SERVICE_CAPS_PCO*応答するときのオプション[OID OID_WWAN_DEVICE_CAPS_EX](oid-wwan-device-caps-ex.md)要求のクエリを実行します。

## <a name="requirements"></a>必要条件

| | |
| --- | --- |
| バージョン | Windows 10 バージョン 1709 |
| Header | Ntddndis.h (include Ndis.h) |

## <a name="see-also"></a>関連項目

[**NDIS_STATUS_WWAN_PCO_STATUS**](ndis-status-wwan-pco-status.md)

[**NDIS_WWAN_PCO_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_pco_status)

[**WWAN_PCO_VALUE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_pco_value) 

[**OID OID_WWAN_DEVICE_CAPS_EX**](oid-wwan-device-caps-ex.md)

[MB プロトコルの構成オプション (PCO) 操作](mb-protocol-configuration-options-pco-operations.md)
