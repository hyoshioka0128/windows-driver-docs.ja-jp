---
title: オブジェクトの有効期間の管理
description: オブジェクトの有効期間の管理
ms.assetid: 55ad8133-a70a-462f-87cd-6aeaffb0aec8
keywords:
- UMDF オブジェクト WDK、有効期間
- フレームワークオブジェクト WDK UMDF、有効期間
- 有効期間 WDK UMDF
- コールバックオブジェクト WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce73d2aaf8a156471d2d89d5642445c70a3cba28
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210770"
---
# <a name="managing-the-lifetime-of-objects"></a>オブジェクトの有効期間の管理


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

UMDF は、参照カウントスキームを使用して、[コールバックオブジェクト](creating-callback-objects.md)と[フレームワークオブジェクト](framework-objects.md)の有効期間を管理します。

## <a name="managing-references-to-driver-supplied-callback-objects"></a>ドライバーによって提供されるコールバックオブジェクトへの参照の管理


ほとんどの場合、コールバックオブジェクトへの参照を保持するためにドライバーは必要ありません。 コールバックオブジェクトインターフェイスのメソッドが、フレームワークおよびその有効期間がコールバックオブジェクトと対になるフレームワークオブジェクトに依存するオブジェクトによってのみ呼び出される場合、ドライバーは参照を保持する必要はありません。 つまり、ドライバーまたはフレームワークは、オブジェクト階層の上位にあるオブジェクトインターフェイスのメソッドを安全に呼び出すことができます。

## <a name="managing-references-to-framework-objects"></a>フレームワークオブジェクトへの参照の管理


UMDF では、一般的な COM 有効期間の原則と WDF 固有の有効期間モデルによって、フレームワークオブジェクトの有効期間が決まります。 適切なタイミングでフレームワークオブジェクトがメモリから解放されるように、ドライバーは両方のモデルの条件を満たす必要があります。

### <a name="com-lifetime-management"></a>COM の有効期間の管理

COM では、通常、オブジェクトが使用されている間は呼び出し元がオブジェクトへの参照を保持し、次にオブジェクトが不要になったときに呼び出し元が参照を解放します。 ただし、UMDF ドライバーは、フレームワークオブジェクトへの参照を保持する必要はありません。 実際、ドライバーは、フレームワークオブジェクトを作成した直後にフレームワークオブジェクト参照を解放できます。

たとえば、UMDF samples は[**Iwdfdriver:: CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)を呼び出した後にデバイスオブジェクトを解放します。 参照は早期にリリースされますが、WDF オブジェクトツリーが参照を保持しているため、デバイスが削除されるまで、デバイスオブジェクトは引き続き存在します。

UMDF はオブジェクトツリー内のすべてのフレームワークオブジェクトを追跡するので、ドライバーはフレームワークオブジェクトへの参照を保持する必要はありません。

ただし、ドライバーがフレームワークオブジェクトへの参照を保持している場合、ドライバーは、オブジェクトが不要になったときに参照を解放する必要があります。 循環参照は、ドライバーがその参照を解放するまで保持されます。 循環参照を回避するには、通常、ドライバーはフレームワークオブジェクトへの明示的な参照を保持しないようにする必要があります。

ドライバーがフレームワークオブジェクトへの参照を保持する必要がある場合、ドライバーのコールバックオブジェクトも[IObjectCleanup](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iobjectcleanup)インターフェイスを実装する必要があります。 ドライバーが[**Iwdfobject:**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject) framework オブジェクトの:D eletewdfobject を呼び出すと、フレームワークオブジェクトは対応するコールバックオブジェクトの[**IObjectCleanup:: oncleanup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iobjectcleanup-oncleanup)メソッドを呼び出します。 フレームワークオブジェクトの破棄を完了するには、 **IObjectCleanup:: OnCleanup**の実装でフレームワークオブジェクトへの参照を解放する必要があります。

### <a name="wdf-lifetime-management"></a>WDF の有効期間管理

既定の親をオーバーライドできる型のオブジェクトを作成する場合は、有効期間がオブジェクトの有効期間に一致する親を選択する必要があります。 既定の親オブジェクトと、ドライバーが既定の親をオーバーライドできる場合の詳細については、「[フレームワークオブジェクト](framework-objects.md)」の表を参照してください。

オブジェクトの有効期間を一致させると、親オブジェクトが削除されたときに、フレームワークによってオブジェクトが削除されます。 オブジェクトの有効期間を一致させず、既定の親を削除する前にオブジェクトを削除する場合は、オブジェクトが不要になったときに[**Deletewdfobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject)を呼び出すことによって、オブジェクトを明示的に削除できます。

たとえば、新しい要求オブジェクトを作成し、 [**Iwdfdriver:: CreateWdfMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createwdfmemory)を呼び出してこの要求のメモリオブジェクトを作成する場合、要求オブジェクトを新しいメモリオブジェクトの親として指定できます。 WDF は親オブジェクトが削除されたときに子オブジェクトを削除するため、ドライバーは、メモリオブジェクトを削除するために[**Deletewdfobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject)を呼び出す必要はありません。

ただし、有効期間がオブジェクトの有効期間と密接に一致する親がなく、既定の親を削除する前にオブジェクトを削除する場合は、明示的な削除を使用する必要があります。 たとえば、ドライバーは、短時間に使用されるいくつかの要求オブジェクトを作成できます。 この場合、ドライバーは不要になった要求を明示的に削除することで、メモリを節約できます。

同様に、既定の親をオーバーライドすることを許可しないオブジェクトを作成し、既定の親を削除する前にオブジェクトを削除する場合、ドライバーはオブジェクトを明示的に削除する必要があります。

 

 





