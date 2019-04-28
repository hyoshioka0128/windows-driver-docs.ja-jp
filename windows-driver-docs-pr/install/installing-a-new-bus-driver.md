---
title: 新しいバス ドライバーのインストール
description: 新しいバス ドライバーのインストール
ms.assetid: 449c0c08-c995-4e23-a770-a567bd48966c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53b58623168024c0eaa228d543b3f64393416cb3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361900"
---
# <a name="installing-a-new-bus-driver"></a>新しいバス ドライバーのインストール


新しいベンダー バス ドライバーはレポート作成、バスの種類とデバイス Id、および、場合によっては、新しいを作成するために、次のガイドラインに準拠する必要があります[デバイス セットアップ クラス](device-setup-classes.md)バス上の子デバイス用です。 次のガイドラインは、構成またはバスとその子デバイスの操作は、他のバスからの大幅に異なる場合に、新しいベンダー バスに適用されます。 ような場合、新しいベンダー バス ドライバーは、バスとその子デバイス誤って、または不適切なグループ分けされていない他のバスや子デバイスとのことを確認するには、次を行う必要があります。

1.  一意の GUID を使用すると、バスの種類を識別します。 バス ドライバー、バスの種類の子デバイスを報告する (物理デバイス オブジェクトとして表されます (*PDO*) への応答、 [ **IRP_MN_QUERY_BUS_INFORMATION** ](https://msdn.microsoft.com/library/windows/hardware/ff551654)の要求、子デバイスです。 このような要求に応答してでは、バス ドライバーはへのポインターを返します。 を[ **PNP_BUS_INFORMATION** ](https://msdn.microsoft.com/library/windows/hardware/ff559608)構造内の GUID を返す、 **PNP_BUS_INFORMATION します。BusTypeGuid**メンバー。 さらに、バス ドライバーを設定する必要があります**PNP_BUS_INFORMATION します。LegacyBusType**に**PNPBus**、および**PNP_BUS_INFORMATION します。BusNumber**に適切なカスタム値。

2.  カスタムのハードウェア Id とバスの子デバイスを使用します。

3.  バスの子デバイス既存に属していないかどうかは[デバイス セットアップ クラス](device-setup-classes.md)、[バスの子デバイスの新しいデバイス セットアップ クラスをインストール](installing-a-new-device-setup-class-for-a-bus.md)します。

 

 





