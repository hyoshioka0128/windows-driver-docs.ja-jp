---
title: 新しいバス ドライバーのインストール
description: 新しいバス ドライバーのインストール
ms.assetid: 449c0c08-c995-4e23-a770-a567bd48966c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66e1c0cc1f2013ac0fb4a18d379d65139040a6b8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828794"
---
# <a name="installing-a-new-bus-driver"></a>新しいバス ドライバーのインストール


新しいベンダーバスドライバーは、バスの種類とデバイス Id を報告するための次のガイドラインに従っている必要があります。また、場合によっては、バス上の子デバイス用に新しい[デバイスセットアップクラス](device-setup-classes.md)を作成します。 これらのガイドラインは、バスとその子デバイスの構成または操作が他のバスと大きく異なる場合に、新しいベンダーバスに適用されます。 このような場合、新しいベンダーバスドライバーでは、次のようにして、バスとその子デバイスが誤って、他のバスおよび子デバイスとグループ化されていないことを確認する必要があります。

1.  バスの種類を識別するには、一意の GUID を使用します。 バスドライバーは、子デバイスの[**IRP_MN_QUERY_BUS_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-bus-information)要求に応答して、子デバイスのバスの種類 (物理デバイスオブジェクト (*PDO*) として表されます) を報告します。 このような要求への応答として、バスドライバーは PNP_BUS_INFORMATION 内の GUID を返す[**PNP_BUS_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_pnp_bus_information)構造体へのポインターを返し**ます。BusTypeGuid**メンバー。 さらに、バスドライバーは PNP_BUS_INFORMATION を設定する必要があり**ます。LegacyBusType** **PNPBus**、 **PNP_BUS_INFORMATION.BusNumber**を適切なカスタム値に設定します。

2.  カスタムハードウェア Id とバスの子デバイスを使用します。

3.  バスの子デバイスが既存の[デバイスセットアップクラス](device-setup-classes.md)に属していない場合は、[バスの子デバイス用の新しいデバイスセットアップクラスをインストール](installing-a-new-device-setup-class-for-a-bus.md)します。

 

 





