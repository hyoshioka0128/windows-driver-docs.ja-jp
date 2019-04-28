---
title: NDIS 6.3 にポート プロトコルまたはフィルター ドライバーへの変更の概要
description: NDIS 6.30 をサポートする NDIS 6.x プロトコルまたはフィルター ドライバーを更新するには、次のセクションで説明したよう変更する必要があります。
ms.assetid: 1C6CB2E1-C129-4F3B-AF7D-357580BEE7F8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfab77acb90427560709423227f8076ea5adfdd2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376947"
---
# <a name="summary-of-changes-required-to-port-a-protocol-or-filter-driver-to-ndis-630"></a>プロトコルまたはフィルター ドライバーを NDIS 6.30 に移植するために必要な変更の概要


NDIS 6.30 をサポートする NDIS 6.x プロトコルまたはフィルター ドライバーを更新するには、次のセクションで説明したよう変更する必要があります。

-   [環境を構築します。](#build-environment)
-   [一般的なプロトコル ドライバーの要件の移植](#general-porting-requirements-for-protocol-drivers)
-   [[全般] のフィルター ドライバーの要件の移植](#general-porting-requirements-for-filter-drivers)

## <a name="build-environment"></a>環境を構築します。


-   NDIS630 で存在する場合、NDIS60 または NDIS61 NDIS620、プリプロセッサの定義を置き換えます。
-   メジャーおよびマイナーの NDIS バージョン番号、NDIS で更新\_*Xxx*\_ドライバー\_特性構造」の説明に従って[NDIS 6.30 ドライバーを実装する](implementing-an-ndis-6-30-driver.md).

## <a name="general-porting-requirements-for-protocol-drivers"></a>一般的なプロトコル ドライバーの要件の移植


プロトコル ドライバーが完了する必要が常に**NetEventSetPower**パケットを待つことがなく。 詳細については、以下をご覧ください。

-   [NDIS 6.30 で電源管理の機能強化](power-management-enhancements-in-ndis-6-30.md)
-   [PnP イベントの処理とプロトコル ドライバーで電源管理イベント](handling-pnp-events-and-power-management-events-in-a-protocol-driver.md)

NDIS 6.30 機能の詳細については、次を参照してください。 [NDIS 6.30 概要](introduction-to-ndis-6-30.md)します。

## <a name="general-porting-requirements-for-filter-drivers"></a>[全般] のフィルター ドライバーの要件の移植


フィルター ドライバーが完了する必要が常に**NetEventSetPower**パケットを待つことがなく。 詳細については、以下をご覧ください。

-   [NDIS 6.30 で電源管理の機能強化](power-management-enhancements-in-ndis-6-30.md)
-   [**NDIS\_ミニポート\_アダプター\_登録\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565934)
-   [**NET\_PNP\_イベント**](https://msdn.microsoft.com/library/windows/hardware/ff568751)
-   [OID\_PNP\_設定\_電源](https://msdn.microsoft.com/library/windows/hardware/ff569780)

NDIS 6.30 機能の詳細については、次を参照してください。 [NDIS 6.30 概要](introduction-to-ndis-6-30.md)します。

 

 





