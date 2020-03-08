---
title: システム定義の ECP
description: システム定義の ECP
ms.assetid: 6acb4be4-a7aa-431d-b2d8-3ef6d41cb4ef
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85b9b23152e693824c6f0092315e8074762a571a
ms.sourcegitcommit: 8c898615009705db7633649a51bef27a25d72b26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/07/2020
ms.locfileid: "78910472"
---
# <a name="system-defined-ecps"></a>システム定義の ECP


オペレーティングシステムでは、 *Ntifs*ヘッダーファイルに次の ecps が定義されています。 これらのシステム定義の ECPs は、指定された追加情報を、ファイルに対する[**IRP\_MJ\_CREATE**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)操作にアタッチします。 ファイルシステムスタックの要素は、追加情報を ECPs に照会できます。

通常、 [**irp\_\_MJ**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)を処理してファイルに対して作成操作を実行し、その下のフィルターにファイルを渡すフィルターは、ファイルに対する**irp\_MJ\_CREATE**操作に、次のシステム定義の ecps をアタッチしてスプーフィングする必要があります。 同様に、IRP\_MJ を処理および発行するカーネルモードドライバーは、ファイルに対して作成操作を実行\_、次のシステム定義のすべての ECPs を、IRP\_MJ\_ファイルに対する作成操作にアタッチして偽装することはできません。 次のシステム定義の ECPs は読み取り専用です。 情報を取得するためにのみ使用する必要があります。

フィルタードライバーが次のシステム定義の ECPs のいずれかをアタッチしないように制限する例外の1つは、フィルタードライバーがレイヤーファイルシステムを実装する場合です。 これを行うには、ファイルオブジェクトを所有し、独自の[**irp\_\_MJ**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)を発行して、そのフィルターの下にあるファイルに対して、IRP\_MJ\_create 操作に応答して、そのファイルオブジェクトでフィルタードライバーがサービスを実行することによって、ファイルオブジェクトを所有します。 このようなフィルタードライバーは、ファイルに対する元の IRP\_MJ\_作成操作から、フィルタードライバーによって発行された IRP\_MJ\_CREATE 操作に、すべての ECP コンテキスト構造リスト (ECP\_リスト) を伝達する必要があります。 これらの ECP リストを伝達することにより、フィルタードライバーは、IRP\_MJ\_CREATE 操作を発行するフィルターの下にあるフィルターが、元の IRP\_MJ\_CREATE 操作のコンテキストを認識していることを確認します。

<span id="GUID_ECP_OPLOCK_KEY"></span><span id="guid_ecp_oplock_key"></span>GUID\_ECP\_OPLOCK\_キー  
[ **\_キー\_ECP\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ifs/oplock-key-ecp-context)構造を識別する GUID。この GUID を使用して、oplock キーが open file 要求にアタッチされます。 Oplock キーを使用すると、アプリケーション独自の oplock を損なうことなく、同じストリームに対して複数のハンドルを開くことができます。

Oplock キーと oplock キーの詳細については、「 [Oplock セマンティクスの概要](oplock-overview.md)」を参照してください。

