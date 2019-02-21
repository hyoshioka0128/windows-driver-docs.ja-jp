---
title: IRP_MN_QUERY_POWER またはデバイスの電源状態の IRP_MN_SET_POWER を送信します。
description: IRP_MN_QUERY_POWER またはデバイスの電源状態の IRP_MN_SET_POWER を送信します。
ms.assetid: 58f65138-abb9-4bb8-bf9b-14f17347e309
keywords:
- IRP_MN_SET_POWER
- IRP_MN_QUERY_POWER
- デバイスの電源状態の WDK カーネル
- クエリ power Irp WDK の電源管理
- 電源 Irp WDK カーネル、デバイス クエリ
- 電源状態のクエリを実行します。
- キューの Irp
- デバイス クエリ power Irp WDK カーネル
- Irp の電源状態を送信します。
- セット power Irp WDK カーネル
- デバイスが電源 Irp WDK カーネルを設定
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e15f682310e29ca2f3a5392b951f00c2633f5bb7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557053"
---
# <a name="sending-irpmnquerypower-or-irpmnsetpower-for-device-power-states"></a>IRP を送信する\_MN\_クエリ\_電源や IRP\_MN\_設定\_電源状態のデバイスの電源





デバイスの電源ポリシー所有者は、デバイスを送信しますクエリ power IRP ([**IRP\_MN\_クエリ\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff551699)) の変更の下位のドライバーに対応できるかどうかを判断するには。デバイスの電源の状態とデバイスのセット電源 IRP ([**IRP\_MN\_設定\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff551744)) デバイスの電源状態を変更します。 (このドライバーでは、待機/ウェイク IRP がスリープ解除するには、そのデバイスを有効にするのには送信もできます外部からの信号に対して、次を参照してください。[サポート デバイスがあるウェイク アップ機能](supporting-devices-that-have-wake-up-capabilities.md)詳細についてはします。)。

ドライバーを送信する必要があります、 [ **IRP\_MN\_クエリ\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551699)要求、次のいずれかが true の場合。

-   ドライバーがシステムを受け取るクエリ power IRP します。

-   ドライバーは、スリープ状態、下位のドライバーを見つけるかどうかを行うのため不可能にクエリを実行する必要がありますようにアイドル状態のデバイスを配置する準備中です。

ドライバーを送信する必要があります、 [ **IRP\_MN\_設定\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551744)要求時に、次のいずれかが true:

-   ドライバーは、デバイスがアイドル状態で、スリープ状態に配置できることを判断しました。

-   デバイスがスリープ状態と、待機中の I/O を処理する作業の状態を再入力する必要があります。

-   ドライバーがシステムを受信 IRP の出力を設定します。

ドライバーは、独自の電源 IRP; を割り当てる必要がありますされません。電源マネージャーは、提供、 [ **PoRequestPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559734)この目的のために日常的な。 として[Power Irp の処理の規則](rules-for-handling-power-irps.md)説明しますが、 **PoRequestPowerIrp**を割り当てるし、IRP を送信およびと組み合わせて**保留**(Windows 7 および Windows Vista) にまたは**PoCallDriver** (で Windows Server 2003、Windows XP、および Windows 2000)、電源のすべての要求が正しく同期されていることを確認します。 呼び出し元**PoRequestPowerIrp** IRQL で実行する必要があります&lt;= ディスパッチ\_レベル。

このルーチンのプロトタイプを次に示します。

```cpp
NTSTATUS
PoRequestPowerIrp (
    IN PDEVICE_OBJECT DeviceObject,
    IN UCHAR MinorFunction,
    IN POWER_STATE PowerState,
    IN PREQUEST_POWER_COMPLETE CompletionFunction,
    IN PVOID Context,
    OUT PIRP *Irp OPTIONAL
    );
```

IRP がドライバーの呼び出しを送信する**PoRequestPowerIrp**、対象のデバイス オブジェクトへのポインターを指定する*デバイス オブジェクト*、マイナー IRP コード IRP\_MN\_セット\_電源や IRP\_MN\_クエリ\_で電源*MinorFunction*、値**DevicePowerState**で、 <em>PowerState</em>**.型**、およびデバイスの電源状態で<em>PowerState</em>**します。状態**します。 Windows 98/、*デバイス オブジェクト*する必要がありますは、基になるデバイスの PDO を指定して、Windows 2000 および以降のバージョンの Windows では、この値は PDO または同じデバイス スタック内のドライバーの FDO をポイントできます。

