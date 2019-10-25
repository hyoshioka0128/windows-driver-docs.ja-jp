---
title: パラレル デバイスの読み取りと書き込み
description: パラレル デバイスの読み取りと書き込み
ms.assetid: f28506b1-fa87-4119-a57a-2b49573197d8
keywords:
- 並列デバイス WDK、読み取り
- 並列デバイス WDK、書き込み
- 並列デバイスの読み取り
- 並列デバイスの作成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7bfb5fb9e9c5f55097c1ea0f66b299eb6b8e3347
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845056"
---
# <a name="reading-and-writing-a-parallel-device"></a>パラレル デバイスの読み取りと書き込み





クライアントは、 [**irp\_MJ\_READ**](https://docs.microsoft.com/previous-versions/ff544164(v=vs.85))および[**IRP\_\_MJ の書き込み**](https://docs.microsoft.com/previous-versions/ff544175(v=vs.85))要求を使用して、並列デバイスの読み取りと書き込みを行います。 カーネルモードドライバーは、システムによって提供される[**pparallel\_READ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_read)および[**PPARALLEL\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_write)コールバックルーチンを使用することもできます。 システムによって提供される読み取りコールバックと書き込みコールバックへのポインターを取得するために、カーネルモードドライバーは[**IOCTL\_内部\_parclass\_CONNECT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_parclass_connect)要求を使用します。これにより、 [**PARCLASS\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ns-parallel-_parclass_information)構造体が返されます。 PARCLASS\_情報構造体の**Parallelread**メンバーと**parallelread**メンバーは、コールバックへのポインターです。

クライアントが読み取りと書き込みの i/o 要求を使用する場合、パラレルポートバスドライバーは、並列デバイスのワークキューで要求をキューに入れます。 パラレルデバイスのクライアントは、デバイスの読み取りと書き込みの前にパラレルポートをロックする必要はありません。パラレルポート用のシステム指定のバスドライバーがクライアントのポートを自動的にロックし、ロックを解除するためです。

 

 




