---
title: SAN 用の Windows ソケット SPI 拡張機能
description: SAN 用の Windows ソケット SPI 拡張機能
ms.assetid: 08f51612-2e2b-439a-8318-43884086828c
keywords:
- SAN サービス プロバイダー WDK、拡張機能
- WDK の San の拡張機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99bf578ef9c7efc9a62132bafaef084235dc95dc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335301"
---
# <a name="windows-sockets-spi-extensions-for-sans"></a>SAN 用の Windows ソケット SPI 拡張機能





このセクションでは、SAN サービス プロバイダーの DLL を指定する必要がありますを提供する SAN 拡張関数の簡単な説明を提供します。 これらの関数は、san の使用の Windows Sockets SPI を拡張します。 拡張機能が Ws2san.h で定義され、記載されて、 [Windows Sockets の直接参照](https://msdn.microsoft.com/library/windows/hardware/ff565857)セクション。

を除き、 **WSPStartupEx**関数の場合、このセクションに記載の拡張機能は、によって取得されます Windows Sockets を切り替えます。 Windows Sockets スイッチが SAN サービス プロバイダーを呼び出すには、これらの拡張機能の各エントリ ポイントを取得する[ **WSPIoctl** ](https://msdn.microsoft.com/library/windows/hardware/ff566296)関数を渡す、SIO\_取得\_拡張機能\_関数\_ポインター コマンド コード値を持つが次のいずれかを識別する GUID とは、関数を拡張します。

SAN サービス プロバイダーは、すべての例外として次の拡張関数を実装する必要があります、 **WSPRdmaRead**と**WSPMemoryRegistrationCacheCallback**関数。 いずれかとも SAN サービス プロバイダーがサポートされていない場合、 **WSPRdmaRead**または**WSPMemoryRegistrationCacheCallback**拡張関数では、その**WSPIoctl**関数が返す必要がありますエラー WSAEOPNOTSUPP Windows Sockets を切り替えるときに要求するか、エントリ ポイント**WSPRdmaRead**または**WSPMemoryRegistrationCacheCallback**します。

<a href="" id="wspstartupex"></a>[**WSPStartupEx**](https://msdn.microsoft.com/library/windows/hardware/ff566321)  
Windows ソケットの切り替えを開始しますの SAN サービス プロバイダーの使用です。

<a href="" id="wspregistermemory"></a>[**WSPRegisterMemory**](https://msdn.microsoft.com/library/windows/hardware/ff566311)  
ソケットがローカルのソースまたはデータ転送操作のローカルの対象として使用するバッファー配列を登録します。 このようなソケットは、このバッファーの配列を使用して、ソース バッファーとして**WSPRdmaWrite**と**WSPSend**内での呼び出しと受信バッファー **WSPRdmaRead**と**WSPRecv**呼び出し。

<a href="" id="wspderegistermemory"></a>[**WSPDeregisterMemory**](https://msdn.microsoft.com/library/windows/hardware/ff566279)  
以前の呼び出しによって登録されるバッファーの配列を解放、 **WSPRegisterMemory**関数。

<a href="" id="wspregisterrdmamemory"></a>[**WSPRegisterRdmaMemory**](https://msdn.microsoft.com/library/windows/hardware/ff566313)  
リモート ピアの接続とそのピア接続の間のデータを転送するために公開されている RDMA バッファー配列を登録します。 リモート ピアのソケットのターゲット バッファーとしてこの RDMA バッファーの配列を使用できます、 **WSPRdmaWrite**内での呼び出しと、ソース バッファーを**WSPRdmaRead**呼び出します。

<a href="" id="wspderegisterrdmamemory"></a>[**WSPDeregisterRdmaMemory**](https://msdn.microsoft.com/library/windows/hardware/ff566281)  
以前の呼び出しによって登録されるバッファーの配列を解放、 **WSPRegisterRdmaMemory**関数。

<a href="" id="--------wspmemoryregistrationcachecallback"></a>[**WSPMemoryRegistrationCacheCallback**](https://msdn.microsoft.com/library/windows/hardware/ff566299)  
アプリケーションのバッファーとバッファーと物理メモリのロックの所有権を解放し、サービス プロバイダーのキャッシュと SAN NIC からバッファー登録 SAN からバッファーを削除します。

<a href="" id="wsprdmaread"></a>[**WSPRdmaRead**](https://msdn.microsoft.com/library/windows/hardware/ff566304)  
ソケットのリモート ピアにアクセスできるアドレス空間が RDMA バッファーからローカル ソケットにアクセスできるアドレス空間内のバッファーにデータを転送します。

<a href="" id="wsprdmawrite"></a>[**WSPRdmaWrite**](https://msdn.microsoft.com/library/windows/hardware/ff566306)  
ソケットのリモート ピアにアクセスできるアドレス空間内のターゲット RDMA バッファーにローカル ソケットにアクセスできるアドレス空間内のソース バッファーからデータを転送します。

 

 





