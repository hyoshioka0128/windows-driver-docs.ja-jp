---
title: NDIS 中間ドライバーとしての登録
description: NDIS 中間ドライバーとしての登録
ms.assetid: 4a095fa7-0d8f-4d7d-885c-bc43cd34c784
keywords:
- 中間ドライバーの登録
- ドライバー WDK 中級レベルのネットワーク、登録します。
- NDIS 中間ドライバ、WDK を登録します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 170d1baa08dfde890655d6fa1343da2878338dc0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364080"
---
# <a name="registering-as-an-ndis-intermediate-driver"></a>NDIS 中間ドライバーとしての登録





NDIS 中間ドライバーを登録する必要があります、 *MiniportXxx*関数とその*ProtocolXxx* NDIS との関数のコンテキストでその[ **DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff544113)関数。 登録するその*MiniportXxx*関数、中間のドライバーを呼び出す必要があります[ **NdisMRegisterMiniportDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff563654) NDIS と\_中間\_ドライバーのフラグを設定します。 このフラグは、 [ **NDIS\_ミニポート\_ドライバー\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565958)構造で、ドライバーが渡される*MiniportDriverCharacteristics*します。 この呼び出しは、中間のドライバーをエクスポートします*MiniportXxx*関数。 登録の詳細については*MiniportXxx*関数を参照してください[ミニポート ドライバーとして中間のドライバーを登録する](registering-an-intermediate-driver-as-a-miniport-driver.md)します。

中間ドライバーがその仮想ミニポートが初期化されると、そのため、ドライバーがそのまま使用する準備が場合送信し、アダプターで要求を制御に注意してください。 NDIS ドライバーの中間の呼び出し[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数と、プラグ アンド プレイ (PnP) マネージャーで仮想ミニポート デバイスが開始した後、中間のドライバーがを呼び出した後[**NdisIMInitializeDeviceInstanceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff562727)デバイスにします。 呼び出し*MiniportInitializeEx*は後で発生することができます、そのため必ずしもへの呼び出しのコンテキスト内で**NdisIMInitializeDeviceInstanceEx**します。 中間のドライバーが 1 つ以上の仮想ミニポートをエクスポートする場合、ドライバーを呼び出す必要があります**NdisIMInitializeDeviceInstanceEx**の各仮想ミニポート ネットワーク要求を利用できるようにします。

登録するその*ProtocolXxx*関数、中間のドライバーを呼び出す必要があります、 [ **NdisRegisterProtocolDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff564520)関数。 登録の詳細については*ProtocolXxx*関数を参照してください[プロトコル ドライバーとして中間のドライバーを登録する](registering-an-intermediate-driver-as-a-protocol.md)します。

 

 





