---
title: IEEE 1394 仮想デバイス ドライバーでサポートされる要求
description: IEEE 1394 仮想デバイス ドライバーでサポートされる要求
ms.assetid: 17e0c84b-29d9-461f-a5f6-7677ecb7fb6e
keywords:
- エミュレーション ドライバー WDK IEEE 1394 バス
- ハードウェア エミュレーション ドライバー WDK IEEE 1394 バス
- 仮想デバイス WDK IEEE 1394 バス
- REQUEST_ASYNC_READ
- REQUEST_ASYNC_WRITE
- REQUEST_ASYNC_LOCK
- REQUEST_ALLOCATE_ADDRESS_RANGE
- REQUEST_GET_ADDR_FROM_DEVICE_OBJECT
- REQUEST_SET_DEVICE_XMIT_PROPERTIES
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd135b602fe40d25fff9a9268454543de52439c9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381014"
---
# <a name="supporting-requests-in-ieee-1394-virtual-device-drivers"></a>IEEE 1394 仮想デバイス ドライバーでサポートされる要求





仮想 Pdo と上に読み込まれるドライバーは、実際のハードウェアに、PDO の機能のドライバーが読み込まれている DDI が 1394 バスへのアクセスの同じレベルにあります。 ただし、その仮想ドライバーの場合、実際のハードウェアがないために、1394 バス ドライバーは特殊なケースとして特定の要求を扱う必要があります。 このトピックでは、さまざまな現象が発生する場合は仮想 PDO 宛ての要求について説明します。

-   [**要求\_ASYNC\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff537634)、 [**要求\_ASYNC\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff537636)、および[ **要求\_ASYNC\_ロック**](https://msdn.microsoft.com/library/windows/hardware/ff537633)

    通常、ターゲット デバイスへの非同期 I/O 要求が、アプリケーションやドライバーのアドレスに移動するとき、1394 バス ドライバーは、デバイスの物理デバイス オブジェクト (PDO) のデバイスの拡張機能から、デバイスのノード ID を抽出します。 この情報は、デバイスが列挙されたときに、デバイスの PDO 拡張機能に記録されます。 仮想デバイスは、ただしは、ドライバー、要求を生成するため、通常の方法で列挙*する必要があります*raw モードでの非同期 I/O を実行していた場合と同様に仮想デバイスの場合は、要求を送信するときに、ノード ID を提供します。 Raw モードのアドレス指定の詳細については、次を参照してください。[を送信する非同期 I/O 要求パケットの IEEE 1394 バス](https://docs.microsoft.com/windows-hardware/drivers/ieee/sending-asynchronous-i-o-request-packets-on-the-ieee-1394-bus)します。

    バス ドライバーでは、仮想デバイスの PDO の要求を受信したときに、デバイスの拡張機能からのノード ID を抽出しようとするとするのではなく、要求を生成したドライバーによって提供されるノード ID を使用します。 厳密に言えば、仮想デバイスがないノード Id、ので、仮想デバイスに要求を送信するドライバーは、代わりのノード ID を指定する必要があります。 慣例により、仮想デバイスは、PC のホスト コント ローラーのノード ID を使用します。

    仮想デバイスのドライバーがメモリを割り当てるときは、1394 バスでは、ブロードキャストするすべてのパケットを受信することを指定します。 次に、ドライバーは、受信したすべてのパケットのホスト コント ローラーのノード ID をチェックしてそのパケットを識別します。

    仮想デバイスがないパケットのサイズまたはハードウェア パラメーターであるため、デバイスの拡張機能で記録されるレート情報を転送しないでください。 仮想デバイスの場合は、バス ドライバーは、パケット サイズと転送率の情報、ポートのデバイス オブジェクトに格納されたを使用します。

-   [**要求\_ALLOCATE\_アドレス\_範囲**](https://msdn.microsoft.com/library/windows/hardware/ff537632)

    仮想デバイス用のドライバーがアクセスを設定する必要があります\_フラグ\_型\_フラグのブロードキャスト、 **fulAccessType**の要求を使用してメモリを割り当てるときに IRB メンバー\_ALLOCATE\_アドレス\_範囲の要求。 仮想デバイスには、実際のノード番号があるありません、ため、仮想デバイス用のドライバーにブロードキャスト モードでパケットを受信した場合を除き、要求の受信の手段はあるありません。 複数のノードには、同じアドレス範囲が割り当てられている、1 つだけがその範囲に送られる要求を非同期に表示されます。 仮想デバイスと物理デバイスのドライバーでは、同じアドレス範囲を割り当て、その物理デバイスが優先度を仮想デバイスの場合に物理デバイスがパケットを受信するため。 複数の仮想デバイスと同じアドレス範囲を割り当てる場合、最初に、範囲の割り当てするドライバー、優先されます。

-   [**REQUEST\_GET\_ADDR\_FROM\_DEVICE\_OBJECT**](https://msdn.microsoft.com/library/windows/hardware/ff537641)

    仮想デバイスがある対応するハードウェア ノードがありませんし、独自のノード ID がありません。 仮想デバイス ドライバーは、バス上の物理ノードのノード ID ではなく、この要求を受信したときに、ホスト コント ローラーのノード ID を返します。

-   [**要求\_設定\_デバイス\_XMIT\_プロパティ**](https://msdn.microsoft.com/library/windows/hardware/ff537662)

    ノード ID の取得元の対応するハードウェア ノードがないために、この要求は仮想デバイスのサポートされていません

その他のすべての要求では、仮想および物理デバイス間の動作は同じです。

 

 




