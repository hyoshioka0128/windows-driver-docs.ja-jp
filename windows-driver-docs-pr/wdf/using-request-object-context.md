---
title: 要求オブジェクトのコンテキストの使用
description: 要求オブジェクトのコンテキストの使用
ms.assetid: befb4a22-0640-45e3-890e-6ff17969b017
keywords:
- 要求オブジェクト WDK KMDF、コンテキストスペース
- コンテキスト空間 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7891c2e6d9bbc2f824bb197965ecd8db6019ac79
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842592"
---
# <a name="using-request-object-context"></a>要求オブジェクトのコンテキストの使用





フレームワークによって作成された、またはドライバーによって作成されたすべてのフレームワークの要求オブジェクトに、ドライバー定義のコンテキスト空間を含めることができます。 フレームワークベースのドライバーがフレームワークデバイスオブジェクトを初期化すると、ドライバーは[**Wdfdeviceinitsetrequestattributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetrequestattributes)を呼び出して、デバイスのコンテキスト空間を記述する[**WDF\_オブジェクト\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)構造を指定できます。要求オブジェクト。

フレームワークは、要求オブジェクトのコンテキスト領域を次のように割り当てます。

-   フレームワークは、ドライバーの要求オブジェクトを作成するときに、 **Wdfdeviceinitsetrequestattributes**を呼び出したときに指定されたドライバーのサイズを使用してコンテキスト空間を割り当てます。

-   ドライバーが[**Wdfrequestcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcreate)を呼び出して追加の要求オブジェクトを作成する場合は、WDF\_オブジェクト\_属性構造を指定することによって、コンテキストサイズを指定できます。

フレームワークオブジェクトのコンテキスト空間の割り当てとアクセスの詳細については、「[フレームワークオブジェクトコンテキスト空間](framework-object-context-space.md)」を参照してください。

 

 





