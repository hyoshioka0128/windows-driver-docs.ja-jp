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
ms.openlocfilehash: 478e4c7482f5e9109429257ff1a769a648a4ad7b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370882"
---
# <a name="framework-objects-for-hardware-resources"></a>ハードウェア リソースのフレームワーク オブジェクト


フレームワークには、デバイスのハードウェア リソースを指定するフレームワークとドライバーを使用する次の 3 つオブジェクトを定義します。

<a href="" id="framework-resource-requirements-list-objects"></a>*Framework のリソース要件のリスト オブジェクト*  
各フレームワークのリソース要件のリスト オブジェクトを表す、[リソース要件一覧](https://msdn.microsoft.com/library/windows/hardware/ff547012)します。 これらのオブジェクトへのハンドルには、WDFIORESREQLIST の型があります。 オブジェクト定義[framework リソース要件の一覧のオブジェクトのメソッドは](https://msdn.microsoft.com/library/windows/hardware/dn265665)します。 リソース要件の一覧は、一連の論理構成で構成されます。

<a href="" id="framework-resource-range-list-objects"></a>*Framework のリソースの一覧の範囲のオブジェクト*  
各フレームワークのリソースの一覧の範囲オブジェクトを表します、[論理構成](https://msdn.microsoft.com/library/windows/hardware/ff547012#ddk-logical-configurations-kg)(つまり、デバイスが使用できるリソースの範囲のセット) のリソース要件の一覧。 これらのオブジェクトへのハンドルには、WDFIORESLIST の型があります。 オブジェクト定義[framework リソースの一覧の範囲のオブジェクトのメソッドは](https://msdn.microsoft.com/library/windows/hardware/dn265665)します。

<a href="" id="framework-resource-list-objects"></a>*Framework のリソース リスト オブジェクト*  
各フレームワークのリソース リスト オブジェクトで論理構成 (つまり、特定のリソースのセット) を表す、[リソース リスト](https://msdn.microsoft.com/library/windows/hardware/ff547012)します。 これらのオブジェクトへのハンドルには、WDFCMRESLIST の型があります。 オブジェクト定義[フレームワーク リソース リスト オブジェクトのメソッド](https://msdn.microsoft.com/library/windows/hardware/dn265665)します。

 

 





