---
title: 要求オブジェクトのコンテキストの使用
description: 要求オブジェクトのコンテキストの使用
ms.assetid: befb4a22-0640-45e3-890e-6ff17969b017
keywords:
- 要求オブジェクト WDK KMDF、コンテキストの領域
- コンテキスト領域 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a70ef85a9c1de9119e7e7ec5f405ce0e9149bfbf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372216"
---
# <a name="using-request-object-context"></a>要求オブジェクトのコンテキストの使用





すべての framework 要求オブジェクト、または、ドライバー、フレームワークによって作成されたかどうかがドライバーによって定義されたコンテキストの領域を含めることができます。 フレームワーク ベースのドライバーでは、framework デバイス オブジェクトを初期化します、ドライバーを呼び出して[ **WdfDeviceInitSetRequestAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetrequestattributes)を指定する、 [ **WDF\_オブジェクト\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/ns-wdfobject-_wdf_object_attributes)コンテキスト場所、デバイスの要求オブジェクトを記述する構造体。

フレームワークは、次のように、要求オブジェクトのコンテキストの領域を割り当てます。

-   ドライバーは、呼び出されたときに指定されたサイズとコンテキストの領域を割り当てますフレームワークでは、ドライバーの要求オブジェクトを作成するときに**WdfDeviceInitSetRequestAttributes**します。

-   ドライバーは、呼び出すことによって追加の要求オブジェクトを作成する場合[ **WdfRequestCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcreate)、コンテキストのサイズを指定するには、WDF を提供することで\_オブジェクト\_属性の構造体。

詳細については、framework のオブジェクトのコンテキストの領域へのアクセスの割り当てとは、次を参照してください。[フレームワーク オブジェクト コンテキストの空間](framework-object-context-space.md)します。

 

 





