---
Description: WpdMultiTransportDriver サンプル
title: WpdMultiTransportDriver サンプル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ddd9d8ca5db775d0985d161f15056c007c2fa5b8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370532"
---
# <a name="the-wpdmultitransportdriver-sample"></a>WpdMultiTransportDriver サンプル


WPD ドライバーのドキュメントのこのセクションでは、WpdMultiTransportDriver、Windows Driver Kit に含まれているサンプルの multitransport ドライバーについて説明します。

トランスポートは、ポータブル デバイスがコンピューターと通信するプロトコルです。 トランスポートの例には、インターネット プロトコル (IP)、Bluetooth、USB などがあります。

さまざまなポータブル デバイスは、複数のトランスポートをサポートします。 たとえば、一部の携帯電話では、Bluetooth と USB の両方をサポートします。

前に Windows 7 では、ユーザーが自分のコンピューターに複数のトランスポートをサポートしているポータブル デバイスを接続されている場合、Windows デバイス マネージャーは表示の各トランスポート – の一意のノード。 複数のデバイスがインストールされていることを示すこの可能性可能性があります。 これを解決するには、Windows 7 では、multitransport ドライバー モデルをサポートしています。 このモデルでは各 multitransport 対応のデバイスの 1 つだけのノードが表示されます。

Multitransport ドライバー スタックは、次の図に示されます。

![ドライバー スタック](images/multi_trans_driver_stack.png)

前の画像では、架空の WPD アプリケーションで (*App.exe*) multitransport と USB または Bluetooth 接続を有効になっている携帯電話間を行き来データを移動できます。 複合 WPD ドライバー (*Wpdcomp.dll*) Microsoft によって提供され、Windows 7 に含まれています。 Multitransport ドライバー (*WpdMultiTranscell.dll*) は架空のベンダーから提供されたドライバーです。

前の画像では、Bluetooth、USB 経由での同時接続を示しています。 一部のドライバー mightimplement この機能。 WpdMultiTransportDriver は、時間の特定の時点ではなく同時) 1 つの接続をサポートします。

このサンプル ドライバーは、WDK に含まれている WpdHelloWorldDriver に基づいています。 このセクションのトピックを確認する前に、知識、 [WpdHelloWorldDriver](the-sample-driver-architecture.md)します。

次の表に、WpdHelloWorldDriver と、WpdMultiTransportDriver 間の主な違いが識別されます。

| リビジョンまたは変更     | 説明                                                                                                                                                                                                                   |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| デバイスの到着         | 機能固有の識別子 (FUID) の特定のデバイスを作成します multitransport オプションを有効に、必要に応じてプラグ アンド プレイ (PnP) の値を設定、および現在のトランスポートの帯域幅の設定に新しい multitransport ドライバー。 |
| 複数のキューのサポート | 新しい multitransport ドライバーでは、2 つの I/O キューをサポートします。 (、WpdHelloWorldDriver には、1 つのキューがサポートしています)。                                                                                                                     |

 

Multitransport ドライバーの機能を確認し、実際のデータ転送の切り替えをテストするをインストールできます、[メディア転送プロトコル移植キット](https://www.microsoft.com/download/details.aspx?id=19153)MTP シミュレーターを使用し、(*MtpSimUi.exe)* アプリケーション。 このアプリケーションを使用すると、Microsoft の MTP ドライバーをインストール、接続またはエミュレートされたデバイスから切断してトランスポートを切り替えます。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[WPD ドライバーのサンプル](the-wpd-driver-samples.md)

 

 





