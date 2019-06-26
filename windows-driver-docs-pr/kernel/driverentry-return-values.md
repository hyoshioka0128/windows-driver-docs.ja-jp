---
title: DriverEntry の戻り値
description: DriverEntry の戻り値
ms.assetid: 052be2ea-375a-4495-931e-8b66972125a5
keywords:
- DriverEntry WDK カーネルでは、戻り値
- WDK DriverEntry ルーチンの戻り値
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 665bc0aa9c21bf9bfc199e914ef91e3365410d3c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384955"
---
# <a name="driverentry-return-values"></a>DriverEntry の戻り値





A [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチンを返します、 [NTSTATUS 値](ntstatus-values.md)、いずれかの状態\_成功またはエラーを適切な状態です。

**DriverEntry**ルーチンへの呼び出しを延期する[ **IoRegisterDriverReinitialization** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioregisterdriverreinitialization)の直前にステータスを返すまで\_成功します。 状態が返されます場合を除き、この呼び出しを行う必要がありますいない、\_成功します。

場合、 **DriverEntry**ルーチンは成功ではない NTSTATUS 値または状態などの情報の値を返します\_成功すると、そのドライバー **DriverEntry**ルーチンが読み込まれていません。

A **DriverEntry**任意のシステム オブジェクト、システム リソース、およびレジストリのリソースが既に設定されているコントロールを返す前に初期化が失敗するルーチンを解放する必要があります。 ドライバーのディスパッチのエントリ ポイントのドライバー オブジェクトをリセットする必要があります[ **IRP\_MJ\_フラッシュ\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers)と[ **IRP\_MJ\_シャット ダウン**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-shutdown)に**NULL**ドライバーは、これらの要求をサポートしている場合。

ドライバーは、初期化に失敗した場合、 **DriverEntry**ルーチンには制御を返す前に、エラーを記録する必要がありますもできます。 します。 参照してください[エラーのログ記録](logging-errors.md)します。

なお、ドライバーの[*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)ルーチンは、ドライバーの場合は呼び出されません[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチンがエラー状態を返します。

 

 




