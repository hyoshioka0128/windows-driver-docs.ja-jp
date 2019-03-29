---
title: 近接通信プロファイルの実装の詳細
description: 電力効率の高いデザインを実現するためにデバイスの実装は Windows と互換性が維持するために特定の要件に従う必要があります。
ms.assetid: 0FFDF345-EA14-4564-AA8A-7E44E9DB28DA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff3e69acee25b32c106caf504137d3cf78f52af2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578807"
---
# <a name="proximity-profile-implementation-details"></a>近接通信プロファイルの実装の詳細


電力効率の高いデザインを実現するためにデバイスの実装は Windows と互換性が維持するために特定の要件に従う必要があります。

次のサブトピックでは、電源を効率的に使用を有効にすると、接続状態を監視できる手法を説明しますデバイス側の要件を調べます。

## <a name="span-idestablishingaconnectionspanspan-idestablishingaconnectionspanspan-idestablishingaconnectionspanestablishing-a-connection"></a><span id="Establishing_a_Connection"></span><span id="establishing_a_connection"></span><span id="ESTABLISHING_A_CONNECTION"></span>接続を確立します。


アプリケーションの登録済み Windows 8.1 は、デバイスに接続に自動的に GattCharacteristic.ValueChanged イベントのハンドラー。 ただし、近接プロファイルに含まれるサービスの基本的な定義では、任意の indicatable や通知用の特性は含まれません。 デバイスが近接プロファイルに含まれるサービスには、indicatable または通知用の特性を含むサービスを追加できます。 つまりは、近接デバイス indicatable や通知用の少なくとも 1 つの特徴的な値をサポートする必要があります、アプリケーションが自動的に確立されている接続の GattCharacteristic.ValueChanged イベントに少なくとも 1 つのハンドラーを登録する必要があります。

## <a name="span-iddetectinglossofconnectionspanspan-iddetectinglossofconnectionspanspan-iddetectinglossofconnectionspandetecting-loss-of-connection"></a><span id="Detecting_Loss_of_Connection"></span><span id="detecting_loss_of_connection"></span><span id="DETECTING_LOSS_OF_CONNECTION"></span>接続の損失を検出します。


説明したよう[Bluetooth 近接プロファイル](bluetooth-proximity-profile.md)Windows 8.1 の Bluetooth 接続の RSSI 値を公開しません。 その結果、アプリでは、接続パスの損失を計算するのに RSSI 値を使用することはできません。 代わりに、デバイスがリンクの損失に近接してを関連付けることをお勧めします。

## <a name="span-idmonitoringtheconnectionstatespanspan-idmonitoringtheconnectionstatespanspan-idmonitoringtheconnectionstatespanmonitoring-the-connection-state"></a><span id="Monitoring_the_connection_state"></span><span id="monitoring_the_connection_state"></span><span id="MONITORING_THE_CONNECTION_STATE"></span>接続状態の監視


アプリでは、PnpObjectWatcher を使用してデバイスの GATT の接続の状態を監視でき、サービスのデバイス オブジェクトの PnP"Connected"プロパティを監視することができます。 この手法の説明については、 [Bluetooth ジェネリック属性プロファイル - 心拍サービス](https://go.microsoft.com/fwlink/p/?linkid=301978)サンプル。

 

 