電源完了関数へのポインターを渡す必要がある場合は、ドライバーは、その他のすべてのドライバーは IRP を完了した後、追加のタスクを実行する必要があります、 *CompletionFunction*します。 I/O マネージャーの呼び出し、 *CompletionFunction*すべてを呼び出した後、 *IoCompletion* IRP が渡されるときに、ドライバーによって設定ルーチンがスタックをダウンします。

デバイスが送信する必要があります、その後、デバイスの電源ポリシー所有者は IRP デバイス電源クエリを送信するたびに、コールバック ルーチンからセット power IRP (*CompletionFunction*) への呼び出しで、指定されている**PoRequestPowerIrp**します。 クエリが成功した場合、セット power IRP は照会された電源の状態を指定します。 クエリが失敗した場合セット power IRP は現在のデバイスの電源状態を再アサートします。 ドライバーでは、I/O をキュー; クエリへの応答であるため、現在の状態を再アサートすることが重要です。ポリシー所有者は、セット power IRP がキューに登録された I/O 要求の処理を開始するには、そのデバイス スタックのドライバーに通知するを送信する必要があります。

デバイスのポリシーの所有者だけでなくデバイスの電源 IRP を送信しますがデバイス スタックを渡される IRP の処理も留意してください。 このようなドライバーが多くの場合、設定、 *IoCompletion*ルーチン (で[ **IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679)) その IRP 処理コードの一部として、特に、デバイスがの場合電源を投入します。 *IoCompletion*での順序でルーチンを呼び出す*IoCompletion*ルーチンを設定して他のドライバーとの前に、 *CompletionFunction*します。 詳細については、次を参照してください。[デバイス電源 Irp の IoCompletion ルーチン](iocompletion-routines-for-device-power-irps.md)します。

すべてのドライバーが IRP が完了したため、ときに、 *CompletionFunction*が呼び出される、 *CompletionFunction*を呼び出してはならない**保留**、 **PoCallDriver**、または**PoStartNextPowerIrp**出所 IRP にします。 (呼び出すことが、ただし、これらのルーチンのさまざまな電源 IRP。)代わりに、このルーチンは IRP を発生させたドライバーで必要な追加の操作を実行します。 ドライバーは IRP、システムへの応答でデバイス IRP を送信する場合、 *CompletionFunction*システム IRP を完了することがあります。 詳細については、次を参照してください。[電源ポリシー所有者のデバイスでシステム セット Power IRP の処理](handling-a-system-set-power-irp-in-a-device-power-policy-owner.md)します。

呼び出しに応答**PoRequestPowerIrp**、電源マネージャー能力 IRP を割り当て、およびデバイスのデバイス スタックの一番上に送信します。 電源マネージャーは、割り当てられた IRP へのポインターを返します。

エラーが発生しなかった場合**PoRequestPowerIrp**ステータスを返します\_保留します。 この状態は、IRP が正常に送信され、完了待ちの状態を意味します。 電源マネージャーは IRP を割り当てることができませんか、呼び出し元が、無効なマイナー power IRP のコードを指定した場合、呼び出しが失敗します。

デバイスの電源を要求は、デバイスの基になるバス ドライバー、続いて各順次上位ドライバー スタックで、最初に処理する必要があります。 そのため、送信するときに、 **PowerDeviceD0**ドライバーを確認する必要がありますを要求します。 その*CompletionFunction* IRP が完了し、デバイスの電源がオンにした後、必要なタスクを実行します。

デバイスの電源を切るとき (**PowerDeviceD3**)、デバイス スタックでは、各ドライバーが、必要なコンテキストのすべてを保存して、行うために必要なクリーンアップ IRP を次の下位ドライバーに送信する前にする必要があります。 コンテキスト情報とクリーンアップのエクステントは、ドライバーの種類によって異なります。 関数のドライバーがハードウェアのコンテキストを保存する必要があります。フィルター ドライバーは、独自のソフトウェア コンテキストを保存する必要があります。 A *CompletionFunction*セットをこのような状況では、完成した電源、IRP に関連付けられているアクションを実行できますが、ドライバーがデバイスにアクセスできません。

 

 




