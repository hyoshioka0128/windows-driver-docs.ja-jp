---
title: 一般フレームワーク オブジェクトの使用
description: 一般フレームワーク オブジェクトの使用
ms.assetid: d3356d3f-8110-44dd-b4a2-36265f5a1714
keywords:
- フレームワークの WDK KMDF、一般的なオブジェクトします。
- 一般的なフレームワーク オブジェクト WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3e4b147e065be7965a59d2ee52d6005c75e3d56
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372252"
---
# <a name="using-general-framework-objects"></a>一般フレームワーク オブジェクトの使用


*一般的なフレームワーク オブジェクト*オブジェクトを派生する他のタイプのフレームワークからフレームワーク オブジェクトです。

フレームワークの他のオブジェクトのような一般的なオブジェクトをサポートして参照カウントをコンテキストの領域、コールバック関数の削除、および親オブジェクトでは」の説明に従って[Framework オブジェクトの概要](introduction-to-framework-objects.md)します。

ドライバーでは、作成でき、一般的なフレームワーク オブジェクトを使用することができます。 ドライバーを呼び出す場合[ **WdfObjectCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectcreate)ドライバーができる一般的なオブジェクトを作成します。

-   一般的なオブジェクトごとに 1 つまたは複数のコンテキストのスペースを作成します。

    オブジェクト コンテキストの領域を使用すると、一般的なオブジェクトに関連付けるシステム リソースに関する情報を格納します。

    コンテキストの領域に関する詳細については、次を参照してください。[フレームワーク オブジェクト コンテキストの空間](framework-object-context-space.md)します。

-   一般的なオブジェクトの親を割り当てます。

    親オブジェクトが削除されたときに、一般的なオブジェクトが削除されます。 たとえばには、ドライバーは、その一般的なオブジェクトの 1 つの親オブジェクトとして、framework デバイス オブジェクトを指定する場合、デバイス オブジェクトを削除するとき、フレームワークは、一般的なオブジェクト削除されます。

    ドライバーを設定して、オブジェクトの親オブジェクトを指定する、 **ParentObject**オブジェクトのメンバー [ **WDF\_オブジェクト\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/ns-wdfobject-_wdf_object_attributes)構造体。

-   削除コールバック関数を提供します。

    ドライバーが提供できる[ *EvtCleanupCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)と[ *EvtDestroyCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)関数で、システム リソースの割り当てを解除できます一般的なオブジェクトが作成されたときに、ドライバーが割り当てられます。 たとえば、ドライバーと呼ばれる[ **ExAllocatePool** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepool) 、クリーンアップ、一般的なオブジェクトを作成またはコールバック関数を破棄する場合に呼び出すことができます[ **ExFreePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool).

一般的なオブジェクトを使用して、ドライバーに割り当てられたリソースを管理する便利な方法が指定できます。 たとえばより高度なドライバーは、ドライバーは、複数のデバイスに、要求を送信します。 または、いくつかの小さな要求に分割する場合、受信した I/O 要求を処理する複数のメモリ割り当てを必要があります。 ドライバーが受信した I/O 要求の子である 1 つまたは複数の一般的なオブジェクトを作成し、一般的なオブジェクトのコンテキストの領域に、メモリの割り当てに関する情報が格納されることができます。

 

 





