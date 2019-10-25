---
title: IRP 処理に関するその他のエラー
description: IRP 処理に関するその他のエラー
ms.assetid: fb46e7a8-8181-46d3-a929-cec01fd71f20
keywords:
- 信頼性 WDK カーネル、二重完了した Irp
- 二重完了した Irp WDK カーネル
- 失われた Irp WDK カーネル
- 信頼性 WDK カーネル、損失した Irp
- パブリック IOCTL およびプライベート IOCTL パスの収束
- 信頼性 WDK カーネル、収束パブリックおよびプライベート IOCTL パス
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2eb729f2c45382db9cf20985e0dcba69e003b50f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837249"
---
# <a name="additional-errors-in-handling-irps"></a>IRP 処理に関するその他のエラー





次に、ドライバーが Irp を処理するときに発生する可能性のある追加のエラーを示します。

### <a name="lost-or-double-completed-irps"></a>失われたか、または二重に完了した Irp

これらの問題と、 [**Iostartnextpacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket)などの i/o マネージャールーチンへの呼び出しが不足していると、多くの場合、エラー処理パスで発生します。 ドライバーパスのクイックレビューでは、このような問題を見つけることができます。

### <a name="converging-public-ioctl-and-private-ioctl-paths"></a>パブリック IOCTL およびプライベート IOCTL パスの収束

一般的な規則として、ドライバーには、パブリックおよびプライベート Ioctl (または FSCTLs) 用の個別の実行パスが含まれている必要があります。 ドライバーは、IOCTL または FSCTL 要求が、制御コードを参照することによって、カーネルモードとユーザーモードのどちらであるかを判断できません。 その結果、パブリックコードとプライベートコードの両方を同じ実行パスで処理する (または、最小の検証を実行してから同じルーチンを呼び出す) と、セキュリティ侵害のためにドライバーを開くことができます。 プライベート IOCTL または FSCTL が特権を持っている場合、その制御コードを知っている権限のないユーザーがアクセスできる可能性があります。 したがって、ドライバーがプライベート IOCTL または FSCTL 要求をサポートしている場合は、このような要求をパブリック Ioctl や FSCTLs とは別に処理するようにしてください。

 

 




