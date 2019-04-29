---
title: ネットワーク モジュールのアタッチ
description: ネットワーク モジュールのアタッチ
ms.assetid: 4b3602dd-a9cf-4cb6-bfeb-d2d74d2f391d
keywords:
- ネットワーク モジュール WDK ネットワーク モジュールの登録、添付ファイル
- プロバイダー モジュール WDK ネットワーク モジュールの登録、添付ファイル
- クライアント モジュール WDK ネットワーク モジュールの登録、添付ファイル
- ネットワーク モジュールのアタッチ
- ネットワーク モジュールの登録
- ネットワーク モジュール レジストラー WDK は、ネットワーク モジュールのアタッチ
- ネットワーク モジュールのアタッチ、NMR WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06aff6e1dd570eb521bd60394cc5d236bdf6cbf1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331910"
---
# <a name="network-module-attachment"></a>ネットワーク モジュールのアタッチ


前に、[クライアント モジュール](client-module.md)と[プロバイダー モジュール](provider-module.md)関連付けることができます、互いに各登録が必要な自体、NMR とします。 クライアント モジュールを呼び出すことによって、NMR で登録、 [ **NmrRegisterClient** ](https://msdn.microsoft.com/library/windows/hardware/ff568782)関数とプロバイダーを呼び出すことによって、NMR モジュールに登録、 [ **NmrRegisterProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff568784)関数。 次の図は、ネットワーク モジュールの登録を示します。

![ネットワーク モジュールの登録を示す図](images/nmrattach1.png)

クライアントのモジュールとプロバイダー、モジュールの両方は指定と同じでかどうか[ネットワーク プログラミング インターフェイス (NPI)](network-programming-interface.md) NMR が 2 つのネットワーク モジュールをまとめて接続を開始、NMR に登録するとき。 NMR クライアントのモジュールを呼び出すことによってアタッチ プロセスを開始します[ *ClientAttachProvider* ](https://msdn.microsoft.com/library/windows/hardware/ff544903)コールバック関数。 次の図は、ネットワーク モジュール レジストラー (NMR)、添付ファイルの開始を示します。

![添付ファイルを開始するネットワーク モジュール レジストラー (nmr) を示す図](images/nmrattach2.png)

クライアント モジュールの[ *ClientAttachProvider* ](https://msdn.microsoft.com/library/windows/hardware/ff544903)コールバック関数は、確認のかどうかは、プロバイダー モジュールに接続するプロバイダー モジュールの登録データを調べることができます。 呼び出して添付ファイルのプロセスを続行クライアント モジュール プロバイダー モジュールに接続すると判断した場合、 [ **NmrClientAttachProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff568770)関数。 クライアント モジュールを呼び出すと、 **NmrClientAttachProvider**関数、NMR はさらに、プロバイダー モジュールの呼び出し[ *ProviderAttachClient* ](https://msdn.microsoft.com/library/windows/hardware/ff570395)コールバック関数。 次の図は、添付ファイルを引き続きクライアント モジュールを示します。

![添付ファイルを引き続きクライアント モジュールを示す図](images/nmrattach3.png)

プロバイダー モジュールの[ *ProviderAttachClient* ](https://msdn.microsoft.com/library/windows/hardware/ff570395)コールバック関数は、確認のかどうかは、クライアント モジュールに接続するクライアント モジュールの登録データを調べることができます。 プロバイダー モジュールがクライアント モジュールに接続すると判断した場合、プロバイダー モジュールとクライアント モジュールは、そのそれぞれ NPI ディスパッチ テーブル構造へのポインターを交換します。 クライアントのモジュールとプロバイダー モジュールをアタッチした後は、NMR の独立した、NPI 関数を使用して相互作用できます。 次の図は、接続されているネットワーク モジュールを示します。

![接続されているネットワーク モジュールを示す図](images/nmrattach4.png)
