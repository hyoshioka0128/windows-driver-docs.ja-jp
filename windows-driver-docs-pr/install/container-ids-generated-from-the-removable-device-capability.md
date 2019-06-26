---
title: リムーバブル デバイス機能で生成されたコンテナー ID
description: リムーバブル デバイス機能で生成されたコンテナー ID
ms.assetid: e09b1ee5-9ccd-428a-8af3-79f138eb07f9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d772fd196b76770b950e42b654348709da02ec3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365469"
---
# <a name="container-ids-generated-from-the-removable-device-capability"></a>リムーバブル デバイス機能で生成されたコンテナー ID


Windows 7 以降、バス ドライバーは、デバイス ノードのコンテナーの ID を提供できない場合 (*devnode*) の列挙、プラグ アンド プレイ (PnP) マネージャーでは、リムーバブル デバイスの機能を使用して、すべて devnode のコンテナー ID を生成すること物理デバイスの列挙。 バス ドライバーへの応答でリムーバブル デバイスの機能の報告、 [ **IRP_MN_QUERY_CAPABILITIES** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)要求。

このセクションでは、次のトピックについて説明します。

[リムーバブル デバイスの機能の概要](overview-of-the-removable-device-capability.md)

[リムーバブル デバイスの機能からコンテナー Id を生成する方法](how-container-ids-are-generated-from-the-removable-device-capability.md)

 

 





