---
title: ブート構成用のリソース リストの作成
description: ブート構成用のリソース リストの作成
ms.assetid: 8b78cbac-b547-45a1-a49c-f5543bf5ffed
keywords:
- ハードウェア リソース WDK KMDF、ブート構成リソースの一覧
- ブート構成のリソースには、WDK KMDF が一覧表示されます。
- ブート構成リソースの作成の WDK KMDF を一覧表示します。
- リソースには、WDK KMDF が一覧表示されます。
- リソースの作成の WDK KMDF を一覧表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: deacb0e4991178f676d773fd7c201d72d9cb26d2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382405"
---
# <a name="creating-a-resource-list-for-a-boot-configuration"></a>ブート構成用のリソース リストの作成


ドライバーのフレームワーク バス ドライバーでは、デバイスを列挙する後[ *EvtDeviceResourcesQuery* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nc-wdfpdo-evt_wdf_device_resources_query)コールバック関数。 このコールバック関数を空のリソースの一覧を表すリソース リスト オブジェクトを識別するハンドルを受け取ります。 ドライバーは、次を情報をデバイスのブート構成が必要なハードウェア リソースの種類ごとに、一覧に追加するを実行しする必要があります。

1.  ドライバーによって提供される入力[ **CM\_部分\_リソース\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_cm_partial_resource_descriptor)構造体は、特定のリソースの有効な値を指定します。

2.  呼び出す[ **WdfCmResourceListAppendDescriptor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfcmresourcelistappenddescriptor)または[ **WdfCmResourceListInsertDescriptor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfcmresourcelistinsertdescriptor) CMの内容を追加するには\_部分的な\_リソース\_リソース リストに記述子構造体。

ドライバーの後に*EvtDeviceResourcesQuery*コールバック関数が返す、フレームワーク、リソース リストを渡します PnP マネージャー。

デバイスのインストーラーは、追加のリソースの一覧を指定できます。 その他のリソースの一覧の詳細については、次を参照してください。[ハードウェア リソース](https://docs.microsoft.com/windows-hardware/drivers/kernel/hardware-resources)します。

 

 





