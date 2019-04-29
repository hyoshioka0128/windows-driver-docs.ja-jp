---
title: SerCx I/O の制御要求
description: SerCx をサポートするシリアル I/O 制御要求の一覧。
ms.assetid: 2697096f-73a2-4474-9040-e1cadbb10b1e
keywords:
- SerCx Ioctl
ms.date: 11/30/2017
ms.localizationpriority: medium
ms.openlocfilehash: df64636c9cba08c5927cdd131bb1f096f2716f6f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388019"
---
# <a name="sercx-io-control-requests"></a>SerCx I/O の制御要求

いくつかの例外は、シリアル フレームワークの拡張機能 (SerCx) のバージョン 1 は、Ntddser.h ヘッダー ファイルで定義されている IOCTL_SERIAL_XXX I/O 制御コード (Ioctl) を使用する I/O 制御要求をサポートします。 SerCx がこれらの要求の一部を処理しますが、SerCx はハードウェアに固有の処理が必要なその他の多くの要求を処理するコント ローラーのシリアル ドライバーに依存する必要があります。 SerCx によって処理される要求の一部には、ハードウェア固有の処理も必要です。 SerCx はこれらの要求の完了に必要ですが、SerCx はこれらの要求をコント ローラーのシリアル ドライバーの処理の大部分をオフロードします。

これらの Ioctl のほとんどは、システムが指定した際にドライバー Pc の名前付きのシリアル ポートの管理によってもサポートされます。 際に、Windows のサポートされているすべてのバージョンで使用できます。 シリアル Ioctl の詳細な説明については、次を参照してください。[シリアル デバイスに対する制御要求](serial-device-control-requests2.md)します。

SerCx は、すべての Ioctl Ntddser.h ヘッダー ファイルで定義されていることをサポートしません。 SerCx は古い形式の IOCTL_SERIAL_CONFIG_SIZE の IOCTL は周辺のクライアント ドライバーでは使用できませんをサポートしていません。 IOCTL_SERIAL_RESET_DEVICE IOCTL、STATUS_NOT_IMPLEMENTED エラー ステータス コードで常に SerCx を完了するにはもサポートされていません。 さらに、SerCx Ntddser.h で定義されている IOCTL_SERIAL_INTERNAL_XXX Ioctl のいずれもサポートしていません。

SerCx をサポートする Ioctl の多くは、シリアル ポートで、ハードウェアの設定を構成に使用されます。 シリアル ポートを開いた直後に、クライアントはそのシリアル ポートが未知または不定状態、および既知の既定の状態でない想定してください。 クライアントは、使用できる状態にあるように、シリアル ポートを構成する責任を負います。

ほとんど Ioctl SerCx をサポートするは、シリアル コント ローラー ドライバーによって実装される EvtSerCxControl コールバック関数によって処理されます。 SerCx は 8 個の serial Ioctl EvtSerCxControl 関数を呼び出すことがなく処理します。 ただし、これらの Ioctl の一部を処理する SerCx EvtSerCxControl 以外のコント ローラーのシリアル ドライバーのコールバック関数の支援が必要です。 詳細については、Ioctl SerCx によって処理されるを参照してください。

## <a name="ioctls-handled-by-the-evtsercxcontrol-function"></a>Ioctl EvtSerCxControl 関数によって処理されます。

SerCx をサポートしていない SerCx IOCTL を持つ I/O 制御要求の受信、SerCx は要求を処理するために、コント ローラーのシリアル ドライバーの EvtSerCxControl コールバック関数を呼び出します。 応答として、この関数は、要求を完了する必要があります。 ただし、この関数は、受信したすべての I/O 制御要求を処理しない場合があります。 EvtSerCxControl 関数 IOCTL が認識またはサポートしない場合、STATUS_NOT_IMPLEMENTED エラー状態コードで要求を完了する必要があります。
EvtSerCxControl 関数によって処理された I/O 制御要求の一部は、構成または何らかの方法でシリアル コント ローラーの動作に変更する可能性があります。 エラーを回避するには、周辺機器のデバイス ドライバーは、コント ローラーがまだ保留中の送信を処理中に、コント ローラーを再構成する I/O 制御の要求が送信されないようにする必要があります。 または受信操作。 さらに、この周辺機器のデバイス ドライバーは新しい転送の実行を回避またはシリアル コント ローラー ドライバーが、コント ローラーの構成が変わる可能性がある保留中の I/O 制御要求を完了するまで、操作を受信する必要があります。