<span id="GUID_ECP_NETWORK_OPEN_CONTEXT"></span><span id="guid_ecp_network_open_context"></span>GUID\_ECP\_ネットワーク\_開いている\_コンテキスト  
ネットワーク\_を識別する GUID [ **\_ECP\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff550896)構造を開き、ネットワークリダイレクターの追加情報をアタッチするために使用されます。 また、この GUID は、windows 7 以降のバージョンの Windows で実行され、Windows Vista 上に存在するファイルでネットワーク ECP コンテキストを解釈する必要があるドライバーに対して、 [ **\_ECP\_コンテキスト\_V0 構造を開くネットワーク\_** ](https://msdn.microsoft.com/library/windows/hardware/ff550899)も識別します。

<span id="GUID_ECP_PREFETCH_OPEN"></span><span id="guid_ecp_prefetch_open"></span>\_プリフェッチ\_の GUID\_ECP  
[ **\_ECP\_コンテキスト構造を開く\_のプリフェッチ**](https://msdn.microsoft.com/library/windows/hardware/ff551843)を識別する GUID。

Prefetcher は、キャッシュマネージャーおよびメモリマネージャーと緊密に統合されているオペレーティングシステムのコンポーネントであり、ディスクへのアクセス効率を高め、パフォーマンスを向上させます。 他のコンポーネントが prefetcher に干渉する場合、システムのパフォーマンスが低下し、デッドロックが発生する可能性があります。 このため、prefetcher は\_ECP\_コンテキスト構造を開いているプリフェッチ\_をファイルにアタッチして、ファイルに対して開いている要求を prefetcher が実行することを通知します。 このオープンな要求は、\_ECP\_コンテキスト\_開いているプリフェッチの**コンテキスト**メンバーによって指定されます。 ファイルシステムフィルタードライバーなどの他のコンポーネントでは、プリフェッチ\_開いている\_ECP\_コンテキストがファイルに添付されているかどうかを判断し、適切なアクションを実行できます。

<span id="GUID_ECP_NFS_OPEN"></span><span id="guid_ecp_nfs_open"></span>\_NFS\_の GUID\_ECP  
[ **\_ECP\_コンテキスト構造を開く\_NFS**](https://msdn.microsoft.com/library/windows/hardware/ff550942)を識別する GUID。 ネットワークファイルシステム (NFS) サーバーは、開いているファイル要求に対して、\_ECP\_の\_開いている NFS をアタッチします。 Nfs サーバーは、NFS サーバーがクライアント要求を満たすために使用するすべての開いているファイル要求で、この GUID を使用します。 その後、ファイルシステムスタックは、\_ECP\_コンテキストが開いているファイルの要求にアタッチされて\_いるかどうかを確認できます。 NFS の情報に基づいて\_ECP\_コンテキストを開く\_、ファイルシステムスタックは、ファイルのオープンを要求したクライアントとその理由を特定できます。

<span id="GUID_ECP_SRV_OPEN"></span><span id="guid_ecp_srv_open"></span>\_ECP\_SRV\_開いている GUID  
[ **\_ECP\_コンテキスト構造を開く\_SRV**](https://msdn.microsoft.com/library/windows/hardware/ff556749)を識別する GUID。 サーバーは、開いているファイル要求に対して\_ECP\_コンテキスト構造を開いている\_SRV をアタッチします。 サーバーは、条件付きクライアント要求を満たすためにサーバーが行うすべての開いているファイル要求で、この GUID を使用します。 その後、ファイルシステムスタックは、SRV\_開いている\_ECP\_コンテキストが open file 要求にアタッチされているかどうかを判断できます。 SRV の情報に基づいて\_ECP\_コンテキストを開く\_、ファイルシステムスタックは、ファイルのオープンを要求したクライアントとその理由を特定できます。

<span id="GUID_ECP_DUAL_OPLOCK_KEY"></span><span id="guid_ecp_dual_oplock_key"></span>GUID\_ECP\_2\_OPLOCK\_キー  
[ **\_ECP\_コンテキスト構造の2つの\_キー**](https://docs.microsoft.com/windows-hardware/drivers/ifs/dual-oplock-key-ecp-context)を識別する GUID。 [**Oplock\_キー\_ecp\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ifs/oplock-key-ecp-context)構造と同様に、**デュアル oplock\_キー\_ecp\_context**を使用して、open file 要求に oplock キーをアタッチします。 **\_キー\_ECP\_コンテキスト**では、親キーを設定して、ターゲットファイルのディレクトリに対して oplock を指定することもできます。

<span id="GUID_ECP_IO_DEVICE_HINT"></span><span id="guid_ecp_io_device_hint"></span>GUID\_ECP\_IO\_デバイス\_ヒント  
**IO\_デバイス\_ヒント\_ECP\_コンテキスト**構造を識別する GUID。 デバイスヒントは、新しいデバイスへの再解析ターゲットを追跡するときに、名前プロバイダーのミニフィルタードライバーを支援するために使用されます。

<span id="GUID_ECP_NETWORK_APP_INSTANCE"></span><span id="guid_ecp_network_app_instance"></span>\_ネットワーク\_アプリ\_インスタンスの GUID\_ECP  
[**ネットワーク\_アプリ\_インスタンス\_ECP\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/hh439443)構造を識別する GUID。 フェールオーバークラスター内のクライアントアプリケーションは、クラスター内のノードで開かれた一連のファイルを持つことができます。 ファイルオブジェクトは、**ネットワーク\_アプリ\_インスタンス\_ECP\_コンテキスト**構造のインスタンス識別子によってアプリケーションにタグ付けされます。 フェールオーバーでは、セカンダリノードは、以前にキャッシュされたアプリケーションインスタンス識別子を使用して、開いているファイルへのクライアントアプリケーションのアクセスを検証できます。

 

 




