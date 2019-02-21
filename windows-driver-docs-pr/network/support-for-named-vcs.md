---
title: 名前付きの VCs のサポート
description: 名前付きの VCs のサポート
ms.assetid: 797f737c-91e7-410b-91d5-5575d5b19e86
keywords:
- WMI の WDK、仮想ネットワークの接続
- ネットワーク、仮想接続の名前を付け、マネージャー WDK を呼び出す
- 仮想接続 WDK NDIS WMI
- VCs WDK NDIS WMI
- 仮想接続の名前を付け、ミニポート コール マネージャー WDK ネットワーク
- MCMs WDK ネットワー キング、namin
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b061c9832f77d1a9a7034a58b809d35a6e52afd0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558793"
---
# <a name="support-for-named-vcs"></a>名前付きの VCs のサポート





NDIS は、WMI クライアント クエリを実行し、接続指向ミニポート アダプター仮想接続 (VC) ごとに情報を設定できます。 WMI クライアントまた VCs を列挙します。 WMI クライアントでは、クエリを実行したり、特定の VC に関連付けられている情報を設定することが、前に、スタンドアロンのコール マネージャーまたはクライアントの接続指向名前する必要があります、VC を呼び出して、 [ **NdisCoAssignInstanceName** ](https://msdn.microsoft.com/library/windows/hardware/ff561692)関数。

スタンドアロンの呼び出しの後にマネージャーまたは接続指向のクライアント設定を開始します VC の呼び出すことによって、 [ **NdisCoCreateVC** ](https://msdn.microsoft.com/library/windows/hardware/ff561696)関数では、スタンドアロンのコール マネージャーまたはクライアントの接続指向のことができます名前と VC **NdisCoAssignInstanceName**します。 VC のインスタンスの名前を割り当てますの NDIS および WMI でインスタンス名を登録します。 WMI クライアントでは、VC とクエリを列挙し、または、VC を基準と Oid を設定できます。

ミニポート コール マネージャー (MCM) は使用できません[ **NdisCoAssignInstanceName** ](https://msdn.microsoft.com/library/windows/hardware/ff561692)の VCs を名前にします。 代わりに、MCM は、VC のカスタム GUID と OID を作成し、NDIS を GUID の OID にマッピングを登録する必要があります。 カスタム Oid の登録の詳細については、次を参照してください。 [Oid のカスタマイズと状態インジケーター](customized-oids-and-status-indications.md)します。

 

 





