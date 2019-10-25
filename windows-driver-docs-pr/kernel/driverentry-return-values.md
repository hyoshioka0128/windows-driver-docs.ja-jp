---
title: DriverEntry の戻り値
description: DriverEntry の戻り値
ms.assetid: 052be2ea-375a-4495-931e-8b66972125a5
keywords:
- DriverEntry WDK カーネル、戻り値
- 戻り値 WDK DriverEntry ルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9e930aa1f57e47e53a904945748d4110bc673e5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838717"
---
# <a name="driverentry-return-values"></a>DriverEntry の戻り値





[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンは、 [NTSTATUS 値](ntstatus-values.md)(状態\_成功または適切なエラー状態) を返します。

**Driverentry**ルーチンは、STATUS\_SUCCESS が返される直前まで、 [**IoRegisterDriverReinitialization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioregisterdriverreinitialization)への呼び出しを延期する必要があります。 この呼び出しを行わないでください。ステータス\_SUCCESS が返される場合を除きます。

**Driverentry**ルーチンが、成功または情報の値ではない NTSTATUS 値 (STATUS\_success など) を返す場合、その**driverentry**ルーチンのドライバーは読み込まれません。

初期化に失敗する**Driverentry**ルーチンは、システムオブジェクト、システムリソース、およびレジストリリソースを解放してから、制御を返す必要があります。 ドライバーがこれらの要求をサポートし**ている場合**は、 [**irp\_MJ\_フラッシュ\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers)および[**irp\_MJ\_SHUTDOWN**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-shutdown)のドライバーオブジェクトにあるドライバーのディスパッチエントリポイントをリセットする必要があります。

ドライバーが初期化に失敗した場合、 **Driverentry**ルーチンも制御を返す前にエラーをログに記録する必要があります。 「[ログエラー](logging-errors.md)」を参照してください。

ドライバーの[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンがエラー状態を返す場合、ドライバーの[*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)ルーチンは呼び出されないことに注意してください。

 

 




