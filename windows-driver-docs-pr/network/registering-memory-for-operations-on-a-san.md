---
title: SAN の操作にメモリを登録します。
description: SAN の操作にメモリを登録します。
ms.assetid: 5492466e-4765-4d43-b6bc-1d5bc74996ba
keywords:
- SAN 接続のセットアップ WDK、メモリを登録します。
- 登録用のメモリの San
- データ バッファーの WDK San
- バッファー WDK San
- データ バッファーを登録します。
- WDK の San のメモリ
- 登録されているメモリ WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bc6a51cde8a8cb5cd7369a8a0c045f3aa8325dc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531346"
---
# <a name="registering-memory-for-operations-on-a-san"></a>SAN の操作にメモリを登録します。





Windows ソケットは、SAN サービス プロバイダーの拡張は、メッセージを送受信するため、および rdma システム エリア ネットワーク上のすべてのデータ バッファーを登録する関数の呼び出しを切り替えます。 これらの拡張関数では、リモート ピアに接続されている特定の SAN ソケットで使用するための物理メモリの領域にバッファーを登録します。 これらの拡張関数の説明は、次を参照してください。、 [Windows Sockets SPI Extensions for San](windows-sockets-spi-extensions-for-sans.md)します。

### <a name="registering-data-buffers"></a>データ バッファーを登録します。

スイッチの呼び出し、SAN サービス プロバイダーの[ **WSPRegisterMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff566311)をによってのみアクセスできるデータ バッファーを登録するローカル プロセスで実行されるアプリケーションに代わって拡張関数プロセスです。 バッファーを処理する**WSPRegisterMemory**返しますが、登録を実行するためのローカル プロセスのコンテキストでのみ有効です。 スイッチ呼び出し**WSPRegisterMemory**への呼び出しにバッファーを受信するメッセージとして使用するバッファーを登録する、 [ **WSPRecv** ](https://msdn.microsoft.com/library/windows/hardware/ff566309)関数またはでバッファーを送信するメッセージ呼び出し、 [ **WSPSend** ](https://msdn.microsoft.com/library/windows/hardware/ff566316)関数。 スイッチの呼び出しも**WSPRegisterMemory**への呼び出しで受信側ローカルの RDMA のバッファーとして機能するバッファーを登録する、 [ **WSPRdmaRead** ](https://msdn.microsoft.com/library/windows/hardware/ff566304)拡張関数、またはローカルの RDMA ソースへの呼び出しで、 [ **WSPRdmaWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff566306)拡張関数。 登録済みのバッファーを使用してローカル処理の終了後**WSPRegisterMemory**、スイッチの呼び出し、 [ **WSPDeregisterMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff566279)拡張関数をこれらのバッファーを解放します。

スイッチの呼び出し、SAN サービス プロバイダーの[ **WSPRegisterRdmaMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff566313) RDMA を登録するローカル プロセスで実行されるアプリケーションに代わって拡張関数をローカルとリモートの両方をバッファー処理プロセスにアクセスできます。 バッファー記述子を**WSPRegisterRdmaMemory**返しますはリモート ピアを登録には、SAN ソケットへのピアの接続のコンテキストで開始する RDMA データ転送操作でのみ有効です実行されます。 リモート ピアの接続にあるスイッチへの呼び出しで、いずれかのターゲットとしてこれらの RDMA バッファーを使用して、 **WSPRdmaWrite**拡張関数またはソースへの呼び出しで、 **WSPRdmaRead**拡張関数。 登録済みのバッファーを使用して、ローカルとリモート プロセスの完了後**WSPRegisterRdmaMemory**、スイッチの呼び出し、 [ **WSPDeregisterRdmaMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff566281)これらのバッファーを解放する拡張関数。

### <a name="managing-memory-access"></a>メモリ アクセスを管理します。

SAN サービス プロバイダーは、登録済みのメモリを不正アクセスを防止する必要があります。

メモリは、次のように登録されている、アクセス可能でなければなりません。

メモリにローカル アクセスをスイッチと呼ばれるプロセスでのみ使用できるが登録されている**WSPRegisterMemory**します。

メモリには、ローカルとリモートの両方のアクセスは、スイッチと呼ばれるプロセスによってアクセスできるが登録されている**WSPRegisterRdmaMemory**メモリを登録または SAN に接続されているリモート ピアによってするソケット、メモリ登録されます。

メモリは、接続が確立されている間、および登録されている場合にのみアクセス可能である必要があります。 SAN サービス プロバイダーは、ことには誤ってこのようなメモリ アクセスできるように、同じコンピューターまたは他のコンピューターを SAN で実行されている他のプロセスにことを確認する必要があります。

メモリの読み取りアクセス用にのみ登録しない書き込みアクセスで使用可能な場合があります。 メモリの書き込みアクセス用にのみ登録しないに対して読み取りアクセスを必要があります。

### <a name="using-registered-memory"></a>登録済みのメモリを使用します。

スイッチは、メモリのデータ転送セッションのネゴシエーションを使用する各接続の TCP ソケットの連続する事実上 2 つのリージョンを登録します。 スイッチでは、メモリの 1 つのリージョンを使用して、SAN サービス プロバイダーの呼び出し時に、送信データを格納するメッセージ バッファーを提供する**WSPSend**関数。 スイッチでは、メモリの他の領域を使用して、SAN サービス プロバイダーの呼び出し時にデータを受信するメッセージ バッファーを転記する**WSPRecv**関数。

スイッチは、rdma でアプリケーション データを転送する場合にのみ、RDMA のバッファーを通常登録します。

スイッチがソケットを閉じる前に、スイッチを呼び出すか**WSPDeregisterMemory**または**WSPDeregisterRdmaMemory**保留中のデータを転送するメモリを解放する SAN サービス プロバイダーの機能操作が現在使用していません。 SAN サービス プロバイダーは、未処理のデータ転送操作に関連付けられているメモリを解放もする必要があります。

 

 





