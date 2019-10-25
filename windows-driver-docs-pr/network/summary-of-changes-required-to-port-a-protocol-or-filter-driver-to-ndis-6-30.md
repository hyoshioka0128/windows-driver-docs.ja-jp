---
title: NDIS 6.3 へのポートプロトコルまたはフィルタードライバーへの変更の概要
description: Ndis 6. x プロトコルまたはフィルタードライバーを更新して NDIS 6.30 をサポートするには、次のセクションで説明されているように変更する必要があります。
ms.assetid: 1C6CB2E1-C129-4F3B-AF7D-357580BEE7F8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1f75ecb622a6374d28a002b3bfb7f1fa2335920
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841805"
---
# <a name="summary-of-changes-required-to-port-a-protocol-or-filter-driver-to-ndis-630"></a>プロトコルまたはフィルター ドライバーを NDIS 6.30 に移植するために必要な変更の概要


Ndis 6. x プロトコルまたはフィルタードライバーを更新して NDIS 6.30 をサポートするには、次のセクションで説明されているように変更する必要があります。

-   [ビルド環境](#build-environment)
-   [プロトコルドライバーの一般的な移植要件](#general-porting-requirements-for-protocol-drivers)
-   [フィルタードライバーの一般的な移植要件](#general-porting-requirements-for-filter-drivers)

## <a name="build-environment"></a>ビルド環境


-   プリプロセッサ定義 NDIS60 または NDIS61 または NDIS620 (存在する場合) を NDIS630 に置き換えます。
-   「Ndis [6.30 ドライバーの実装](implementing-an-ndis-6-30-driver.md)」で説明されているように、Ndis\_*Xxx*\_ドライバー\_特性の構造に含まれるメジャーおよびマイナーバージョン番号を更新します。

## <a name="general-porting-requirements-for-protocol-drivers"></a>プロトコルドライバーの一般的な移植要件


プロトコルドライバーは、常にパケットを待機せずに**NetEventSetPower**を完了する必要があります。 詳しくは、次のトピックをご覧ください。

-   [NDIS 6.30 の電源管理の機能強化](power-management-enhancements-in-ndis-6-30.md)
-   [プロトコルドライバーでの PnP イベントと電源管理イベントの処理](handling-pnp-events-and-power-management-events-in-a-protocol-driver.md)

NDIS 6.30 の機能の詳細については、「 [ndis 6.30 の概要](introduction-to-ndis-6-30.md)」を参照してください。

## <a name="general-porting-requirements-for-filter-drivers"></a>フィルタードライバーの一般的な移植要件


フィルタードライバーは、常にパケットを待機せずに**NetEventSetPower**を完了する必要があります。 詳しくは、次のトピックをご覧ください。

-   [NDIS 6.30 の電源管理の機能強化](power-management-enhancements-in-ndis-6-30.md)
-   [**NDIS\_ミニポート\_アダプター\_登録\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)
-   [**NET\_PNP\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event)
-   [OID\_PNP\_設定\_電源](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)

NDIS 6.30 の機能の詳細については、「 [ndis 6.30 の概要](introduction-to-ndis-6-30.md)」を参照してください。

 

 





