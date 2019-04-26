---
title: リムーバブル デバイス機能で生成されたコンテナー ID
description: リムーバブル デバイス機能で生成されたコンテナー ID
ms.assetid: e09b1ee5-9ccd-428a-8af3-79f138eb07f9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c095c8c503a36b56e3d01ee25b8984e0388d5f63
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344312"
---
# <a name="container-ids-generated-from-the-removable-device-capability"></a>リムーバブル デバイス機能で生成されたコンテナー ID


Windows 7 以降、バス ドライバーは、デバイス ノードのコンテナーの ID を提供できない場合 (*devnode*) の列挙、プラグ アンド プレイ (PnP) マネージャーでは、リムーバブル デバイスの機能を使用して、すべて devnode のコンテナー ID を生成すること物理デバイスの列挙。 バス ドライバーへの応答でリムーバブル デバイスの機能の報告、 [ **IRP_MN_QUERY_CAPABILITIES** ](https://msdn.microsoft.com/library/windows/hardware/ff551664)要求。

このセクションでは、次のトピックについて説明します。

[リムーバブル デバイスの機能の概要](overview-of-the-removable-device-capability.md)

[リムーバブル デバイスの機能からコンテナー Id を生成する方法](how-container-ids-are-generated-from-the-removable-device-capability.md)

 

 





