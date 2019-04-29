---
title: BUS_INTERFACE_STANDARD を使用してアクセスのメモリ
description: BUS_INTERFACE_STANDARD インターフェイスを使用してアクセス PCMCIA 属性メモリ
ms.assetid: 2696a9ca-38b5-47f2-9639-029bba1173b5
keywords:
- 属性のメモリ バス WDK PCMCIA BUS_INTERFACE_STANDARD インターフェイス
- BUS_INTERFACE_STANDARD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c89c86a41547e892e94ec5452fa7be9ad7a60cd6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391584"
---
# <a name="access-pcmcia-attribute-memory-by-using-a-businterfacestandard-interface"></a>PCMCIA 属性のメモリ バスを使用してへのアクセス\_インターフェイス\_標準インターフェイス





このセクションでは、PC カードまたは CardBus カードのドライバーが、バスを使用する方法について説明します\_インターフェイス\_メモリにアクセスする属性の標準的なインターフェイスです。

ドライバー、バスを使用する必要があります\_インターフェイス\_I/O 要求のオーバーヘッドが許容されない場合、標準的なインターフェイスです。 このメソッドは、バッファーへのポインターを渡すことでは、I/O 要求のメソッドと同様にします。 ただし、このメソッドは、I/O 要求のオーバーヘッドを取り除いてインターフェイス ルーチンを呼び出します。 実行中の IRQL のディスパッチに属性のメモリにアクセスした場合、ドライバーはこのメソッドを使用する必要があります\_レベル − など内遅延プロシージャ呼び出し (DPC)。

ドライバーは、このメソッドを使用して、IRQL での実行中に&lt;= DISPTACH\_レベル。

ドライバーは通常、バスを取得\_インターフェイス\_初期化中に標準的なインターフェイスです。 ドライバーを使用して、 [ **IRP\_MN\_クエリ\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff551687) PCMCIA バス ドライバーからインターフェイスを取得する要求。 IRQL パッシブでインターフェイスのクエリ要求を送信する必要があります\_レベル。

ドライバー インターフェイス ルーチンを呼び出すことができます、ドライバーは、標準バス インターフェイスを取得した後に**GetBusData**または**SetBusData**メモリにアクセスする属性。

 

 





