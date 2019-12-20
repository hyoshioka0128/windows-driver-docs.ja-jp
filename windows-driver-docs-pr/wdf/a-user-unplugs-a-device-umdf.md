---
title: ユーザーがデバイスを取り外す
description: ユーザーがデバイスを取り外す
ms.assetid: d0c8fd6d-b356-4048-aa97-ebe331d23361
keywords:
- 電源管理のシナリオ WDK UMDF、デバイスの取り外し
- デバイスシナリオの取り外し WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0ffa7cf9423150f26e81593ba97b490000f75ac
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210076"
---
# <a name="a-user-unplugs-a-device"></a>ユーザーがデバイスを取り外す


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

システムが実行されている間、ユーザーは、次の2つの方法のいずれかでデバイスを削除できます。*つまり、デバイス*が削除されようとしていることをシステムに通知します (たとえば、プラグまたは取り出しハードウェアプログラムを使用して)。または、*突然削除*することによって、ユーザーがシステムに通知せずにデバイスを unplugs することになります。 バスで突然の削除 (USB など) がサポートされている場合、デバイスのドライバーはデバイスの突然の消失を処理できる必要があります。

<a href="" id="orderly-removal-------"></a>**正常に削除**   
ユーザーは、デバイスマネージャーを使用してデバイスを無効にするか、ejectable デバイスの取り出しボタンを押すことによって、システムの取り外しまたは取り出しハードウェアプログラムを使用して削除を要求します。 このフレームワークでは、ドライバーが[**IPnpCallback:: OnQueryRemove**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-onqueryremove)コールバック関数を提供し、コールバック関数が削除を拒否していない限り、デバイスを削除または無効にすることができます。

次の図は、一連の UMDF コールバックの電源をオンにして削除する方法を示しています。 シーケンスは、動作中の電源状態 (D0) のデバイスを使用して、図の上部から開始されます。

![umdf ドライバーのデバイスの電源ダウンと正常な削除シーケンス](images/umdf-powerdown-sequence.png)

<a href="" id="surprise-removal-------"></a>**突然の削除**   
このシナリオでは、ユーザーがデバイスを予期せず unplugs しています。 予期しない削除シーケンスでは、UMDF は[**IPnpCallback:: OnSurpriseRemoval**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-onsurpriseremoval)コールバックを呼び出して、デバイスが予期せず削除されたことをドライバーに通知します。 このコールバックは、削除シーケンス内の他のコールバックと共に、特定の順序で発生するとは限りません。

一般に、ドライバーは、削除パス内のハードウェアにアクセスしないようにする必要があります。 ハードウェアへのアクセス試行が無制限に待機すると、リフレクターはタイムアウトします。 次の図は、UMDF ドライバーの予期しない削除シーケンスを示しています。

![umdf ドライバーの予期しない削除順序](images/umdf-surprise-removal-sequence.png)

 

 





