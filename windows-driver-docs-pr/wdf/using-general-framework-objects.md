---
title: 一般フレームワーク オブジェクトの使用
description: 一般フレームワーク オブジェクトの使用
ms.assetid: d3356d3f-8110-44dd-b4a2-36265f5a1714
keywords:
- フレームワークオブジェクト WDK KMDF、全般
- 一般的なフレームワークオブジェクト WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8c2c310b79638b54f20b99ed77456e1af7b29e3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843077"
---
# <a name="using-general-framework-objects"></a>一般フレームワーク オブジェクトの使用


*一般的なフレームワーク*オブジェクトは、他のすべての種類のフレームワークオブジェクトの派生元であるフレームワークオブジェクトです。

他のフレームワークオブジェクトと同様に、一般的なオブジェクトでは、「 [Framework オブジェクトの概要](introduction-to-framework-objects.md)」で説明されているように、参照カウント、コンテキストスペース、削除コールバック関数、および親オブジェクトがサポートされています。

ドライバーは、一般的なフレームワークオブジェクトを作成して使用できます。 ドライバーが[**Wdfobjectcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectcreate)を呼び出して一般的なオブジェクトを作成する場合、ドライバーは次のことができます。

-   一般的なオブジェクトごとに1つまたは複数のコンテキストスペースを作成します。

    オブジェクトコンテキスト領域を使用すると、一般的なオブジェクトに関連付けるシステムリソースに関する情報を格納できます。

    コンテキスト空間の詳細については、「[フレームワークオブジェクトコンテキスト空間](framework-object-context-space.md)」を参照してください。

-   一般オブジェクトに親を割り当てます。

    一般オブジェクトは、親オブジェクトが削除されると削除されます。 たとえば、ドライバーで、一般的なオブジェクトの1つの親オブジェクトとしてフレームワークデバイスオブジェクトを指定した場合、フレームワークは、デバイスオブジェクトを削除するときに、一般的なオブジェクトを削除します。

    ドライバーでオブジェクトの親オブジェクトを指定するには、オブジェクトの[**WDF\_オブジェクト\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)構造体の**ParentObject**メンバーを設定します。

-   削除コールバック関数を指定します。

    ドライバーは、標準オブジェクトの作成時にドライバーによって割り当てられたシステムリソースの割り当てを解除できる[*Evtcleanupcallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)関数と[*evtcleanupcallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)関数を提供できます。 たとえば、ドライバーが汎用オブジェクトを作成したときに[**Exallocatepool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool)という名前の場合、クリーンアップまたは destroy コールバック関数は[**exfreepool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)を呼び出すことができます。

一般的なオブジェクトを使用すると、ドライバーで割り当てられたリソースを簡単に管理できます。 たとえば、高レベルのドライバーでは、受信した i/o 要求を処理するために複数のメモリ割り当てが必要になる場合があります。この場合、ドライバーが複数のデバイスに要求を送信するか、または要求を複数の小さなデバイスに分割します。 ドライバーは、受信 i/o 要求の子である1つまたは複数の一般的なオブジェクトを作成できます。また、メモリ割り当てに関する情報を一般的なオブジェクトのコンテキスト空間に格納できます。

 

 





