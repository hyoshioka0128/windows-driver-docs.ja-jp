---
title: サポートされるプロパティ セット
description: サポートされるプロパティ セット
ms.assetid: 49a3e3e6-3a09-4202-a2cb-df65806d3336
keywords:
- .Sys クラスドライバー WDK Windows 2000 カーネル、プロパティセット
- streaming ミニドライバー WDK Windows 2000 カーネル、プロパティセット
- ミニドライバー WDK Windows 2000 カーネルストリーミング、プロパティセット
- プロパティ設定 WDK streaming ミニドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb985211af2c8c20ff484f5f5b78ebe9c58db215
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837663"
---
# <a name="supporting-property-sets"></a>サポートされるプロパティ セット





ミニドライバーと個々のストリームは両方とも、プロパティ要求を受け取ることができます。 ミニドライバーは、 [**HW\_STREAM\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_header)の**devicepropertiesarray**でサポートされるプロパティセットを提供します。 各ストリームは、そのストリームの[**HW\_ストリーム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_information)構造の**streampropertiesarray**でサポートされるプロパティセットを提供します。

ミニドライバーは、 [**Ksk プロパティ\_set**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_set)データ構造体を介して処理されるプロパティセットを定義します。これは、プロパティセット内の各プロパティに対して1つずつ、 [**KSK プロパティ\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_item)構造体の配列を指します。 \_ITEM の**getsupported**メンバーが**TRUE**の場合、ミニドライバーはプロパティデータの取得をサポートしています。 KSK プロパティ\_ITEM の**setsupported**メンバーが**TRUE**の場合、ミニドライバーはプロパティデータの設定をサポートしています。

ほとんどのプロパティサポート要求は、クラスドライバーによって自動的に処理されます。ミニドライバーが提供する情報は、プロパティの KSK プロパティ\_項目構造体で提供されます。 たとえば、クラスドライバーが\_BASICSUPPORT request という種類の KSK プロパティ\_受信した場合、KSK プロパティ\_ITEM の**Values**メンバーのデータ型と値の範囲が検索されます。 詳細については、 [**Ksk プロパティ\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_item)を参照してください。 ミニドライバーがサポート要求のカスタム処理 (まれ) を実行する必要がある場合は、KSK プロパティ\_ITEM の**SupportHandler**メンバーを**TRUE**に設定できます。 次に、クラスドライバーは、サポート要求をプロパティ get 要求であるかのように処理します。 ミニドライバーは、プロパティ識別子の**Flags**メンバーから要求の実際の型を特定できます。

クラスドライバーは、ミニドライバープロパティを取得または設定します。このためには、 [**SRB\_GET\_device\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-device-property)または[**SRB\_設定\_デバイス\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-set-device-property)要求をミニドライバーの[*strminireceivedevicepacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)ルーチンに渡します。 クラスドライバーはストリームのプロパティを取得または設定します。これを行うには、ストリームの**StrMiniReceiveStreamControlPacket**ルーチンにストリーム\_プロパティ要求を設定\_\_プロパティまたは SRB を\_\_ストリームを渡します。\_

クラスドライバーは、ミニドライバーの代わりに多くのプロパティを処理しますが、ミニドライバーからは、ミニドライバーのコールバックの1つを通じて不定期に支援を受けることができます。 ミニドライバーでは、プロパティセットの配列にこれらのプロパティが定義されていません。 クラスドライバーが[Ksk propsetid\_ピン](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-pin)および[kspropsetid\_トポロジ](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-topology)のプロパティセットを処理する方法の詳細については、「[複数のストリームのサポート](supporting-multiple-streams.md)」を参照してください。

 

 




