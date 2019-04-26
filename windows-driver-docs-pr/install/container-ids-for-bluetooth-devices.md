---
title: Bluetooth デバイス用のコンテナー ID
description: Bluetooth デバイス用のコンテナー ID
ms.assetid: 7e9c40d9-ed19-4ad2-a749-6e3f4aaca2de
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ab6ed16e6bfb88af6a342e73d352c3ed6c4efdd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346814"
---
# <a name="container-ids-for-bluetooth-devices"></a>Bluetooth デバイス用のコンテナー ID


コンピューターに接続されている Bluetooth デバイスの場合、デバイスのメディア アクセス制御 (MAC) アドレスを使用してデバイスのコンテナー ID を生成します。

Bluetooth のバス ドライバーは、デバイスの一意のコンテナー ID を生成するのにシード値としての MAC アドレスを使用します。 このコンテナーの Bluetooth デバイスの各ノードの Bluetooth バス ドライバーによって ID が指定された (*devnode*) 物理デバイスを列挙します。

Bluetooth デバイスは、頻繁に特定の Bluetooth サービスを実装します。 これらのサービスでは、Windows PnP デバイスとしてインストールされていないと、そのため、関連付けられている devnode はありません。 ただし、特定の機能を提供し、Bluetooth デバイスと通信できるようにするために、これらのサービスは、効果的に機能するデバイスのインスタンスです。

Windows 7 以降のオペレーティング システムが機能するデバイスのインターフェイスであると Bluetooth サービスを考慮し、デバイスの Bluetooth devnode と共にこれらのサービスをグループ化します。

すべての Bluetooth デバイスには、MAC アドレスを含める必要があります。 したがって、Bluetooth devnode とサービスのコンテナー ID は常に、MAC アドレスの値に基づきます。 USB デバイスとは異なり Bluetooth デバイスのコンテナー Id を生成するリムーバブル デバイスの機能は使用されません。

一意のコンテナーのすべてのデバイスの ID を生成するように、Bluetooth デバイスの開発者は、一意の MAC アドレスを各デバイスを構成する必要があります。

 

 





