---
title: IRP 処理に関するその他のエラー
description: IRP 処理に関するその他のエラー
ms.assetid: fb46e7a8-8181-46d3-a929-cec01fd71f20
keywords:
- 信頼性の WDK カーネル、Irp の二重完了
- Irp WDK カーネルの二重完了
- 失われた Irp WDK カーネル
- Irp の紛失、信頼性の WDK カーネル
- 収束 IOCTL がパブリックとプライベートの IOCTL パス
- 信頼性 WDK カーネルでは、パブリックおよびプライベートの IOCTL パスを収束します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7a5ab2ebffd9c0dd4b3a9d64f73fbf60e5cf47f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369994"
---
# <a name="additional-errors-in-handling-irps"></a>IRP 処理に関するその他のエラー





ドライバーは Irp を処理するときにも構成するその他のエラーを次に示します。

### <a name="lost-or-double-completed-irps"></a>紛失したまたは double 完了 Irp

I/O マネージャー ルーチンの呼び出しが失われるなどと共に、これらの問題[**います**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartnextpacket)、多くの場合、エラー処理パスで発生します。 ドライバーのパスのクイック レビューでは、このような問題を確認できます。

### <a name="converging-public-ioctl-and-private-ioctl-paths"></a>収束 IOCTL がパブリックとプライベートの IOCTL パス

一般的な規則として、ドライバーはパブリックとプライベートの Ioctl (または FSCTLs) の個別の実行パスを含める必要があります。 ドライバーは、IOCTL かどうかを判断できないまたは FSCTL 要求がカーネル モードまたはユーザー モードで制御コードを調べることで発生します。 その結果、同じ実行パスにおけるパブリックとプライベート両方のコードを処理 (または最低限の検証を実行して、同じルーチンを呼び出す) は、セキュリティ侵害するためのドライバーを開くことができます。 プライベート IOCTL または FSCTL 特権が場合、制御コードを知っている特権のないユーザーはそれにアクセスすることがあります。 そのため、ドライバーは、プライベートの IOCTL または FSCTL 要求をサポートする場合確認パブリック Ioctl または FSCTLs もサポートする必要がありますから個別には、このような要求を処理します。

 

 




