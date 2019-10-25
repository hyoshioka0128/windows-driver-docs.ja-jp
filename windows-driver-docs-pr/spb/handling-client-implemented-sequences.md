---
title: クライアント実装シーケンスの処理
description: 省略可能な Evtspbコントローラーと Evtspbコントローラーの Unlock イベントコールバック関数は、補完的な操作を実行します。
ms.assetid: C1DED853-059D-481F-A524-E50772072018
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d731e3217c9c52a52f9148065004beb80e0c3df3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843372"
---
# <a name="handling-client-implemented-sequences"></a>クライアント実装シーケンスの処理


省略可能な[*evtspbコントローラー*](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_lock)と[*evtspbコントローラーの unlock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_unlock)イベントコールバック関数は、補完的な操作を実行します。 *Evtspbcontroller ロック*関数は、 [ **\_コントローラー要求をロック\_、IOCTL\_SPB**](https://msdn.microsoft.com/library/windows/hardware/hh450858)のハンドラーです。 *Evtspbcontroller unlock*関数は、 [ **\_コントローラー要求のロックを解除\_IOCTL\_SPB**](https://msdn.microsoft.com/library/windows/hardware/hh450859)のハンドラーです。 クライアント (つまり、バス上の周辺機器のドライバー) は、これらの要求を開始および終了[i/o 転送シーケンス](https://docs.microsoft.com/windows-hardware/drivers/spb/i-o-transfer-sequences)に送信します。 ほとんどの SPB コントローラードライバーでは、 **\_ロック\_コントローラー**および**ioctl\_SPB**を\_サポートしていません。これは\_コントローラー要求のロックを解除し、そのため、 *evtspbcontroller ロック*を実装しないようにします。*Evtspbコントローラーのロック解除*関数。

クライアントは、一連の単純な転送要求 (つまり、 [**irp\_MJ\_READ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)および[**irp\_MJ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)要求) として i/o 転送シーケンスを実行できます。 シーケンス内の最初の転送は、 **\_コントローラーの要求\_、IOCTL\_spb**が前に置かれている必要があります。この要求は、i/o 転送シーケンスが実行されている間、バスをロックするように spb コントローラードライバーに指示します。 最後の転送の後に**IOCTL\_SPB\_ロック\_解除**する必要があります。これにより、ドライバーはバスのロックを解除するように指示します。 この種類の i/o 転送シーケンスは、 [1 つの要求](https://docs.microsoft.com/windows-hardware/drivers/spb/i-o-transfer-sequences#buses-single-request-sequences)シーケンスと区別するために、[クライアントによって実装](https://docs.microsoft.com/windows-hardware/drivers/spb/i-o-transfer-sequences#buses-client-implemented-sequences)されたシーケンスと呼ばれます。これは ioctl\_SPB を使用して、ioctl ではなく[ **\_シーケンス要求を実行\_** ](https://msdn.microsoft.com/library/windows/hardware/hh450857) **\_SPB\_ロック\_コントローラー**および**IOCTL\_SPB\_\_コントローラー**要求のロックを解除します。

周辺機器のドライバーはバスのロックを保持していますが、バスコントローラーはバス上の他の周辺機器にアクセスすることを許可していません。 バスロック操作の詳細は、バスの種類によって異なります。 I ² C コントローラーの場合、転送方向の変更 (読み取りの後に書き込みを行う、またはその逆) を行うには、I ² C の再起動操作が必要です。 SPI コントローラーの場合は、コントローラーロックが有効なままで、ターゲットデバイスに対するチップ選択をアサートしたままにする必要があります。 詳細については、「 [Atomic Bus の操作](https://docs.microsoft.com/windows-hardware/drivers/spb/atomic-bus-operations)」を参照してください。

クライアントによって実装される転送シーケンスのサポートはオプションです。 SPB コントローラードライバーは、コントローラーが次の操作を実行できる場合にのみ、それらをサポートするように要求する必要があります。

-   クライアントによって実装されたシーケンスの間、バスをロックします。
-   バスのロックをいつでも解除します。 たとえば、バイト転送の間にロック解除要求が発生した場合、コントローラーは、バス上の次のバイト転送を待機せずにバスのロックを解除できる必要があります。

バスがロックされている間、クライアントは任意の順序の単純な転送要求を送信できます。 つまり、シーケンスは任意の長さにすることができ、読み取りと書き込みの任意の組み合わせにすることができます。

クライアントによって実装されたシーケンスのサポートを示すために、SPB コントローラードライバーは*Evtspbcontroller unlock*関数を実装します。 ドライバーがこの関数を実装している場合、SPB フレームワーク拡張機能 (SpbCx) では、クライアントからの\_コントローラーの要求をロック解除\_、\_コントローラーと**ioctl\_spb**の **\_、ioctl\_spb**を受け入れます。 それ以外の場合、SpbCx は、サポートされて\_いない状態コードではなくステータス\_を完了することによって、これらの要求に失敗します。

Evtspbcontroller *unlock*関数を実装する SPB コントローラードライバーは、 *Evtspbcontroller ロック*関数を実装する必要はありません。 ただし、 *evtspbcontroller ロック*関数を実装する SPB コントローラードライバーは、 *Evtspbcontroller unlock*関数も実装する必要があります。

ドライバーで evtspbcontroller *unlock*関数が実装されていても、 *Evtspbcontroller ロック*関数が実装されていない場合、Spbcx は*evtspbcontroller unlock*関数を呼び出して、 **IOCTL\_SPB を処理\_\_コントローラーのロックを解除します。** 要求を行いますが、単に IOCTL\_SPB を完了させるだけで、状態\_成功状態コードの **\_コントローラー要求\_ロック**します。

ドライバーには、クライアントによって実装されたシーケンスの開始を検出する2つの方法があります。 1つ目の方法として、ドライバーが*Evtspbcontroller ロック*関数を実装している場合、SpbCx はこの関数を呼び出して、クライアントからの**ロック\_コントローラー要求\_、IOCTL\_SPB**を処理します。 ドライバーは、シーケンス内の最初の転送要求の前に発生したこの呼び出しに依存することができます。 2番目に、ドライバーが*Evtspbコントローラーロック*関数を実装していない場合、ドライバーは、クライアントからの単純な転送要求を処理するときに、 [**Spbrequestgetparameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbrequestgetparameters)メソッドを呼び出すことができます。 要求された転送がシーケンス内の最初の転送であることを示すために、このメソッドは、メソッドの出力構造体の**Position**メンバーを**最初に Spbrequestsequencepositionfirst**設定します。

*Evtspbコントローラーのロック解除*コールバックは、ドライバーがシーケンスが終了するタイミングを判断する唯一の方法です。 *Evtspbコントローラーロック解除*関数を実装していないドライバーは、クライアントに実装されたシーケンスをサポートできません。

 

 




