---
title: ブート構成用のリソース リストの作成
description: ブート構成用のリソース リストの作成
ms.assetid: 8b78cbac-b547-45a1-a49c-f5543bf5ffed
keywords:
- ハードウェアリソース WDK KMDF、ブート構成リソースリスト
- ブート構成リソースの一覧 WDK KMDF
- ブート構成リソースの一覧 WDK KMDF, 作成
- リソースリスト WDK KMDF
- リソースリスト WDK KMDF, 作成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e452f7da8fdca658653a26849d0a100fefeb040f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845617"
---
# <a name="creating-a-resource-list-for-a-boot-configuration"></a>ブート構成用のリソース リストの作成


バスドライバーによってデバイスが列挙されると、フレームワークはドライバーの[*EvtDeviceResourcesQuery*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resources_query)コールバック関数を呼び出します。 このコールバック関数は、空のリソースリストを表すリソースリストオブジェクトへのハンドルを受け取ります。 次の手順を実行して、デバイスのブート構成に必要なハードウェアリソースの種類ごとに、情報を一覧に追加する必要があります。

1.  ドライバーが提供した[**CM\_部分\_リソース\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_partial_resource_descriptor)の構造体に入力します。これは、特定のリソースの有効な値を指定します。

2.  [**Wdfcmresourcelistappenddescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfcmresourcelistappenddescriptor)または[**Wdfcmresourcelistappenddescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfcmresourcelistinsertdescriptor)を呼び出して、CM\_部分\_リソース\_記述子構造体の内容をリソースリストに追加します。

ドライバーの*EvtDeviceResourcesQuery* callback 関数がを返すと、フレームワークはリソースリストを PnP マネージャーに渡します。

デバイスインストーラーでは、追加のリソースリストを指定できます。 その他のリソースリストの詳細については、「[ハードウェアリソース](https://docs.microsoft.com/windows-hardware/drivers/kernel/hardware-resources)」を参照してください。

 

 