通常、SerCx EvtSerCxControl 関数に送信される要求の多くを完了できるこの関数によってが返されます。 要求は、遅延処理を必要とする関数は、要求を完了する DPC ルーチンまたはワーカー スレッドをスケジュールできます。 パフォーマンス上の理由から、関数が、不必要な遅延処理を必要としない操作の DPC ルーチンまたはワーカー スレッドのスケジューリングを避ける必要があります。

SerCx は EvtSerCxControl 関数の呼び出しをシリアル化を試みません。 これらの呼び出しは別のスレッドから同時に発生する可能性し、同時に EvtSerCxControl 関数の 2 つ以上の呼び出しを実行している可能性があります。

## <a name="ioctls-handled-by-sercx"></a>Ioctl SerCx によって処理されます。

SerCx を処理し、シリアル コント ローラー ドライバーからの支援を受けることがなく IOCTL_SERIAL_GET_TIMEOUTS および IOCTL_SERIAL_SET_TIMEOUTS の要求が完了するしますが、SerCx は送信する現在のタイムアウト パラメーターを適用して、受信操作をドライバー実行します。 シリアル コント ローラー ドライバーでは、SerCxGetReadIntervalTimeout メソッドを呼び出して、現在の読み取り間隔タイムアウト値を取得できます。 タイムアウトの詳細については、SERIAL_TIMEOUTS を参照してください。

SerCx は処理し、IOCTL_SERIAL_APPLY_DEFAULT_CONFIGURATION 要求を完了します。 この要求の処理中には、SerCx は、要求の既定の接続設定を使用するシリアル コント ローラーを構成するドライバーの EvtSerCxApplyConfig コールバック関数を呼び出します。 これらの設定は、ACPI のファームウェアをハードウェア プラットフォームからコピーされます。

SerCx は処理し、IOCTL_SERIAL_PURGE 要求を完了します。 このような要求の処理中に SerCx、必要に応じて、受信の削除についての支援、ドライバーの EvtSerCxPurge コールバック関数を呼び出すしたり、保留中のシリアル コント ローラー ドライバーがあります。 操作を送信できます。 現在実装されている、SerCx ハンドルすべてサポートされている EvtSerCxPurge 関数からの支援を受けることがなく操作を削除します。 ただし、SerCx の将来の実装では、新しい種類のパージ操作を実行する EvtSerCxPurge 関数を呼び出すことがあります。

SerCx は処理し、IOCTL_SERIAL_GET_WAIT_MASK、IOCTL_SERIAL_SET_WAIT_MASK、および IOCTL_SERIAL_WAIT_ON_MASK 要求を完了します。 IOCTL_SERIAL_SET_WAIT_MASK 要求の処理中には、SerCx は、シリアル コント ローラー ドライバー待機マスクが変更されたことを通知するドライバーの EvtSerCxWaitmask コールバック関数を呼び出します。 この関数は、新しい待機のマスクを取得する SerCxGetWaitMask メソッドを呼び出します。 後で、この待機マスクで指定されているハードウェア イベントが発生するは、シリアル コント ローラー ドライバーが SerCx に通知する SerCxCompleteWait メソッドを呼び出し、SerCx すべて保留中のイベントを待機している可能性があります IOCTL_SERIAL_WAIT_ON_MASK 要求が完了するとします。 保留中のような要求がない場合、SerCx は今後 IOCTL_SERIAL_WAIT_ON_MASK 要求に応じるためには、その内部のイベント履歴にイベントを格納します。

待機操作が保留中、SerCx は EvtSerCxWaitmask 関数を呼び出すことができます。 新しい待機操作を開始するかどうかを確認するのには、関数は、SerCxGetWaitMask を呼び出します。 SerCxGetWaitMask が 0 以外の場合の待機マスクを返す場合は、この待機のマスクが、古い待機マスクを置き換え、更新された待機のマスクを含む新しい待機操作を開始します。 SerCxGetWaitMask 待機マスクは 0 を返す場合、関数は、待機操作を終了します。 どちらの場合は、関数を呼び出す SerCxCompleteWait。
