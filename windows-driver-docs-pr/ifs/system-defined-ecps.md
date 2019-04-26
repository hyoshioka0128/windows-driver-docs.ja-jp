---
title: システム定義の ECP
description: システム定義の ECP
ms.assetid: 6acb4be4-a7aa-431d-b2d8-3ef6d41cb4ef
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3dc84b3904b4b97aa42a79b96c4e4b9808847751
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344350"
---
# <a name="system-defined-ecps"></a>システム定義の ECP


オペレーティング システムで次の ECPs の定義、 *Ntifs.h*ヘッダー ファイル。 これらのシステム定義の ECPs に指定した追加情報をアタッチする、 [ **IRP\_MJ\_作成**](https://msdn.microsoft.com/library/windows/hardware/ff548630)ファイルを操作します。 ファイル システム スタックの要素の追加情報について ECPs を照会できます。

通常、フィルター処理、 [ **IRP\_MJ\_作成**](https://msdn.microsoft.com/library/windows/hardware/ff548630)ファイルしまで下にあるフィルター ファイルのアタッチし、次のいずれかになりすます必要がありますいないパスの操作システム定義に ECPs、 **IRP\_MJ\_作成**ファイルで操作します。 処理し、IRP を発行するカーネル モード ドライバーに同様に、\_MJ\_ファイルに対する操作を作成する必要がありますいないアタッチし、IRP を次のシステム定義 ECPs のいずれかになりすます\_MJ\_作成操作で、ファイル。 次のシステム定義 ECPs は読み取り専用です。 それらを使用して、情報のみを取得する必要があります。

1 つの例外が次のシステム定義 ECPs のいずれかをアタッチするフィルター ドライバーを制限することには、フィルター ドライバーは、階層型ファイル システムを実装している場合です。 これは、ファイル オブジェクトを所有し、独自に発行して[ **IRP\_MJ\_作成**](https://msdn.microsoft.com/library/windows/hardware/ff548630) IRP への応答でそのフィルターの下のファイルに対する操作\_MJ\_ファイル フィルター ドライバーは、独自のファイル オブジェクトのサービスを作成する操作。 フィルター ドライバーがこのような ECP コンテキスト構造体のリストを反映する必要があります (ECP\_リスト) 元の IRP から\_MJ\_IRP のファイルの作成操作\_MJ\_作成操作をフィルター ドライバーその下の問題です。 これらの ECP リストを伝達することで、フィルター ドライバーにより、IRP を発行するフィルターの下のすべてのフィルター\_MJ\_作成操作は元の IRP のコンテキストを認識\_MJ\_作成操作です。

<span id="GUID_ECP_OPLOCK_KEY"></span><span id="guid_ecp_oplock_key"></span>GUID\_ECP\_OPLOCK\_キー  
識別する GUID、 [ **OPLOCK\_キー\_ECP\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff551003)構造体であり、oplock のキーをファイルを開く要求にアタッチするために使用します。 Oplock キーには、アプリケーションのアプリケーションの oplock を損なうことがなく、同じストリームへの複数のハンドルを開くことができます。

各 oplock と oplock のキーの詳細については、次を参照してください。 [Oplock セマンティクス概要](overview.md)します。

<span id="GUID_ECP_NETWORK_OPEN_CONTEXT"></span><span id="guid_ecp_network_open_context"></span>GUID\_ECP\_ネットワーク\_オープン\_コンテキスト  
識別する GUID、 [**ネットワーク\_オープン\_ECP\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff550896)構造体し、ネットワーク リダイレクターの余分な情報をアタッチするために使用します。 この GUID も識別、 [**ネットワーク\_オープン\_ECP\_コンテキスト\_V0** ](https://msdn.microsoft.com/library/windows/hardware/ff550899)ドライバーが Windows 7 および以降のバージョンで動作するための構造Windows および Windows Vista に存在するファイルをネットワーク ECP コンテキストを解釈する必要があります。

<span id="GUID_ECP_PREFETCH_OPEN"></span><span id="guid_ecp_prefetch_open"></span>GUID\_ECP\_プリフェッチ\_開く  
識別する GUID、 [**プリフェッチ\_オープン\_ECP\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff551843)構造体。

プリフェッチャは、ディスク アクセスをより効率的に行うし、パフォーマンスが向上するには、キャッシュ マネージャーとメモリ マネージャーと緊密に統合されているオペレーティング システムのコンポーネントです。 その他のコンポーネントに干渉プリフェッチャ場合、システムのパフォーマンスが低下し、デッドロックの可能性があります。 プリフェッチャがプリフェッチをアタッチするため、\_開く\_ECP\_コンテキスト通信プリフェッチャがファイルで、オープンの要求を実行するために、ファイル構造体。 このオープン要求がで指定された、**コンテキスト**プリフェッチのメンバー\_開く\_ECP\_コンテキスト。 その他のコンポーネントでは、次のように、ファイル システム フィルター ドライバー、プリフェッチするかどうかを調べる\_オープン\_ECP\_ファイルとし、適切なアクションを実行するコンテキストが接続されています。

<span id="GUID_ECP_NFS_OPEN"></span><span id="guid_ecp_nfs_open"></span>GUID\_ECP\_NFS\_開く  
識別する GUID、 [ **NFS\_オープン\_ECP\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff550942)構造体。 Network File System (NFS) サーバー、NFS をアタッチします\_開く\_ECP\_ファイルを開く要求にコンテキストの構造体。 NFS サーバーは、NFS サーバーはクライアント要求を満たすために、すべてのファイルを開く要求で、この GUID を使用します。 ファイル システム スタックを確認できるかどうか NFS\_開く\_ECP\_コンテキストが開いているファイルの要求に添付します。 NFS の情報に基づいて\_オープン\_ECP\_コンテキスト、ファイル システム スタックは、ファイルが開かれることを要求したクライアントを判断できますとその理由です。

<span id="GUID_ECP_SRV_OPEN"></span><span id="guid_ecp_srv_open"></span>GUID\_ECP\_SRV\_開く  
識別する GUID、 [ **SRV\_オープン\_ECP\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff556749)構造体。 サーバーが、SRV をアタッチします\_開く\_ECP\_ファイルを開く要求にコンテキストの構造体。 サーバーは、条件付きのクライアント要求を満たすために、サーバーを使用するすべてのファイルを開く要求でこの GUID を使用します。 ファイル システム スタックを確認できるかどうか SRV\_開く\_ECP\_コンテキストが開いているファイルの要求に添付します。 SRV の情報に基づいて\_オープン\_ECP\_コンテキスト、ファイル システム スタックは、ファイルが開かれることを要求したクライアントを判断できますとその理由です。

<span id="GUID_ECP_DUAL_OPLOCK_KEY"></span><span id="guid_ecp_dual_oplock_key"></span>GUID\_ECP\_デュアル\_OPLOCK\_キー  
識別する GUID、 [**デュアル OPLOCK\_キー\_ECP\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/hh406392)構造体。 ように、 [ **OPLOCK\_キー\_ECP\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff551003)構造、**デュアル OPLOCK\_キー\_ECP\_コンテキスト**oplock のキーをファイルを開く要求にアタッチするために使用します。 **デュアル OPLOCK\_キー\_ECP\_コンテキスト**、ただし、親キーも設定できますターゲット ファイルのディレクトリに oplock を提供します。

<span id="GUID_ECP_IO_DEVICE_HINT"></span><span id="guid_ecp_io_device_hint"></span>GUID\_ECP\_IO\_デバイス\_ヒント  
識別する GUID、 **IO\_デバイス\_ヒント\_ECP\_コンテキスト**構造体。 デバイスのヒントは、新しいデバイスを再解析対象の追跡プロバイダー ミニフィルター ドライバーの名前を支援するために使用されます。

<span id="GUID_ECP_NETWORK_APP_INSTANCE"></span><span id="guid_ecp_network_app_instance"></span>GUID\_ECP\_ネットワーク\_アプリ\_インスタンス  
識別する GUID、 [**ネットワーク\_アプリ\_インスタンス\_ECP\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/hh439443)構造体。 フェールオーバー クラスター内のクライアント アプリケーションでは、クラスター内のノードで開いたファイルのセットがあります。 インスタンス識別子で、ファイル オブジェクトをアプリケーションにタグが付けられた、**ネットワーク\_アプリ\_インスタンス\_ECP\_コンテキスト**構造体。 フェールオーバー時は、セカンダリ ノードは、開いているファイルを以前にキャッシュされたアプリケーションのインスタンス識別子を使用するクライアント アプリケーションのアクセスを検証できます。

 

 




