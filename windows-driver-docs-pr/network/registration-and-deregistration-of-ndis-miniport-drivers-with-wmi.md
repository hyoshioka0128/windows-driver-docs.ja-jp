---
title: 登録および wmi の NDIS ミニポート ドライバーの登録解除
description: 登録および wmi の NDIS ミニポート ドライバーの登録解除
ms.assetid: 7460cb3f-7dc1-4454-b683-e1849233fc1d
keywords:
- ミニポート アダプタ WDK ネットワーク、登録します。
- アダプター WDK ネットワーク、登録します。
- WMI の WDK ネットワーク、ミニポート アダプターを登録します。
- ミニポート ドライバーの登録
- ミニポート アダプタの登録
- ミニポート アダプタの WDK ネットワー キング、WMI
- WD アダプター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01397140076554bb1e7033f53b826674e31fa0c6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549201"
---
# <a name="registration-and-deregistration-of-ndis-miniport-drivers-with-wmi"></a>登録および wmi の NDIS ミニポート ドライバーの登録解除





NDIS では、各ミニポート アダプターが WMI を自動的に登録します。 ミニポート ドライバーが WMI を使って、明示的に登録する登録されるため NDIS 自動的に関連付けられているミニポート アダプターのミニポート ドライバーから返された後、 [ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数。

NDIS は、WMI でのデータ プロバイダーとしてミニポート アダプターを登録、WMI クライアント クエリを送信し、要求を設定および登録できる状態インジケーターを受信します。

NDIS ミニポート ドライバーを呼び出す前に[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)関数、NDIS 自動的に登録を解除しますミニポート アダプターの WMI と WMI、ミニポート ドライバーに WMI 要求を送信できなくようにします。

WMI に登録 NDIS ミニポート アダプターごとには、NDIS は、特定の Oid または状態インジケーターに対応する Guid を登録します。 NDIS は、ミニポート アダプターのサポートされている一連の標準の Oid と状態インジケーターの Guid を登録します。 これらの標準的な Guid の詳細については、[標準ミニポート ドライバー Oid に登録されている WMI](standard-miniport-driver-oids-registered-with-wmi.md)と[標準ミニポート ドライバーの状態に登録されている WMI](standard-miniport-driver-status-indications-registered-with-wmi.md)を参照してください。

NDIS は、カスタム Oid と状態インジケーターのカスタム Guid を登録することもできます。 ミニポート ドライバーでは、カスタム Oid をサポートする場合は、関連付けられたカスタム Guid を提供します。 カスタマイズされた Oid と状態インジケーターの詳細については、[カスタマイズされた Oid と状態インジケーター](customized-oids-and-status-indications.md)を参照してください。

接続指向のミニポート ドライバーでは、NDIS はまた、名前付き接続 (VCs) を登録します。 WMI クライアントは、スタンドアロンのコール マネージャー、またはクライアントの接続指向がという VCs のみを操作できます、 [ **NdisCoAssignInstanceName** ](https://msdn.microsoft.com/library/windows/hardware/ff561692)関数。 名前付きの VCs の NDIS WMI サポートの詳細については、[という名前の VCs のサポート](support-for-named-vcs.md)を参照してください。

 

 





