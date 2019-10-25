---
title: 名前付き VC のサポート
description: 名前付き VC のサポート
ms.assetid: 797f737c-91e7-410b-91d5-5575d5b19e86
keywords:
- WMI WDK ネットワーク, 仮想接続
- 呼び出しマネージャーの WDK ネットワーク、仮想接続の名前付け
- 仮想接続 WDK NDIS WMI
- VCs WDK NDIS WMI
- ミニポート呼び出しマネージャー WDK ネットワーク、仮想接続の名前付け
- MCMs WDK ネットワーク、namin
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4039d70d9117bb40d86f3e9e7f3df53e85368b8f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841800"
---
# <a name="support-for-named-vcs"></a>名前付き VC のサポート





NDIS を使用すると、WMI クライアントは、接続指向のミニポートアダプターについて、仮想接続 (VC) ごとに照会し、情報を設定することができます。 WMI クライアントでは、VCs を列挙することもできます。 WMI クライアントが特定の VC に関連付けられている情報を照会または設定するには、スタンドアロンコールマネージャーまたは接続指向クライアントが、 [**NdisCoAssignInstanceName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscoassigninstancename)関数を呼び出すことによって vc に名前を付ける必要があります。

スタンドアロンコールマネージャーまたは接続指向クライアントが、 [**NdisCoCreateVC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscocreatevc)関数を呼び出すことによって vc のセットアップを開始した後、スタンドアロンコールマネージャーまたは接続指向クライアントは、Vc に**NdisCoAssignInstanceName**という名前を付けます。 NDIS は、VC にインスタンス名を割り当て、インスタンス名を WMI に登録します。 WMI クライアントは、vc とクエリを列挙したり、VC に対して相対的な Oid を設定したりできます。

ミニポートコールマネージャー (MCM) では、 [**NdisCoAssignInstanceName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscoassigninstancename)を使用して VCs に名前を指定することはできません。 代わりに、MCM で VC のカスタム GUID と OID を作成し、その GUID から OID へのマッピングを NDIS に登録する必要があります。 カスタム Oid の登録の詳細については、「カスタマイズされた[oid と状態](customized-oids-and-status-indications.md)の表示」を参照してください。

 

 





