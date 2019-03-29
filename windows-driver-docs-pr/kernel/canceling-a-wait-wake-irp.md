---
title: 待機/ウェイク IRP のキャンセル
description: 待機/ウェイク IRP のキャンセル
ms.assetid: 08e1d11a-91a3-496a-b3ad-f99456e4ce1d
keywords:
- 電源管理の WDK カーネル、ウェイク アップ機能
- 外部ウェイク信号 WDK
- アクティブになるデバイス
- 電源管理のウェイク アップ機能 WDK
- デバイスのスリープ解除 ups WDK 電源管理
- IRP_MN_WAIT_WAKE
- 待機/ウェイク Irp WDK の電源管理のキャンセル
- キャンセル待機/ウェイク Irp
- キャンセル ルーチン、Irp を待ってスリープ解除.
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 930e7d6a365f2cc49c0588909e04062619cd4b40
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573620"
---
# <a name="canceling-a-waitwake-irp"></a>待機/ウェイク IRP のキャンセル





送信待機/ウェイク IRP のドライバーだけでは、その IRP をキャンセルできます。

ドライバーは、保留中待機/ウェイク IRP 次の状況をキャンセルする必要があります。

-   ドライバーが受信、PnP [ **IRP\_MN\_停止\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551755)、 [ **IRP\_MN\_クエリ\_削除\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551705)、 [ **IRP\_MN\_削除\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551738)、または[ **IRP\_MN\_突然\_削除**](https://msdn.microsoft.com/library/windows/hardware/ff551760)デバイスの要求。 ドライバーは IRP 待機/ウェイクを再発行する必要があります ([**PoRequestPowerIrp**](https://msdn.microsoft.com/library/windows/hardware/ff559734))、デバイスが再起動後です。

-   システムがスリープ状態にしようが、デバイスをシステムをスリープ解除を有効にするされません。

    たとえば、USB ハブのドライバーは送信、 **IRP\_MN\_待機\_WAKE**スリープ状態に後でその入力デバイスの 1 つ置かれる場合は、デバイスの起動時に要求します。 システムが稼働状態には、ウェイク信号をデバイスからデバイスを動作状態に戻します (ただし、システムの電源状態に影響を与えません)。 システムがシャット ダウンする準備を行います、システムがスリープ解除するデバイスを許可しない場合、USB ハブのドライバーはこの IRP をキャンセルします。

-   システムが元となるデバイス呼び起こすことはできません、スリープ状態を入力します。 つまりよりも小さいの電源状態が入力、 [ **SystemWake** ](systemwake.md)で指定された値、 [**デバイス\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)構造体。

-   デバイスが応答をウェイク アップ信号できない電源状態を入力します。 つまりより低い電源状態が入力、 [ **DeviceWake** ](devicewake.md)で指定された値、**デバイス\_機能**構造体。

待機/ウェイク IRP、IRP の呼び出しを送信したドライバーをキャンセルする[ **IoCancelIrp**](https://msdn.microsoft.com/library/windows/hardware/ff548338)、ドライバーが呼び出されたときに以前返された IRP にポインターを渡す**PoRequestPowerIrp**.

ドライバーは、待機/ウェイク送信しなかった IRP をキャンセルする必要があります。

### <a href="" id="ddk-cancel-routines-for-wait-wake-irps-kg"></a>待機/ウェイク Irp のルーチンをキャンセルします。

多くの関数とバス ドライバーを設定する必要があります[*キャンセル*](https://msdn.microsoft.com/library/windows/hardware/ff540742)保留中のためのルーチン待機/ウェイク Irp; 次の種類のドライバーは、このようなルーチンを設定する必要があります。

-   ドライバーを有効または無効のウェイク アップにデバイスの設定を変更します。

-   送信ドライバー [ **IRP\_MN\_待機\_WAKE** ](https://msdn.microsoft.com/library/windows/hardware/ff551766)親デバイスのドライバーを要求します。

A [*キャンセル*](https://msdn.microsoft.com/library/windows/hardware/ff540742)ルーチンがそのデバイスのウェイク アップを無効にして、保留中待機/ウェイク IRP に関連するすべてのデータをクリーンアップするドライバーを使用します。 ドライバーの要求を待機/ウェイク Irp の親デバイスにもこれら Irp をキャンセルできます。

その待機/ウェイクで*キャンセル*、日常的なドライバーは、以下の手順を実行する必要があります。

1.  呼び出す[ **IoSetCancelRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549674)をリセットする、*キャンセル*に IRP の日常的な**NULL**します。

2.  呼び出す[ **IoReleaseCancelSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff549550)を渡して、 **CancelIRQL** IRP のキャンセル スピン ロックを解除する IRP で指定します。

3.  デバイスの拡張機能内の関連するフィールドをリセットします。 たとえば、待機/ウェイク IRP が保留中の場合は、ほとんどのドライバーは、フラグを設定し、デバイス拡張機能の IRP にポインターを保持すること。

    このような別の IRP のキャンセル中に、待機/ウェイク IRP を受信するためのドライバーの可能性があるに注意してください。 ドライバーは IRP スピン ロック保護 (またはそれと同等) を既に持っているかどうかを確認する必要があります。 そうである場合、ドライバーは正しい IRP をキャンセルすることを確認するには、その処理を慎重に同期する必要があります。 スピンの使用に関する詳細についてロックの*キャンセル*ルーチンを参照してください[キャンセル Irp](canceling-irps.md)します。

4.  必要なデバイス設定を変更します。 たとえば、モデムのドライバーが、デバイスのスリープ解除設定を無効にすることにします。

5.  設定**Irp -&gt;IoStatus.Status**ステータス\_キャンセルします。

6.  呼び出す[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)待機/ウェイク IRP を完了するには、IO を指定する\_いいえ\_インクリメントします。

7.  場合は、ドライバー、関連する以前要求した**IRP\_MN\_待機\_WAKE**親デバイスの場合、ドライバーがその IRP 内からをキャンセルしますその*キャンセル*。ルーチンです。 ドライバーは、親の IRP をキャンセルする前に、キャンセルのスピン ロックを解放する必要があります。

    たとえばはデバイスのバス ドライバーとして機能し、その親の電源ポリシーのドライバーを所有しているドライバーでは、関連する待機/ウェイクの IRP をその親に送信された以前を取り消す必要があります。 呼び出す[ **IoCancelIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548338)は起動の親の*キャンセル*日常的なデバイス スタックの下位にあります。

 

 




