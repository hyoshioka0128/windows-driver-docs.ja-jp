---
title: WMI の NDIS サポート
description: WMI の NDIS サポート
ms.assetid: ce35ddb4-bf18-4ba1-bc6f-dbe659f5d781
keywords:
- Windows Management Instrumentation の WDK ネットワーク
- ミニポート ドライバー WDK ネットワー キング、WMI のサポート
- NDIS ミニポート ドライバー WDK には、WMI をサポートします。
- WMI の WDK ネットワーク
- プロトコル ドライバー WDK ネットワー キング、WMI のサポート
- NDIS プロトコル ドライバー WDK、WMI をサポートします。
- アイコン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: adf3052ca42132558adfc1e64445523bb9431862
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384389"
---
# <a name="ndis-support-for-wmi"></a>WMI の NDIS サポート





クライアントの Windows Management Instrumentation (WMI) を取得し、その NDIS および NDIS は、情報を設定する NDIS、を通じてサービス ドライバー。 WMI クライアントも、状態の更新プログラムを受信登録できます。

NDIS は、ミニポート アダプターが、WMI では、各ミニポート アダプターの仮想接続 (VCs) と一連のグローバル一意識別子 (Guid) をという名前が自動的に登録します。 これらの Guid の詳細については、次を参照してください。[標準ミニポート ドライバー Oid に登録されている WMI](standard-miniport-driver-oids-registered-with-wmi.md)します。 ミニポート ドライバーもなサポートを提供カスタム オブジェクト識別子 (Oid) とカスタム状態のインジケーターとして、 [Oid のカスタマイズと状態インジケーター](customized-oids-and-status-indications.md)トピックについて説明します。

NDIS では、プロトコルのドライバーの WMI のサポートは提供されません。 プロトコル ドライバー、または、中間のドライバーは自身のデバイス オブジェクトを作成し、WMI を直接登録できます。 WMI を直接登録の詳細については、次を参照してください。 [WMI データ プロバイダーとして登録する](https://docs.microsoft.com/windows-hardware/drivers/kernel/registering-as-a-wmi-data-provider)します。

WMI アーキテクチャの詳細については、次を参照してください。 [Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi)します。

このセクションの内容:

[登録および wmi の NDIS ミニポート ドライバーの登録解除](registration-and-deregistration-of-ndis-miniport-drivers-with-wmi.md)

[Guid の Oid をミニポート ドライバーの状態のマッピング](mapping-of-guids-to-oids-and-miniport-driver-status.md)

[名前付きの VCs のサポート](support-for-named-vcs.md)

[NDIS でサポートされている WMI の操作](ndis-supported-wmi-operations.md)

[標準の WMI の Oid と状態インジケーター](standard-wmi-oids-and-status-indications.md)

[カスタマイズされた Oid と状態インジケーター](customized-oids-and-status-indications.md)

[NDIS WMI Guid](ndis-wmi-guids.md)

 

 





