---
title: クライアントで実装されたシーケンスの処理
description: 省略可能な EvtSpbControllerLock と EvtSpbControllerUnlock イベント コールバック関数では、補完的な操作を実行します。
ms.assetid: C1DED853-059D-481F-A524-E50772072018
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d391105da7f94c485b96594b946d16560ce12987
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550607"
---
# <a name="handling-client-implemented-sequences"></a>クライアントで実装されたシーケンスの処理


省略可能な[ *EvtSpbControllerLock* ](https://msdn.microsoft.com/library/windows/hardware/hh450814)と[ *EvtSpbControllerUnlock* ](https://msdn.microsoft.com/library/windows/hardware/hh450816)イベント コールバック関数を補完的な実行操作です。 *EvtSpbControllerLock*関数は、ハンドラーを[ **IOCTL\_SPB\_ロック\_コント ローラー** ](https://msdn.microsoft.com/library/windows/hardware/hh450858)要求。 *EvtSpbControllerUnlock*関数は、ハンドラーを[ **IOCTL\_SPB\_UNLOCK\_コント ローラー** ](https://msdn.microsoft.com/library/windows/hardware/hh450859)要求。 クライアント (つまり、バス上の周辺機器のデバイスのドライバー) の先頭し、末尾にこれらの要求を送信する[I/O 転送シーケンス](https://msdn.microsoft.com/library/windows/hardware/hh450890)します。 ほとんどの SPB コント ローラー ドライバーがサポートしていません**IOCTL\_SPB\_ロック\_コント ローラー**と**IOCTL\_SPB\_UNLOCK\_コント ローラー**要求と、そのため、実装しない*EvtSpbControllerLock*と*EvtSpbControllerUnlock*関数。

クライアントは、一連の単純な転送要求としての I/O 転送シーケンスを実行できます (つまり、 [ **IRP\_MJ\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff550794)と[ **IRP\_MJ\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff550819)要求)。 シーケンスの最初の転送は続く必要があります、 **IOCTL\_SPB\_ロック\_コント ローラー**要求-この要求に指示 SPB のコント ローラー ドライバー、バスの I/O の中にロックをシーケンスを転送します。 最後の転送は続く必要があります、 **IOCTL\_SPB\_UNLOCK\_コント ローラー**要求は、ドライバー、バスのロックを解除するように指示します。 この種類の I/O 転送シーケンスが呼び出されます、[クライアントで実装されたシーケンス](https://msdn.microsoft.com/library/windows/hardware/hh450890#buses-client-implemented-sequences)から区別するために、[単一要求シーケンス](https://msdn.microsoft.com/library/windows/hardware/hh450890#buses-single-request-sequences)、使用、 [ **IOCTL\_SPB\_EXECUTE\_シーケンス**](https://msdn.microsoft.com/library/windows/hardware/hh450857)要求の代わりに**IOCTL\_SPB\_ロック\_コント ローラー**と**IOCTL\_SPB\_UNLOCK\_コント ローラー**要求。

周辺機器のデバイスのドライバー、バスにロックをかけて、バス コント ローラー、バスのない他の周辺機器へのアクセスを使用できます。 バス ロック操作の詳細については、バスの種類によって異なります。 I²C コント ローラーでは、転送の方向 (読み取り後に、書き込み、またはその逆) に変更を I²C 再起動操作が必要です。 SPI コント ローラーでは、ターゲット デバイスにチップ選択する必要がありますままアサートされたコント ローラーのロックが有効になります。 詳細については、[Bus のアトミック操作](https://msdn.microsoft.com/library/windows/hardware/jj850339)を参照してください。

転送のクライアントで実装されたシーケンスのサポートは、省略可能です。 SPB コント ローラーのドライバーは、コント ローラーは、次の場合にのみ、それらをサポートするために要求する必要があります。

-   クライアントで実装されたシーケンスの実行中には、バスをロックします。
-   いつでも、バスのロックを解除します。 たとえば、バイト転送間隔をロック解除要求が発生した場合、コント ローラーはずバス経由で、[次へ] のバイト転送を待機することがなく、バスのロックを解除します。

バスがロックされている間、クライアントは、単純な転送要求の任意のシーケンスを送信できます。 つまり、シーケンスは任意の長さであることができます、読み取りと書き込みの組み合わせにすることができます。

SPB コント ローラーのドライバーの実装をクライアントで実装されたシーケンスのサポートを示すために、 *EvtSpbControllerUnlock*関数。 SPB フレームワーク拡張機能 (SpbCx) を受け入れる場合は、ドライバーは、この関数を実装、 **IOCTL\_SPB\_ロック\_コント ローラー**と**IOCTL\_SPB\_UNLOCK\_コント ローラー**クライアントからの要求。 それ以外の場合、これらの要求は状態が、それらを実行して失敗 SpbCx\_いない\_サポートされている状態コード。

実装する SPB コント ローラー ドライバー、 *EvtSpbControllerUnlock*関数が実装する必要はありません、 *EvtSpbControllerLock*関数。 ただし、SPB コント ローラーのドライバーを実装する、 *EvtSpbControllerLock*関数を実装する必要がありますも、 *EvtSpbControllerUnlock*関数。

ドライバーが実装されている場合、 *EvtSpbControllerUnlock*機能しない場合は、 *EvtSpbControllerLock*関数、SpbCx を呼び出す、 *EvtSpbControllerUnlock*関数処理**IOCTL\_SPB\_UNLOCK\_コント ローラー**要求しますが、完了するだけです**IOCTL\_SPB\_ロック\_コント ローラー**状態要求\_成功ステータス コード。

ドライバーでは、クライアントで実装されたシーケンスの先頭を検出するために 2 つの方法があります。 ドライバーを実装する場合は、まず、 *EvtSpbControllerLock*関数、SpbCx 呼び出しを処理するには、この関数を**IOCTL\_SPB\_ロック\_コント ローラー**要求クライアント。 この呼び出しのシーケンスの最初の転送要求の前に発生しているドライバーが利用できます。 ドライバーが実装していない場合、2 番目、 *EvtSpbControllerLock*関数の場合、ドライバーが呼び出すことができます、 [ **SpbRequestGetParameters** ](https://msdn.microsoft.com/library/windows/hardware/hh450922)メソッド、ドライバーが処理されるとき、クライアントからの単純な転送要求。 このメソッドは、要求された転送がシーケンス内の最初の転送であることを示す、設定、**位置**メソッドでメンバーの出力を構造体を**SpbRequestSequencePositionFirst**します。

*EvtSpbControllerUnlock*コールバックはシーケンスが終了するか、ドライバーを調べる唯一の方法です。 実装されていないドライバー、 *EvtSpbControllerUnlock*関数は、クライアントで実装されたシーケンスをサポートできません。

 

 




