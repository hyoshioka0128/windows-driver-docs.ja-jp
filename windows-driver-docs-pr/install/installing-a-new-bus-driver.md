---
title: 新しいバス ドライバーのインストール
description: 新しいバス ドライバーのインストール
ms.assetid: 449c0c08-c995-4e23-a770-a567bd48966c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d4e4207f2d5e97da6c4504b15723bea4a8d3809
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379454"
---
# <a name="installing-a-new-bus-driver"></a>新しいバス ドライバーのインストール


新しいベンダー バス ドライバーはレポート作成、バスの種類とデバイス Id、および、場合によっては、新しいを作成するために、次のガイドラインに準拠する必要があります[デバイス セットアップ クラス](device-setup-classes.md)バス上の子デバイス用です。 次のガイドラインは、構成またはバスとその子デバイスの操作は、他のバスからの大幅に異なる場合に、新しいベンダー バスに適用されます。 ような場合、新しいベンダー バス ドライバーは、バスとその子デバイス誤って、または不適切なグループ分けされていない他のバスや子デバイスとのことを確認するには、次を行う必要があります。

1.  一意の GUID を使用すると、バスの種類を識別します。 バス ドライバー、バスの種類の子デバイスを報告する (物理デバイス オブジェクトとして表されます (*PDO*) への応答、 [ **IRP_MN_QUERY_BUS_INFORMATION** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-bus-information)の要求、子デバイスです。 このような要求に応答してでは、バス ドライバーはへのポインターを返します。 を[ **PNP_BUS_INFORMATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_pnp_bus_information)構造内の GUID を返す、 **PNP_BUS_INFORMATION します。BusTypeGuid**メンバー。 さらに、バス ドライバーを設定する必要があります**PNP_BUS_INFORMATION します。LegacyBusType**に**PNPBus**、および**PNP_BUS_INFORMATION します。BusNumber**に適切なカスタム値。

2.  カスタムのハードウェア Id とバスの子デバイスを使用します。

3.  バスの子デバイス既存に属していないかどうかは[デバイス セットアップ クラス](device-setup-classes.md)、[バスの子デバイスの新しいデバイス セットアップ クラスをインストール](installing-a-new-device-setup-class-for-a-bus.md)します。

 

 





