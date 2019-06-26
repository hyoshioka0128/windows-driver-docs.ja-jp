---
title: 名前付き VC のサポート
description: 名前付き VC のサポート
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
ms.openlocfilehash: 61cc42d335bd53104f26c39ad00d20e60b7329b4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384201"
---
# <a name="support-for-named-vcs"></a>名前付き VC のサポート





NDIS は、WMI クライアント クエリを実行し、接続指向ミニポート アダプター仮想接続 (VC) ごとに情報を設定できます。 WMI クライアントまた VCs を列挙します。 WMI クライアントでは、クエリを実行したり、特定の VC に関連付けられている情報を設定することが、前に、スタンドアロンのコール マネージャーまたはクライアントの接続指向名前する必要があります、VC を呼び出して、 [ **NdisCoAssignInstanceName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscoassigninstancename)関数。

スタンドアロンの呼び出しの後にマネージャーまたは接続指向のクライアント設定を開始します VC の呼び出すことによって、 [ **NdisCoCreateVC** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscocreatevc)関数では、スタンドアロンのコール マネージャーまたはクライアントの接続指向のことができます名前と VC **NdisCoAssignInstanceName**します。 VC のインスタンスの名前を割り当てますの NDIS および WMI でインスタンス名を登録します。 WMI クライアントでは、VC とクエリを列挙し、または、VC を基準と Oid を設定できます。

ミニポート コール マネージャー (MCM) は使用できません[ **NdisCoAssignInstanceName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscoassigninstancename)の VCs を名前にします。 代わりに、MCM は、VC のカスタム GUID と OID を作成し、NDIS を GUID の OID にマッピングを登録する必要があります。 カスタム Oid の登録の詳細については、次を参照してください。 [Oid のカスタマイズと状態インジケーター](customized-oids-and-status-indications.md)します。

 

 





