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
ms.openlocfilehash: 8bb5f11c654adf814a47ed669fad989fdaf2bef9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387371"
---
# <a name="ndis-support-for-wmi"></a>WMI の NDIS サポート





クライアントの Windows Management Instrumentation (WMI) を取得し、その NDIS および NDIS は、情報を設定する NDIS、を通じてサービス ドライバー。 WMI クライアントも、状態の更新プログラムを受信登録できます。

NDIS は、ミニポート アダプターが、WMI では、各ミニポート アダプターの仮想接続 (VCs) と一連のグローバル一意識別子 (Guid) をという名前が自動的に登録します。 これらの Guid の詳細については、次を参照してください。[標準ミニポート ドライバー Oid に登録されている WMI](standard-miniport-driver-oids-registered-with-wmi.md)します。 ミニポート ドライバーもなサポートを提供カスタム オブジェクト識別子 (Oid) とカスタム状態のインジケーターとして、 [Oid のカスタマイズと状態インジケーター](customized-oids-and-status-indications.md)トピックについて説明します。

NDIS では、プロトコルのドライバーの WMI のサポートは提供されません。 プロトコル ドライバー、または、中間のドライバーは自身のデバイス オブジェクトを作成し、WMI を直接登録できます。 WMI を直接登録の詳細については、次を参照してください。 [WMI データ プロバイダーとして登録する](https://msdn.microsoft.com/library/windows/hardware/ff560870)します。

WMI アーキテクチャの詳細については、次を参照してください。 [Windows Management Instrumentation](https://msdn.microsoft.com/library/windows/hardware/ff547139)します。

このセクションの内容:

[登録および wmi の NDIS ミニポート ドライバーの登録解除](registration-and-deregistration-of-ndis-miniport-drivers-with-wmi.md)

[Guid の Oid をミニポート ドライバーの状態のマッピング](mapping-of-guids-to-oids-and-miniport-driver-status.md)

[名前付きの VCs のサポート](support-for-named-vcs.md)

[NDIS でサポートされている WMI の操作](ndis-supported-wmi-operations.md)

[標準の WMI の Oid と状態インジケーター](standard-wmi-oids-and-status-indications.md)

[カスタマイズされた Oid と状態インジケーター](customized-oids-and-status-indications.md)

[NDIS WMI Guid](ndis-wmi-guids.md)

 

 





