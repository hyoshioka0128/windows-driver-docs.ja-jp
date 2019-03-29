---
title: 停止 IRP の処理 (Windows 2000 以降)
description: 停止 IRP の処理 (Windows 2000 以降)
ms.assetid: 5148ca15-07f0-4a93-aa65-45b13184184b
keywords:
- Irp WDK PnP 停止します。
- WDK PnP Irp
- I/O 要求パケット PnP WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76f3e916fb18ec21eadfc22b1e179c85524384a9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570402"
---
# <a name="handling-stop-irps-windows-2000-and-later"></a>停止 IRP の処理 (Windows 2000 以降)





ドライバーを Windows 2000 および以降のバージョンの Windows のみを実行する (WDM バージョン 0x10 以降) が表示される PnP マネージャーがリソースを再配分ときにのみ、Irp を停止します。 次のセクションには、処理の停止の Irp でこのようなドライバーを使用する必要がありますの手法について説明します。

[IRP の処理\_MN\_クエリ\_停止\_デバイス (Windows 2000 以降) を要求します。](handling-an-irp-mn-query-stop-device-request--windows-2000-and-later-.md)

[IRP の処理\_MN\_停止\_デバイス (Windows 2000 以降) を要求します。](handling-an-irp-mn-stop-device-request--windows-2000-and-later-.md)

[IRP の処理\_MN\_キャンセル\_停止\_デバイス (Windows 2000 以降) を要求します。](handling-an-irp-mn-cancel-stop-device-request--windows-2000-and-later-.md)

[デバイスが一時停止すると、着信 Irp を保持しています。](holding-incoming-irps-when-a-device-is-paused.md)

WDM ドライバーも上で実行される Windows 98/Me 異なる方法でこれらの Irp を処理する必要があります。 参照してください[停止 Irp の処理 (Windows 98/Me)](handling-stop-irps--windows-98-me-.md)詳細についてはします。

 

 




