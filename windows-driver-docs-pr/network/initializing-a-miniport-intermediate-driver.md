---
title: ミニポート中間ドライバーの初期化
description: ミニポート中間ドライバーの初期化
ms.assetid: b0beea1f-7374-49e9-9650-0bdb37902469
keywords:
- NDIS 中間ドライバ、WDK の初期化
- ドライバー WDK 中級レベルのネットワーク、初期化しています
- ミニポート中間ドライバーの初期化
- ミニポート中間ドライバー WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20a705826c93ac3511218a85a1571efdbf2f6571
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325014"
---
# <a name="initializing-a-miniport-intermediate-driver"></a>ミニポート中間ドライバーの初期化





ミニポート中間ドライバーには、仮想デバイス用のミニポート ドライバー、プロトコル ドライバーでは、物理デバイスのミニポート ドライバーが統合されています。 ミニポート ドライバーの上層に中間のドライバーと同様にミニポート中間ドライバー機能。 このようなドライバーには、2 つの個別のドライバーとなる可能性があるパフォーマンスの低下を発生させずに、基になるミニポート ドライバーと直接通信する中間のドライバーができます。

ミニポート中間ドライバーを呼び出してその物理ミニポート ドライバーに登録する、 [ **NdisMRegisterMiniportDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff563654)ミニポート ドライバーと同様の適切なパラメーターを持つ関数です。 その仮想のミニポート ドライバーの呼び出しを登録する**NdisMRegisterMiniportDriver** NDIS がもう一度、\_中間\_ドライバー フラグの設定の構造で*MiniportDriverCharacteristics*します。

ミニポート中間ドライバーの場合は、各仮想または物理デバイス インスタンスの場合、 **IMMiniport**にレジストリ キーが設定されている**DWORD:0x0000001**、NDIS 呼び出し、 [ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)仮想デバイスのドライバーが登録されている関数。 それ以外の場合、ドライバーの呼び出す NDIS *MiniportInitializeEx*物理的なデバイス ドライバーが登録されている関数。

 

 





