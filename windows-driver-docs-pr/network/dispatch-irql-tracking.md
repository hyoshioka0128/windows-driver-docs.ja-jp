---
title: ディスパッチ IRQL の追跡
description: ディスパッチ IRQL の追跡
ms.assetid: ac559f4f-0138-4b9a-8f1b-44a2973fd6a1
keywords:
- ディスパッチレベルフラグ WDK ネットワーク
- IRQLs WDK ネットワーク
- ネットワークドライバー WDK、IRQLs
- 現在の IRQLs WDK ネットワーク
- ディスパッチ IRQL 追跡 WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b9b0184b3d69aafadc064ba3fb7666309f42fdf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838137"
---
# <a name="dispatch-irql-tracking"></a>ディスパッチ IRQL の追跡





システムパフォーマンスを向上させるために、一部の NDIS 関数 (たとえば、 [*Miniportsendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)関数) には、現在の IRQL を示すディスパッチレベルフラグが含まれています。 ディスパッチレベルフラグを適切に使用することは、不要な IRQL の設定の試行を回避するのに役立ちます。

他の属性を制御するフラグは他にもありますが、ディスパッチレベルフラグの名前は次のとおりです。

NDIS\_\_のフラグ\_ディスパッチ\_レベルを送信する

NDIS\_\_完全な\_フラグ\_ディスパッチ\_レベルを送信する

NDIS\_\_のフラグ\_ディスパッチ\_レベルを受け取る

NDIS\_\_のフラグ\_ディスパッチ\_レベルを返す

\_ディスパッチ\_レベルでの NDIS\_RWL\_

呼び出し元は、IRQL をテストするのではなく、既知の現在の IRQL からディスパッチレベルフラグの設定を決定する必要があります。 たとえば、ドライバーの設計の特性が固定されているか、ドライバーによって現在の IRQL が保存されているため、IRQL がわかっています。

既知の現在の IRQL がディスパッチ\_レベルの場合、呼び出し元はこのフラグを設定する必要があります。 現在の IRQL が不明である場合、または呼び出し元がディスパッチ\_レベルで実行されていない場合、呼び出し元はこのフラグをクリアする必要があります。 呼び出し元が NDIS の場合、呼び出された関数は、IRQL を変更しないように、このフラグをテストする必要があります。

ドライバーは、ディスパッチレベルフラグの値を決定するために、IRQL をテストしないでください。 テストを行うと、フラグの目的が損なわれます。 必要に応じて、呼び出された関数は単にテスト自体を実行できます。 ドライバーがフラグを設定する必要があるかどうかを判断する方法は、特定のドライバーの設計に残されます。

 

 





