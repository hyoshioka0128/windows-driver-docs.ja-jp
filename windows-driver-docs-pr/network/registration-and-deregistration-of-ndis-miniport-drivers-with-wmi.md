---
title: NDIS ミニポート ドライバーの WMI への登録および登録解除
description: NDIS ミニポート ドライバーの WMI への登録および登録解除
ms.assetid: 7460cb3f-7dc1-4454-b683-e1849233fc1d
keywords:
- ミニポートアダプター WDK ネットワーク、登録
- WDK ネットワークのアダプター、登録
- WMI WDK ネットワーク, ミニポートアダプターの登録
- ミニポートドライバーの登録
- ミニポートアダプターの登録
- ミニポートアダプター WDK ネットワーク、WMI
- アダプター WD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0f0bd99916f75b192980546962bf6545402fab5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842064"
---
# <a name="registration-and-deregistration-of-ndis-miniport-drivers-with-wmi"></a>NDIS ミニポート ドライバーの WMI への登録および登録解除





NDIS では、各ミニポートアダプターが自動的に WMI に登録されます。 ミニポートドライバーは、ミニポートドライバーから[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数が返された後に、関連するミニポートアダプターに自動的に登録されるため、WMI に明示的に登録する必要はありません。

NDIS がミニポートアダプターをデータプロバイダーとして WMI に登録した後、WMI クライアントは it クエリを送信し、要求を設定して、状態の表示を受信するように登録できます。

NDIS がミニポートドライバーのミニ[*Porthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数を呼び出す前に、ndis はミニポートアダプターを wmi に自動的に解除して、wmi がミニポートドライバーに wmi 要求を送信しないようにします。

Ndis は、NDIS が WMI に登録する各ミニポートアダプターについて、特定の Oid または状態の兆候に対応する Guid を登録します。 NDIS は、ミニポートアダプターでサポートされている標準の Oid と状態を示すセットの Guid を登録します。 これらの標準 Guid の詳細については、「 [wmi に登録されている標準ミニポートドライバー oid](standard-miniport-driver-oids-registered-with-wmi.md) 」と「 [Wmi に登録されている標準ミニポートドライバーの状態](standard-miniport-driver-status-indications-registered-with-wmi.md)」を参照してください。

また、カスタムの Oid と状態を示すカスタム Guid を登録することもできます。 ミニポートドライバーでカスタム Oid がサポートされている場合は、関連付けられているカスタム Guid を提供する必要があります。 カスタマイズされた Oid と状態の表示の詳細については、「カスタマイズされた[oid と状態](customized-oids-and-status-indications.md)の表示」を参照してください。

接続指向のミニポートドライバーでは、NDIS によって名前付き仮想接続 (VCs) も登録されます。 WMI クライアントは、スタンドアロンの呼び出しマネージャー (または接続指向クライアント) に[**NdisCoAssignInstanceName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscoassigninstancename)関数を使用して名前が付けられている VCs でのみ機能します。 名前付き VCs の NDIS WMI サポートの詳細については、「[名前付き vcs のサポート](support-for-named-vcs.md)」を参照してください。

 

 





