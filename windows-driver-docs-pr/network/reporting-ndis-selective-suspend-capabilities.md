---
title: NDIS セレクティブ サスペンド機能のレポート
description: NDIS セレクティブ サスペンド機能のレポート
ms.assetid: 8A738A51-D116-4DDC-96B7-17D046B6890D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0b07dbfb0e9339dcd93a336f0987f2e896ff9ed
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842038"
---
# <a name="reporting-ndis-selective-suspend-capabilities"></a>NDIS セレクティブ サスペンド機能のレポート


NDIS 6.30 以降では、ドライバーが NDIS のセレクティブサスペンドのサポートを有効にしたかどうかをミニポートドライバーで報告する必要があります。 NDIS のセレクティブサスペンドのサポートは、 **\*SelectiveSuspend**標準化された INF キーワードの設定によって有効または無効になります。 この INF キーワードの詳細については、「 [NDIS 選択的中断の標準化](standardized-inf-keywords-for-ndis-selective-suspend.md)された inf キーワード」を参照してください。

NDIS がドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出すと、ミニポートドライバーは、次の手順に従って、ndis セレクティブサスペンドサポートのサポートを報告します。

1.  このドライバーは、基盤となるハードウェアの電源管理機能を使用して、 [**NDIS\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)構造を初期化します。

    ドライバーで NDIS セレクティブサスペンドのサポートが有効になっている場合は、次のように、 [**ndis\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)構造のメンバーを設定する必要があります。

    -   ミニポートドライバーでは、 [**ndis\_pm\_機能\_リビジョン\_2 および ndis\_SIZEOF\_ndis\_pm\_機能\_リビジョン\_2 を指定する必要があります。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)構造体の**ヘッダー**メンバー内にある NDIS\_PM\_機能構造体。
    -   **\*SelectiveSuspend**キーワードの値が1の場合、NDIS のセレクティブサスペンドに対するミニポートドライバーのサポートが有効になります。 ミニポートドライバーは、この構造体の**Flags**メンバー内で、NDIS\_PM\_選択的\_SUSPEND\_supported フラグを設定することによってこれを報告します。

2.  [**Ndis\_PM\_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)構造体が初期化されると、ミニポートドライバーは 、 [**NDIS\_ミニポート\_アダプターの PowerManagementCapabilitiesEx メンバーを\_全般に設定\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)初期化された**NDIS\_PM\_CAPABILITIES**構造体を指す属性構造体。 ドライバーが[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)を呼び出すと、ミニポートドライバーは、 *miniportattributes*パラメーターの **\_全般\_属性構造に、NDIS\_ミニポート\_アダプター**へのポインターを渡します。プロシージャ.

ミニポートドライバーが NDIS の選択的中断のサポート状態を報告するために使用する方法は、電源管理機能を報告するための NDIS 6.20 の方法に基づいています。 この方法の詳細については、「[電源管理機能のレポート](reporting-power-management-capabilities.md)」を参照してください。

アダプター初期化プロセスの詳細については、「[ミニポートアダプターの初期化](initializing-a-miniport-adapter.md)」を参照してください。

 

 





