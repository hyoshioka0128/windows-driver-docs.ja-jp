---
title: オブジェクトの有効期間の管理
description: オブジェクトの有効期間の管理
ms.assetid: 55ad8133-a70a-462f-87cd-6aeaffb0aec8
keywords:
- UMDF オブジェクト WDK、有効期間
- framework オブジェクト WDK UMDF、有効期間
- WDK UMDF の有効期間
- コールバック オブジェクト WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93901287175746f3104d6cc1b57beccc62fd7400
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371728"
---
# <a name="managing-the-lifetime-of-objects"></a>オブジェクトの有効期間の管理


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

UMDF では、参照カウント スキームを使用して、有効期間を管理する[コールバック オブジェクト](creating-callback-objects.md)と[framework オブジェクト](framework-objects.md)します。

## <a name="managing-references-to-driver-supplied-callback-objects"></a>ドライバーが提供するコールバック オブジェクトへの参照を管理します。


ほとんどの場合、ドライバーとは、コールバック オブジェクトへの参照を保持するために必要ありません。 コールバック オブジェクトのインターフェイスのメソッドはオブジェクトの有効期間は、コールバック オブジェクトとコールバック オブジェクトのペアになっている framework オブジェクトによって異なります。 および、framework によってのみ呼び出されると、ドライバーがの参照を保持する必要はありません。 つまり、ドライバーやフレームワークを安全に呼び出す、オブジェクト階層の上位にあるオブジェクトのインターフェイスのメソッド。

## <a name="managing-references-to-framework-objects"></a>Framework のオブジェクトへの参照を管理します。


UMDF、一般的な COM 有効期間の原則および WDF 固有の有効期間のモデルでは、framework のオブジェクトの有効期間を決定します。 ドライバーは、framework のオブジェクトがメモリから適切なタイミングで解放されるように、両方のモデルの条件を満たす必要があります。

### <a name="com-lifetime-management"></a>COM 有効期間管理

COM では、呼び出し元では、オブジェクトが使用し、呼び出し元が不要になったオブジェクトが必要な参照を解放し、オブジェクトへの参照が通常保持します。 ただし、UMDF ドライバーは、framework オブジェクトへの参照を保持する必要はありません。 実際には、ドライバーは、ドライバーは、framework のオブジェクトを作成した直後に、framework のオブジェクト参照を解放できます。

呼び出すことが後に、UMDF サンプルが、デバイス オブジェクトを解放するなど、 [ **IWDFDriver::CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createdevice)します。 参照が早期にリリースされるが、デバイス オブジェクトは、WDF オブジェクトのツリーへの参照を保持しているために、デバイスが削除されるまでに存在し続けます。

UMDF には、オブジェクト ツリー内のすべてのフレームワーク オブジェクトが追跡しているため、ドライバーが framework のオブジェクトへの参照を保持する必要はありません。

ただしには、ドライバーは、framework オブジェクトへの参照を保持している場合、オブジェクトが必要がなくなったときに、ドライバーは、参照リリースする必要があります。 循環参照は、ドライバーの参照を解放するまでの場所に残ります。 循環参照を避けるためには、ドライバー通常いないにならないように framework オブジェクトを明示的に参照します。

ドライバーのコールバック オブジェクトを実装する必要がありますもドライバーは、framework のオブジェクトへの参照を保持する必要がある場合、 [IObjectCleanup](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iobjectcleanup)インターフェイス。 ドライバーを呼び出すと[ **IWDFObject::DeleteWdfObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject)フレームワーク オブジェクト、framework のオブジェクトを呼び出すその対応するコールバック オブジェクトの[ **IObjectCleanup::OnCleanup** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iobjectcleanup-oncleanup)メソッド。 実装**IObjectCleanup::OnCleanup**ダウン framework オブジェクトの終了処理が完了するためにフレームワークを有効にするフレームワーク オブジェクトへの参照を解放する必要があります。

### <a name="wdf-lifetime-management"></a>WDF の有効期間管理

既定の親をオーバーライドできるようにする型のオブジェクトを作成する場合、オブジェクトの有効期間と一致する有効期間を持つ親を選択する必要があります。 既定の親オブジェクトと、ドライバーが既定の親をオーバーライドできるかどうかの詳細については、内のテーブルを参照してください。 [Framework オブジェクト](framework-objects.md)します。

オブジェクトの有効期間を照合する場合、フレームワークは、親オブジェクトが削除されたときに、オブジェクトを削除します。 明示的に呼び出すことによってオブジェクトを削除することができる場合、オブジェクトの有効期間と一致し、既定の親が削除される前に削除するオブジェクト、 [ **DeleteWdfObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject)オブジェクトがありません不要にします。

たとえば、新しい要求オブジェクトを作成し、呼び出すと[ **IWDFDriver::CreateWdfMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createwdfmemory)この要求のメモリ オブジェクトを作成するには、新しいメモリの親として要求オブジェクトを指定できますオブジェクト。 ドライバーを呼び出す必要はありませんので、WDF は、親オブジェクトが削除されたときに、子オブジェクトを削除、 [ **DeleteWdfObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject)メモリ オブジェクトを削除します。

ただし、その有効期間に近いオブジェクトの有効期間は、親が存在しない場合、既定の親が削除される前に削除するオブジェクトを設定する場合は、明示的な削除を使用する必要があります。 たとえば、ドライバーは、短い期間に使用されるいくつかの要求オブジェクトを作成できます。 ここでは、ドライバーでは、不要になったときに、要求を明示的に削除することによってメモリを節約することができます。

同様に、既定の親をオーバーライドできないオブジェクトを作成して、既定の親が削除される前に削除するオブジェクトの場合、ドライバーする必要があります、オブジェクトを削除に明示的にします。

 

 





