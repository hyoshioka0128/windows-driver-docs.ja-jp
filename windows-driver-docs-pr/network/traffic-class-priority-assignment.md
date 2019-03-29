---
title: トラフィック クラス優先順位割り当て
description: トラフィック クラス優先順位割り当て
ms.assetid: 846AC7E6-28D9-4610-9493-BE547869AB15
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a998ea9d816eb812ae4bd26846270e8003bd70aa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581208"
---
# <a name="traffic-class-priority-assignment"></a>トラフィック クラス優先順位割り当て


Enhanced Transmission Selection (ETS) アルゴリズムでは、これで、トラフィック クラスの 802.1p の優先度レベルが割り当てられますメソッドを指定します。 ETS が IEEE 802.1 qaz で指定されたドラフト標準。 この標準は、IEEE 802.1 データ センター ブリッジング (DCB) インターフェイスのフレームワークの一部です。

NDIS サービスの品質 (QoS) トラフィック クラスは、一連のネットワーク アダプターの送信、処理方法を決定するポリシーを指定または*エグレス*パケット。 ETS、トラフィック クラスごとにパケットを送信するための IEEE 802.1p の優先度レベルが割り当てられます。 トラフィック クラスは、IEEE 802.1p の優先度レベルに割り当てることができます。 ただし、各 IEEE 802.1p の優先度レベルは 1 つのトラフィック クラスにのみ割り当てることができます。

NDIS QoS パラメーターを使用して指定、 [ **NDIS\_QOS\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451640)構造体。 **PriorityAssignmentTable**メンバーにトラフィック クラスごとに優先順位の割り当てを指定する配列が含まれています。

優先度レベルの詳細については、次を参照してください。 [IEEE 802.1p の優先度レベル](ieee-802-1p-priority-levels.md)します。

 

 





