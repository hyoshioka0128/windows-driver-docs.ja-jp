---
title: 多機能デバイス用のリソース マップの作成
description: 多機能デバイス用のリソース マップの作成
ms.assetid: 332eef11-4056-4fe0-87ed-4305c091bab1
keywords:
- WDK 多機能デバイスは、リソース マップします。
- リソース マップ WDK 多機能デバイス
- 子関数のリソースは、WDK をマップします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1392401397dbd09a0df1ece29fedf8e778898fd7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362927"
---
# <a name="creating-resource-maps-for-a-multifunction-device"></a>多機能デバイス用のリソース マップの作成





A*リソース マップ*子関数によって使用されている多機能デバイスのリソースを識別します。 リソース マップを指定する、 [ **INF AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)します。 多機能デバイスには、リソース マップが必要とする場合、デバイスの INF には通常、デバイスの各関数に対して、リソース マップが含まれます。

2 種類のリソース マップ −*標準*リソース マップと*さまざまな*リソース マップします。 このセクションでは、リソース マップを構築する方法について説明し、次のトピックが含まれています。

[標準的なリソースのマップを作成します。](creating-standard-resource-maps.md)

[さまざまなリソース マップの作成](creating-varying-resource-maps.md)

一部の多機能デバイスは、唯一の標準リソース マップを使用して記述できます。 リソース マップでは、さまざまな他のユーザーが必要またはの standard、およびさまざまな組み合わせにマップします。 まだ他のユーザーは必要ありませんリソース マップにします。 参照してください[多機能 PC カード デバイスをサポートしている](supporting-multifunction-pc-card-devices.md)多機能デバイスには、リソース マップが必要な決定をします。

 

 




