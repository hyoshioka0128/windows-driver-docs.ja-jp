---
title: プロトコル ドライバーの送信および受信操作
description: プロトコル ドライバーの送信および受信操作
ms.assetid: c621d673-167e-41e1-a121-68e0d0bc6f8a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb76d8424590c461c50e2c26551f89344b9c3609
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581324"
---
# <a name="protocol-driver-send-and-receive-operations"></a>プロトコル ドライバーの送信および受信操作





プロトコル ドライバーでは、送信要求を発信し、基になるドライバーの受信の兆候を処理します。 1 つの関数呼び出しでは、NDIS プロトコル ドライバーが複数送信できます[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)複数構造[ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造で各 NET\_バッファー\_リスト構造体。 プロトコル ドライバー受信パスでは、NET の一覧を受信できる\_バッファー\_リストの構造体。

プロトコル ドライバーには、送信するバッファー プールを管理する必要があります。 このようなプールの適切な管理には、システムのパフォーマンスを最適化するために十分なバッファー領域の事前割り当てが必要です。

次のトピックは、プロトコル ドライバー バッファー管理の詳細について説明し、操作を送信、受信操作。

[プロトコル ドライバー バッファー管理](protocol-driver-buffer-management.md)

[プロトコル ドライバーからデータを送信します。](sending-data-from-a-protocol-driver.md)

[プロトコル ドライバーにデータの受信](receiving-data-in-protocol-drivers.md)

 

 





