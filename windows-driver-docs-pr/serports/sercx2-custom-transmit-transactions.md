---
title: SerCx2 カスタム送信トランザクション
description: シリアル コント ローラーの一部のハードウェアでは、PIO またはシステム DMA 以外シリアル コント ローラーにデータを書き込むためのデータ転送メカニズムを実装できます。
ms.assetid: E72E68BC-A60A-41BE-8606-92A608648042
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 097f850487cb4c26cb5b0b1d162facc9eb840acf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551466"
---
# <a name="sercx2-custom-transmit-transactions"></a>SerCx2 カスタム送信トランザクション


シリアル コント ローラーの一部のハードウェアでは、PIO またはシステム DMA 以外シリアル コント ローラーにデータを書き込むためのデータ転送メカニズムを実装できます。 シリアル コント ローラー ドライバーがサポートできるトランザクションが SerCx2 で使用できるようにこのデータ転送メカニズムをカスタム送信します。

開始する、トランザクションのカスタムの送信、SerCx2 呼び出しのドライバーの[ *EvtSerCx2CustomTransmitTransactionStart* ](https://msdn.microsoft.com/library/windows/hardware/dn265207)イベント コールバック関数の書き込みをパラメーターとして提供し、([ **IRP\_MJ\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff546904)) 要求と、トランザクションの書き込みバッファーの説明。 この呼び出しでは、関数は、トランザクションを開始し、返します。 ドライバーは、トランザクションを完了して、書き込み要求を完了する責任を負います。

## <a name="creating-the-custom-transmit-object"></a>Custom-transmit オブジェクトを作成します。


SerCx2 がコント ローラーのシリアル ドライバーを呼び出す前に*EvtSerCx2CustomTransmitTransaction*Xxx * * 関数の場合、ドライバーが呼び出す必要があります、 [ **SerCx2CustomTransmitTransactionCreate** ](https://msdn.microsoft.com/library/windows/hardware/dn265259) SerCx2 をこれらの関数を登録するメソッド。 このメソッドは、入力パラメーターとしてへのポインターを[ **SERCX2\_カスタム\_送信\_トランザクション\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/dn265321)構造体ドライバーへのポインターを含む*EvtSerCx2CustomTransmitTransaction*Xxx * * 関数。

ドライバーは、次の関数を実装する必要があります。

-   [*EvtSerCx2CustomTransmitTransactionStart*](https://msdn.microsoft.com/library/windows/hardware/dn265207)

オプションとして、ドライバーは、次の関数の一方または両方を実装できます。

-   [*EvtSerCx2CustomTransmitTransactionInitialize*](https://msdn.microsoft.com/library/windows/hardware/dn265206)
-   [*EvtSerCx2CustomTransmitTransactionCleanup*](https://msdn.microsoft.com/library/windows/hardware/dn265205)

**SerCx2CustomTransmitTransactionCreate**メソッド custom-transmit オブジェクトを作成し、呼び出し元のドライバーを提供する[ **SERCX2CUSTOMTRANSMITTRANSACTION** ](https://msdn.microsoft.com/library/windows/hardware/dn265257)このオブジェクトへのハンドルします。 ドライバーの*EvtSerCx2CustomTransmitTransaction*Xxx * * すべての関数は、最初のパラメーターとしてこのハンドルを受け取ります。 次の SerCx2 メソッドは、最初のパラメーターとして、このハンドルを受け取ります。

-   [**SerCx2CustomTransmitTransactionInitializeComplete**](https://msdn.microsoft.com/library/windows/hardware/dn265260)
-   [**SerCx2CustomTransmitTransactionCleanupComplete**](https://msdn.microsoft.com/library/windows/hardware/dn265258)

## <a name="hardware-initialization-and-clean-up"></a>ハードウェアの初期化とクリーンアップ


シリアル コント ローラーのドライバーによっては、シリアル コント ローラーのハードウェアの開始時に初期化する必要があります、カスタムの送信、トランザクションまたはトランザクションの最後に、シリアル コント ローラーのハードウェアの状態をクリーンアップします。

ドライバーが実装されている場合、 [ *EvtSerCx2CustomTransmitTransactionInitialize* ](https://msdn.microsoft.com/library/windows/hardware/dn265206)イベント コールバック関数では、SerCx2 がトランザクションを開始する前に、シリアル コント ローラーを初期化するには、この関数を呼び出す. 実装されている場合、 *EvtSerCx2CustomTransmitTransactionInitialize*関数を呼び出す必要があります、 [ **SerCx2CustomTransmitTransactionInitializeComplete** ](https://msdn.microsoft.com/library/windows/hardware/dn265260)メソッドドライバーでは、シリアル コント ローラーの初期化が完了すると、SerCx2 を通知します。

ドライバーが実装されている場合、 [ *EvtSerCx2CustomTransmitTransactionCleanup* ](https://msdn.microsoft.com/library/windows/hardware/dn265205)イベント コールバック関数、SerCx2 がトランザクションの終了後に、ハードウェアの状態をクリーンアップするには、この関数を呼び出します。 実装されている場合、 *EvtSerCx2CustomTransmitTransactionInitialize*関数を呼び出す必要があります、 [ **SerCx2CustomTransmitTransactionCleanupComplete** ](https://msdn.microsoft.com/library/windows/hardware/dn265258)メソッドドライバーでは、シリアル コント ローラーのクリーンアップが完了すると、SerCx2 を通知します。

## <a name="accessing-the-request-object"></a>要求オブジェクトへのアクセス


開始する、トランザクションのカスタムの送信、SerCx2 呼び出しのドライバーの[ *EvtSerCx2CustomTransmitTransactionStart* ](https://msdn.microsoft.com/library/windows/hardware/dn265207)関数を渡します (、WDFREQUEST でカプセル化された関連付けられている書き込み要求オブジェクトのハンドル) をパラメーターとしてこの関数にします。 ドライバーは、メソッドの呼び出しを担当[ **WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945)トランザクションが完了すると、この要求を完了します。 要求を完了しない限り、すぐに、前に、 *EvtSerCx2CustomTransmitTransactionStart*関数を返します、ドライバーはなどのメソッドを呼び出す必要があります[ **WdfRequestMarkCancelableEx**](https://msdn.microsoft.com/library/windows/hardware/ff549984)要求をキャンセル可能としてマークします。

シリアル コント ローラー ドライバーがなど、メソッドを使用しない必要があります[ **WdfRequestRetrieveInputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550014)書き込み要求のデータ バッファーにアクセスします。 代わりに、ドライバーを使用する必要があります、 *Mdl*、*オフセット*、および*長さ*に渡されるパラメーター値、 *EvtSerCx2CustomTransmitTransactionStart*このバッファーにアクセスする関数。

中に、トランザクションのカスタムの送信、ドライバーは、要求オブジェクトに関連付けられているコンテキストに、トランザクションに関する情報を格納する必要があります。 そうである場合、ドライバーの[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)イベント コールバック関数を呼び出すことができます、 [ **WdfDeviceInitSetRequestAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff546786)メソッド要求オブジェクトに使用する属性を設定します。 これらの属性には、要求コンテキストを使用する名前と割り当てのサイズが含まれます。 この呼び出しで指定された要求属性は、ドライバーをへの呼び出しで指定する要求属性に一致する必要があります、 [ **SerCx2InitializeDevice** ](https://msdn.microsoft.com/library/windows/hardware/dn265261)メソッド。 これらの属性がで指定された、 **RequestAttributes**のメンバー、 **SERCX2\_CONFIG**ドライバーに渡します構造**SerCx2InitializeDevice**. 詳細については、[ **SERCX2\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/dn265310)を参照してください。

書き込み要求の開始時シリアル コント ローラーのドライバーを受信するため、トランザクションのカスタムの送信、ドライバー、フレームワークによって割り当てられている要求コンテキストが初期化されていません。 ドライバー呼び出す必要があります、ベスト プラクティスとして、 [ **RtlZeroMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff563610)ルーチンをすべてゼロには、この要求コンテキストを初期化します。

 

 




