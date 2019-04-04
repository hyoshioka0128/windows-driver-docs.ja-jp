---
title: Framework オブジェクトのライフ サイクル
description: Framework オブジェクトのライフ サイクル
ms.assetid: 33efc3a8-ac46-4626-ba0f-beb1eaa9ee47
keywords:
- framework オブジェクト WDK KMDF、ライフ サイクル
- WDK KMDF のライフ サイクル
- framework のオブジェクトを作成する、WDK KMDF
- 参照カウントの WDK KMDF
- framework のオブジェクトを削除する、WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31db062268fc2f45dffd6fb0c1889bbbd4308df3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530937"
---
# <a name="framework-object-life-cycle"></a>Framework オブジェクトのライフ サイクル





Framework オブジェクトの「ライフ サイクル」は、削除されるときに、オブジェクトの作成時から時間をまたがっています。 オブジェクトの参照カウント コントロールが削除されるときにします。

### <a name="creating-a-framework-object"></a>Framework オブジェクトを作成します。

ほとんどのフレームワーク オブジェクトは、オブジェクトの作成方法のドライバーの呼び出しによって作成されます。 たとえば、各フレームワーク ドライバーを呼び出す必要があります[ **WdfDriverCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547175)フレームワーク ドライバー オブジェクトを作成します。

その他のフレームワーク オブジェクトは、フレームワークによって作成されます。 たとえば、ユーザーのアプリケーションでのデバイスを開くと読み取りまたは書き込み操作、フレームワークが framework ファイル オブジェクトを作成し、ドライバーに渡します[ *EvtDeviceFileCreate* ](https://msdn.microsoft.com/library/windows/hardware/ff540868)コールバック関数。

いずれか、フレームワークによって、またはドライバーによって、いくつかのフレームワーク オブジェクトを作成できます。 たとえば、I/O マネージャーは、ドライバー、I/O 要求を配信するときにフレームワークはフレームワーク要求オブジェクトを作成しに配信、ドライバーでは、通常、ドライバーの要求ハンドラーの 1 つを呼び出すことによって。 ドライバーは framework 要求オブジェクトを作成し、その他のドライバーに配信できます。

### <a name="using-reference-counts"></a>参照を使用してカウントします。

フレームワークは、各オブジェクトの参照カウントを保持します。 オブジェクトが作成されたときに、フレームワークは、1 つに、参照カウントを設定します。 参照カウントには、0 になると、フレームワークは、オブジェクトを削除します。

ドライバーは、呼び出すことによって、オブジェクトの参照カウントを変更できます[ **WdfObjectReference** ](https://msdn.microsoft.com/library/windows/hardware/ff548758)参照カウントをインクリメントするまたは[ **WdfObjectDereference**](https://msdn.microsoft.com/library/windows/hardware/ff548739)参照カウントをデクリメントします。 (ドライバーが呼び出せる**WdfObjectDereference**が以前に呼び出された場合にのみ**WdfObjectReference**)。

ほとんどの場合、ドライバーはインクリメントまたはオブジェクトの参照カウントをデクリメントする必要はありません。 フレームワーク カウントをインクリメント数を渡す前に、オブジェクトのハンドルと、ドライバーでは、デクリメント、ドライバーが不要になったオブジェクトを必要がある場合。

ドライバー呼び出し[ **WdfObjectReference** ](https://msdn.microsoft.com/library/windows/hardware/ff548758)オブジェクトは削除しないようにする (フレームワークまたはドライバーのスレッドによって) を使用して、ドライバーを完了する前にします。 ドライバーが呼び出す必要があります例ような状況の**WdfObjectReference**と[ **WdfObjectDereference**](https://msdn.microsoft.com/library/windows/hardware/ff548739)を参照してください[送信の取り消しを同期します。要求](synchronizing-cancellation-of-sent-requests.md)します。

### <a name="deleting-a-framework-object"></a>Framework のオブジェクトを削除します。

オブジェクトは、ドライバーを呼び出すため、削除された[ **WdfObjectDelete** ](https://msdn.microsoft.com/library/windows/hardware/ff548734)またはフレームワークは、内部削除ルーチンを呼び出しますが、参照カウントが 0 の場合にのみ、オブジェクトが削除されたためです。 ドライバーやフレームワークは、オブジェクトを削除しようとしましたが、後に、オブジェクトのハンドルの値は、参照カウントがゼロになった後まで有効です。 ドライバー*できません*オブジェクトを呼び出すだけで削除[ **WdfObjectDereference** ](https://msdn.microsoft.com/library/windows/hardware/ff548739) 0 - オブジェクトの参照カウントをデクリメントするドライバー呼び出す必要がありますも**WdfObjectDelete**します。

Framework オブジェクトの親の子オブジェクトである親が削除されている場合は、フレームワークは、親を削除する前に、子オブジェクトを削除しようとします。 オブジェクトの削除は、惑星の親オブジェクトから開始し、オブジェクト階層のルートに向かってを動作します。

ドライバーは、ドライバーやフレームワークがオブジェクトを削除するときにフレームワークから呼び出される次の 2 つのコールバック関数を登録できます。

-   [ *EvtCleanupCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540840)コールバック関数は、フレームワーク、ドライバーを呼び出せるように[ **WdfObjectDereference** ](https://msdn.microsoft.com/library/windows/hardware/ff548739)場合以前と呼ばれていた[ **WdfObjectReference** ](https://msdn.microsoft.com/library/windows/hardware/ff548758)オブジェクトの削除中です。

-   [ *EvtDestroyCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540841)コールバック関数では、フレームワークを呼び出した後、オブジェクトの参照カウントがゼロにデクリメントされています。

これらのコールバック関数のいずれかのオブジェクトが作成されたときに、ドライバーが割り当てられているオブジェクトに固有のリソースの割り当てを解除する必要があります。

フレームワークは、常に、フレームワークの一部のオブジェクトの削除を処理して、ドライバーがこれらのオブジェクトを削除しないでください。 ドライバーを削除できません framework オブジェクトの一覧は、[ **WdfObjectDelete**](https://msdn.microsoft.com/library/windows/hardware/ff548734)を参照してください。

 

 





