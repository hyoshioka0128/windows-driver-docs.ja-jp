---
title: ハードウェア リソースのフレームワーク オブジェクト
description: ハードウェア リソースのフレームワーク オブジェクト
ms.assetid: 64eb628f-ce3d-494b-9fc1-7179a722c5f2
keywords:
- ハードウェア リソース WDK KMDF、framework のオブジェクト
- フレームワークは、WDK KMDF、ハードウェア リソースをオブジェクトします。
- フレームワーク リソース要件リスト オブジェクトの WDK KMDF
- framework リソースの一覧の範囲オブジェクト WDK KMDF
- フレームワーク リソース リスト オブジェクト WDK KMDF
- リソース リスト オブジェクト WDK KMDF
- リソースの一覧の範囲オブジェクト WDK KMDF
- リソース要件のリスト オブジェクト WDK KMDF
- ハードウェア リソースを指定する、WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34a4303c4a0d0e7ef84c9c005952fa12376523fb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384449"
---
# <a name="framework-objects-for-hardware-resources"></a>ハードウェア リソースのフレームワーク オブジェクト


フレームワークには、デバイスのハードウェア リソースを指定するフレームワークとドライバーを使用する次の 3 つオブジェクトを定義します。

<a href="" id="framework-resource-requirements-list-objects"></a>*Framework のリソース要件のリスト オブジェクト*  
各フレームワークのリソース要件のリスト オブジェクトを表す、[リソース要件一覧](https://docs.microsoft.com/windows-hardware/drivers/kernel/hardware-resources)します。 これらのオブジェクトへのハンドルには、WDFIORESREQLIST の型があります。 オブジェクト定義[framework リソース要件の一覧のオブジェクトのメソッドは](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/)します。 リソース要件の一覧は、一連の論理構成で構成されます。

<a href="" id="framework-resource-range-list-objects"></a>*Framework のリソースの一覧の範囲のオブジェクト*  
各フレームワークのリソースの一覧の範囲オブジェクトを表します、[論理構成](https://docs.microsoft.com/windows-hardware/drivers/kernel/hardware-resources#ddk-logical-configurations-kg)(つまり、デバイスが使用できるリソースの範囲のセット) のリソース要件の一覧。 これらのオブジェクトへのハンドルには、WDFIORESLIST の型があります。 オブジェクト定義[framework リソースの一覧の範囲のオブジェクトのメソッドは](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/)します。

<a href="" id="framework-resource-list-objects"></a>*Framework のリソース リスト オブジェクト*  
各フレームワークのリソース リスト オブジェクトで論理構成 (つまり、特定のリソースのセット) を表す、[リソース リスト](https://docs.microsoft.com/windows-hardware/drivers/kernel/hardware-resources)します。 これらのオブジェクトへのハンドルには、WDFCMRESLIST の型があります。 オブジェクト定義[フレームワーク リソース リスト オブジェクトのメソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/)します。

 

 





