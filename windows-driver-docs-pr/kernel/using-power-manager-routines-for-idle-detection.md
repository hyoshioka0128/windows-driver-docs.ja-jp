---
title: アイドル検出に電源マネージャールーチンを使用する
description: アイドル検出に電源マネージャールーチンを使用する
ms.assetid: 6a89b2eb-d987-4722-b521-9df93153d957
keywords:
- アイドル検出 WDK 電源管理
- PoRegisterDeviceForIdleDetection
- PoSetDeviceBusy
- power manager WDK カーネル
- アイドルタイムアウトの WDK 電源管理
- タイムアウトの WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d11adcb9a98ff1850e07c6ccb407d9f69b93532c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838339"
---
# <a name="using-power-manager-routines-for-idle-detection"></a>アイドル検出に電源マネージャールーチンを使用する





電源マネージャーでは、 [**PoRegisterDeviceForIdleDetection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-poregisterdeviceforidledetection)および[**Posetdevicebusy**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)ルーチンによるアイドル検出がサポートされています。

デバイスのアイドル状態の検出を有効にするために、デバイスの電源ポリシー所有者は**PoRegisterDeviceForIdleDetection**を呼び出し、以下を指定します。

-   システムのパフォーマンスを最適化するときに適用するアイドルタイムアウト値。

-   システムを節約するために最適化するときに適用するアイドルタイムアウト値。

-   アイドル時にデバイスが遷移するデバイスの電源状態。

**PoRegisterDeviceForIdleDetection**は、アイドル状態のカウンターへのポインターを返します。このカウンターは、ドライバーがアイドル状態の検出を無効にするために後で使用します。 **PoRegisterDeviceForIdleDetection**の呼び出し元は、IRQL &lt; ディスパッチ\_レベルで実行されている必要があります。

ドライバーは、デバイスが起動し、デバイスの電源 Irp を処理する準備が整うと、いつでもデバイスをアイドル状態の検出に登録できます。 たとえば、PnP 開始デバイスの IRP の*Iocompletion*ルーチンの一部として、ドライバーによってアイドル検出が有効になる場合があります。

特定のデバイスのタイムアウト値は、デバイスの電力の待機時間に比例し、デバイスの動作の観察に基づいている必要があります。 特定の種類のデバイスの場合、ドライバーは、デバイスクラスの標準の電源ポリシータイムアウトを使用するために、-1 の節約とパフォーマンスのタイムアウト値を指定できます。 詳細については、デバイス固有のドキュメントを参照してください。

デバイスが使用されている場合、ドライバーは[**Posetdevicebusy**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を呼び出して、 **PoRegisterDeviceForIdleDetection**から返されたポインターを渡す必要があります。 **Posetdevicebusy**は、アイドル状態のカウンターをリセットし、デバイスのアイドル状態のカウントダウンを再開します。 ドライバーは、すべての i/o 操作で**Posetdevicebusy**を呼び出す必要があります。

デバイスがアイドル状態であるかどうかを判断するために、電源マネージャーは、現在のシステム電源ポリシー (保護またはパフォーマンス) のために、アイドル状態のカウンターの値とドライバーによって指定されたアイドル状態のタイムアウト値を比較します。 システム電源ポリシーに関連する関数については、Microsoft Windows SDK を参照してください。

デバイスがタイムアウト値を満たすと、電源マネージャーはデバイスセット-電源 IRP を送信します。これは、ドライバーが**PoRegisterDeviceForIdleDetection**への呼び出しで渡したデバイスの電源状態を指定します。 パワーマネージャーは、set-power IRP を送信する前に、クエリの IRP を送信しません。 スタック内のドライバーは、他のものを処理するように、set-power IRP を処理します。これらは、適切なタイミングで完了する必要があり、失敗することはできません。 (「[デバイスの電源を切る irp の処理](handling-device-power-down-irps.md)」を参照してください)。

ドライバーがアイドル状態の検出を必要としなくなった場合、またはデバイスの電源ダウン Irp を処理する準備ができていない場合は、 **PoRegisterDeviceForIdleDetection**を再度呼び出し、両方のタイムアウト値に0を渡す必要があります。 タイムアウトをゼロに設定すると、節約 (バッテリ) とパフォーマンス (AC) の両方の電源ポリシーのアイドル検出が無効になります。 ドライバーは、アイドル状態の検出をすぐに再び有効にすることができます。これは、ゼロ以外のタイムアウト値を使用して**PoRegisterDeviceForIdleDetection**を呼び出すだけです。 デバイスが登録されると、デバイスの電源がオフになっている場合でも、タイムアウト値を変更することでアイドル検出を有効または無効にすることができます。

 

 




