---
title: アイドル状態検出のための電源マネージャー ルーチンの使用
description: アイドル状態検出のための電源マネージャー ルーチンの使用
ms.assetid: 6a89b2eb-d987-4722-b521-9df93153d957
keywords:
- アイドル状態検出 WDK 電源管理
- PoRegisterDeviceForIdleDetection
- PoSetDeviceBusy
- 電源マネージャー WDK カーネル
- アイドル タイムアウト WDK の電源管理
- タイムアウト WDK の電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c25ae08b4ef5f4b6d5d83b6812816a00bb3830da
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391062"
---
# <a name="using-power-manager-routines-for-idle-detection"></a>アイドル状態検出のための電源マネージャー ルーチンの使用





電源マネージャーからのアイドル状態の検出のサポートを提供する、 [ **PoRegisterDeviceForIdleDetection** ](https://msdn.microsoft.com/library/windows/hardware/ff559721)と[ **PoSetDeviceBusy** ](https://msdn.microsoft.com/library/windows/hardware/ff559755)ルーチン。

デバイスの電源ポリシー所有者の呼び出しをそのデバイスのアイドル状態の検出を有効にする**PoRegisterDeviceForIdleDetection**を指定します。

-   システムのパフォーマンスの最適化時に適用するアイドル状態のタイムアウト値。

-   この活動のシステムを最適化するときに適用するアイドル状態のタイムアウト値。

-   デバイスの電源状態は、デバイスにするアイドル状態のときに移行する必要があります。

**PoRegisterDeviceForIdleDetection**アイドル状態の検出を無効にする新しいドライバー バージョンで使用されるアイドル カウンターへのポインターを返します。 呼び出し元**PoRegisterDeviceForIdleDetection** IRQL で実行する必要があります&lt;ディスパッチ\_レベル。

ドライバーは、アイドル状態、デバイスが起動し、デバイスの電源 Irp を処理する準備ができて、後任意の時点を検出するためには、そのデバイスを登録できます。 たとえば、ドライバーは可能性がありますの一部としてアイドル状態の検出を有効にその*IoCompletion*開始-デバイスの PnP IRP のルーチンです。

どのデバイスに対してタイムアウト値は、デバイスの電源投入待機時間に比例する必要がありますや、監視対象デバイスの動作に基づいています。 特定の種類のデバイスの場合、ドライバーは、デバイス クラスに対する標準的な電源ポリシーのタイムアウトを使用する場合は-1 の節約とパフォーマンスのタイムアウト値を指定できます。 詳細については、デバイスに固有のドキュメントを参照してください。

デバイスが使用して、ドライバーで呼び出す必要があります[ **PoSetDeviceBusy**](https://msdn.microsoft.com/library/windows/hardware/ff559755)、によって返されたポインターを渡す**PoRegisterDeviceForIdleDetection**します。 **PoSetDeviceBusy**デバイスのアイドル状態のカウント ダウンを再起動するため、アイドル状態のカウンターをリセットします。 ドライバーを呼び出す必要があります**PoSetDeviceBusy** I/O 操作のたびにします。

デバイスがアイドル状態かどうかを確認するのには、電源マネージャーは、現在のシステム電源ポリシー (保護またはパフォーマンスのいずれか) のアイドル タイムアウトのドライバーが指定した値でアイドル状態のカウンターの値を比較します。 システム電源ポリシーに関連する関数の Microsoft Windows SDK を参照してください。

デバイスがタイムアウト値を満たすデバイスを電源マネージャー送信しますセット power IRP、デバイスを指定する電源の状態、ドライバーは、呼び出しで渡される**PoRegisterDeviceForIdleDetection**します。 電源マネージャーは、セット power IRP を送信する前に IRP のクエリを送信しません。 他; 処理する際は、スタックのドライバーがセット power IRP を処理します。適切なタイミングで実行する必要あるし、失敗することはできません。 (を参照してください[デバイス電源 Irp の処理](handling-device-power-down-irps.md))。

ときに、ドライバー アイドル状態の検出が必要なくなったデバイスの電源を処理する準備ができていません呼び出す必要がありますの Irp で**PoRegisterDeviceForIdleDetection**ここでも、両方のタイムアウト値に 0 を渡します。 タイムアウトの設定値を 0 に設定すると、(バッテリ使用時) の節約とパフォーマンス (AC) 電源ポリシーの両方のアイドル状態の検出が無効にします。 ドライバーがすばやく; アイドル状態の検出を再度有効にできます。呼び出すだけ**PoRegisterDeviceForIdleDetection** 0 以外のタイムアウト値を使用します。 ドライバーがデバイスを登録すると、有効にし、デバイスが電源を切ると再起動された場合でも、タイムアウトの値を変更することでアイドル状態の検出を無効にできます。

 

 




