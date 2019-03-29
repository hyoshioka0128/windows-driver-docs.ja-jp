---
title: ミニポート ドライバーの送信および受信操作
description: ミニポート ドライバーの送信および受信操作
ms.assetid: f495cf1f-9896-4259-b885-cff4a0112d17
keywords:
- ミニポート ドライバー WDK ネットワークは、データを送信します。
- NDIS ミニポート ドライバー WDK、データを送信します。
- ミニポート ドライバー WDK ネットワークは、データの受信
- NDIS ミニポート ドライバー WDK、データの受信
- WDK ネットワークのデータを送信します。
- 受信側のデータの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c92a3629e8be996726811e4479b4fab22098d58a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572285"
---
# <a name="miniport-driver-send-and-receive-operations"></a>ミニポート ドライバーの送信および受信操作





ハンドルが重なってドライバーから要求を送信および発信のミニポート ドライバーでは、インジケーターが表示されます。 1 つの関数の呼び出しで NDIS ミニポート ドライバーは、受信した複数のリンクされたリストを指定できます[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。 ミニポート ドライバーが複数のネットワークの一覧については、送信要求を処理できる\_バッファー\_複数のリストの構造体[ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)各ネットワーク上の構造\_バッファー\_リスト構造体。

ミニポート ドライバーを管理する必要があるバッファー プールを受信します。 ほとんどのミニポート ドライバーが事前に割り当てる 1 つの NET するプールを作成\_各 NET でバッファー構造\_バッファー\_リスト構造体。

次のトピックは、ミニポート ドライバー バッファー管理の詳細について説明し、操作を送信、受信操作。

[ミニポート ドライバー バッファー管理](miniport-driver-buffer-management.md)

[ミニポート ドライバーからデータを送信します。](sending-data-from-a-miniport-driver.md)

[ミニポート ドライバーでは、送信要求を取り消す](canceling-a-send-request-in-a-miniport-driver.md)

[ミニポート ドライバーからデータを受信したことを示します](indicating-received-data-from-a-miniport-driver.md)

 

 





