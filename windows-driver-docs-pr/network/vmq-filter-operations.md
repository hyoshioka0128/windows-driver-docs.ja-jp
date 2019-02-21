---
title: VMQ フィルター操作
description: VMQ フィルター操作
ms.assetid: e8a977e8-2622-461b-9ca0-4834d33d76c0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d2d302ebbb59a912a22fe9a1b446528ad6b1d0f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532368"
---
# <a name="vmq-filter-operations"></a>VMQ フィルター操作





複数のフィルターの受信し、受信キューに設定することができます。 また、現在 VMQ の実装では、仮想ローカル エリア ネットワーク (VLAN) id を検査する省略可能なフィルターと受信パケットの宛先メディア アクセス制御 (MAC) アドレスのフィルターをサポートします。

次の図は、VLAN 識別子と MAC アドレスのテスト、フィルター、およびキュー間の関係を示します。

![vlan 識別子と mac アドレスのテスト、フィルター、およびキューの間の関係を示す図](images/vmqfilter.png)

前の図では、ネットワーク データ パケットには、送信先アドレス (DA) と VLAN 識別子のフィールドが含まれています。 ネットワーク アダプターのハードウェアでは、ミニポート ドライバーが受信され、ネットワーク アダプターのハードウェアの設定の設定に基づいて、キューにフィルターを実装します。 受信キューにフィルターの設定に関する詳細については、次を参照してください。[設定および VMQ のフィルターをクリアする](setting-and-clearing-vmq-filters.md)します。

この図では、2 つのフィルター各フィルターは、送信先アドレスと、着信パケット内のフィールドに、VLAN 識別子を比較します。 DA や VLAN の両方のテストが一致する場合は、そのフィルターの条件が満たされるし、着信パケットがキューに割り当てられています。 [キュー]、次の任意のフィルターに一致する 1 つ以上のフィルターがある場合、ネットワーク アダプターは、キューにパケットを割り当てます。

 

 





