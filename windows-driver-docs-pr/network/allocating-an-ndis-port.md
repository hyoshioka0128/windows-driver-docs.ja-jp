---
title: NDIS ポートの割り当て
description: NDIS ポートの割り当て
ms.assetid: 39c77921-5841-40f5-90ba-0fba89b3b55e
keywords:
- ポートの割り当ての WDK NDIS
- NDIS、WDK のポートの割り当て
- NDIS ポートの割り当てください。
- WDK NDIS、最大数をポートします。
- NDIS ポート WDK、最大数
- WDK NDIS ポートの最大数
- ポートの状態が WDK NDIS
- 割り当てられているポート状態 WDK NDIS
- ポート番号
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: decc3b9c8065ff4b5f7e697b0b0d632a4c8bfcc8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367870"
---
# <a name="allocating-an-ndis-port"></a>NDIS ポートの割り当て





ミニポート アダプタの NDIS ポートを割り当て、ミニポート ドライバーを呼び出す、 [ **NdisMAllocatePort** ](https://msdn.microsoft.com/library/windows/hardware/ff562779)関数。 **NdisMAllocatePort**は同期と NDIS が正常に割り当てられた後、リソースを返しますが、ポートに必要です。

ミニポート ドライバーの呼び出しの前に**NdisMAllocatePort**、ドライバーを呼び出す必要があります、 [ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672) で属性を設定する関数[ **NDIS\_ミニポート\_アダプター\_登録\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565934)構造体。 ミニポート ドライバーが呼び出せる**NdisMAllocatePort**ミニポート アダプターへの呼び出し後の**NdisMSetMiniportAttributes** NDIS 呼び出される前に正常に返します、 [ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)そのミニポート アダプター関数。

NDIS は常に既定のポート (ポート 0) を割り当てるため、ミニポート ドライバーが既定のポートを割り当てることはできません。 NDIS ミニポート ドライバーは、フォームを返します。 既定のポートを解放[ *MiniportHaltEx*](https://msdn.microsoft.com/library/windows/hardware/ff559388)します。

NDIS は、ミニポート ドライバーを呼び出すときのポートにポート番号を割り当てます[ **NdisMAllocatePort**](https://msdn.microsoft.com/library/windows/hardware/ff562779)します。 ドライバーでは、ポートの特性を指定します、 [ **NDIS\_ポート\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff566791)ドライバー呼び出しの前に構造**NdisMAllocatePort**. ときに**NdisMAllocatePort**正常に返される、 **PortNumber**の NDIS メンバー\_ポート\_特性を*ポート特性*パラメーターは、その NDIS をポートに割り当てられているポート番号に設定を指定します。

返す前に[ *MiniportHaltEx*](https://msdn.microsoft.com/library/windows/hardware/ff559388)、ミニポート ドライバーを呼び出す必要があります、 [ **NdisMFreePort** ](https://msdn.microsoft.com/library/windows/hardware/ff563588)関数をすべてのポートを解放します。ミニポート アダプターに関連付けられます。 ミニポート アダプタの初期化に失敗した場合、ドライバーを呼び出す必要があります**NdisMFreePort**を解放するすべてのポートを返す前に割り当てられているドライバー、 [ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数。 NDIS ポートを解放する方法の詳細については、次を参照してください。[解放 NDIS ポート](freeing-an-ndis-port.md)します。

ミニポート ドライバーを割り当てることができるポートの最大数は、0 xffffff です。 ただし、実際には、ドライバーは、ポートの種類と、ドライバー アプリケーションの要件に基づいている最大数が設定されます。 たとえば、bridge アプリケーションでは、ポート数ない 16 を超える可能性があります。 ポートの数は、802.1 x サプリカントのポートを使用して、アクセス ポイントの高い、仮想プライベート ネットワーク (VPN) のポートを使用して、WAN のドライバーに対しては、大幅に高くなります。

ミニポート ドライバーでは、ポートを割り当てます後、は、ポートが割り当てられている状態で、およびポートがアクティブでないです。 送信およびデータの受信、状態表示の開始、OID 要求では、発行またはプラグ アンド プレイ (PnP) イベント、ポートがアクティブ化されるまでは開始ポートを使用できません。 NDIS 既定のポート自動的にアクティブ化、ミニポート ドライバー登録属性を設定した後、 [ **NDIS\_ミニポート\_アダプター\_登録\_属性** ](https://msdn.microsoft.com/library/windows/hardware/ff565934)構造体。 NDIS がアクティブ化しない既定のポートをミニポート ドライバーは、NDIS を設定できますを要求する\_ミニポート\_属性\_コントロール\_既定\_ポート、 **AttributeFlags**の NDIS メンバー\_ミニポート\_アダプター\_登録\_属性。

NDIS 通過する既定のポートの認証の状態、 [ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数の**DefaultPortAuthStates**のメンバー、 [**NDIS\_ミニポート\_INIT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff565972)構造体。 ミニポート ドライバーは、ミニポート ドライバーには、既定のポートがアクティブにしたときに、既定のポートを制御する場合は、既定の認証設定を使用して、既定のポートをアクティブ化できます。 既定のポートをアクティブ化についての詳細については、次を参照してください。[ライセンス NDIS ポート](activating-an-ndis-port.md)します。

ミニポート ドライバーは、NDIS を使用できます\_ポート\_CHAR\_使用\_既定\_AUTH\_でフラグを設定、**フラグ**のメンバー、 [**NDIS\_ポート\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff566791)ドライバーを割り当てるし、アクティブ化ポートの構造体。 NDIS 割り当ての場合、新しいポートを既定の認証状態を割り当てますに渡される認証の状態は無視されます、 [ **NdisMAllocatePort** ](https://msdn.microsoft.com/library/windows/hardware/ff562779)関数。

NDIS ポートの状態の詳細については、次を参照してください。 [NDIS ポートの状態](ndis-port-states.md)します。 ポートのアクティブ化についての詳細については、次を参照してください。[ライセンス NDIS ポート](activating-an-ndis-port.md)します。

 

 





