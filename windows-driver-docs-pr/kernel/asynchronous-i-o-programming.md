---
title: 非同期 I/O のプログラミング
description: 非同期 I/O のプログラミング
ms.assetid: f50c98ab-3aae-43f6-be91-2ae587105767
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ac4bd2b94be60cfd5021a5a3e568c4bef4f576c4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326058"
---
# <a name="asynchronous-io-programming"></a>非同期 I/O のプログラミング


非同期プログラミングは待機するその他のユーザーを強制しません。 これは、Windows デバイス ドライバーのプログラミング手法をお勧めします。 非同期 I/O をサポートするいると、WDM ドライバーの設計目標の 1 つです。 ドライバーでの非同期 I/O の詳細については、次を参照してください。[非同期 I/O をサポートしている](supporting-asynchronous-i-o.md)します。 デバイス ドライバー、割り込みを使っては非同期的にプログラムする最善の方法です。 デバイスに要求を送信し、システムに制御できるようにだけです。 デバイスが何かを確認したい場合に、ドライバー、割り込みハンドラーを呼び出すことによって、オペレーティング システムを処理する割り込みがトリガーされます。 この通信は Irp によって処理されます。 IRP の詳細については、次を参照してください。 [Irp の処理](handling-irps.md)します。

 

 




