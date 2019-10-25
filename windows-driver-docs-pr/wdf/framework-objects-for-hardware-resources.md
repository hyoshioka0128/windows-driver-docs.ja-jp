---
title: ハードウェア リソースのフレームワーク オブジェクト
description: ハードウェア リソースのフレームワーク オブジェクト
ms.assetid: 64eb628f-ce3d-494b-9fc1-7179a722c5f2
keywords:
- ハードウェアリソース WDK KMDF、フレームワークオブジェクト
- フレームワークオブジェクト WDK KMDF、ハードウェアリソース
- フレームワークリソース-要件リストオブジェクト WDK KMDF
- フレームワークリソース範囲リストオブジェクト WDK KMDF
- フレームワークリソースリストオブジェクト WDK KMDF
- リソースリストオブジェクト WDK KMDF
- リソース範囲リストオブジェクト WDK KMDF
- リソース-必要条件-リストオブジェクト WDK KMDF
- ハードウェアリソース WDK KMDF、指定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c10fa62675b0d58b143492f87be130af23a0ff0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845135"
---
# <a name="framework-objects-for-hardware-resources"></a>ハードウェア リソースのフレームワーク オブジェクト


フレームワークでは、次の3つのオブジェクトが定義されています。これらのオブジェクトは、フレームワークとドライバーがデバイスのハードウェアリソースを指定するために使用します。

<a href="" id="framework-resource-requirements-list-objects"></a>*フレームワークリソース-必要条件-リストオブジェクト*  
各フレームワークリソース要件リストオブジェクトは、[リソース要件の一覧](https://docs.microsoft.com/windows-hardware/drivers/kernel/hardware-resources)を表します。 これらのオブジェクトへのハンドルの型は WDFIORESREQLIST です。 オブジェクトは、[フレームワークリソース要件リストオブジェクトメソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/)を定義します。 リソース要件の一覧は、一連の論理構成で構成されます。

<a href="" id="framework-resource-range-list-objects"></a>*フレームワークリソース範囲リストオブジェクト*  
各フレームワークリソース範囲リストオブジェクトは、リソース要件の一覧で[論理構成](https://docs.microsoft.com/windows-hardware/drivers/kernel/hardware-resources#ddk-logical-configurations-kg)(つまり、デバイスが使用できるリソースの範囲のセット) を表します。 これらのオブジェクトへのハンドルの種類は WDFIORESLIST です。 オブジェクトは、[フレームワークのリソース範囲リストのオブジェクトメソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/)を定義します。

<a href="" id="framework-resource-list-objects"></a>*フレームワークリソースリストオブジェクト*  
各フレームワークリソースリストオブジェクトは、[リソースリスト](https://docs.microsoft.com/windows-hardware/drivers/kernel/hardware-resources)内の論理構成 (つまり、特定のリソースのセット) を表します。 これらのオブジェクトへのハンドルの型は WDFCMRESLIST です。 オブジェクトは、[フレームワークのリソースリストオブジェクトのメソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/)を定義します。

 

 





