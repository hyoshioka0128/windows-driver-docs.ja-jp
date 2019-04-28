---
title: RPC 状態情報の内部構造
description: RPC 状態情報の内部構造
ms.assetid: fac4a1e4-e1ec-41f2-8de9-073a04a979be
keywords:
- RPC デバッグは、RPC 状態情報の内部構造
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6445fd83745dfaa98e2b52ab5f3692da18fbe87d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382047"
---
# <a name="rpc-state-information-internals"></a>RPC 状態情報の内部構造


## <span id="ddk_rpc_state_information_internals_dbg"></span><span id="DDK_RPC_STATE_INFORMATION_INTERNALS_DBG"></span>


このセクションでは、RPC ランタイムによって収集された状態情報の内部構造の詳細を提供します。

すべての RPC ランタイム状態情報は、セルに含まれます。 セルは、個別に更新および表示が可能な情報の最小単位です。

RPC ランタイムの各キー オブジェクトの状態に関する情報の 1 つまたは複数のセルが維持されます。 各セルはセルの ID を持つ そのオブジェクトのセルの ID を指定することでは、オブジェクトは、別のオブジェクトを参照しているときに RPC ランタイムは、に関する情報を維持できる主要なオブジェクトは、エンドポイント、スレッド、接続オブジェクト、サーバーを呼び出す (SCALL) オブジェクト、およびクライアントの呼び出し (CCALL) オブジェクト。

**RPC サーバーが実行されている**、RPC ランタイムは、一連の 1 つまたは複数のワーカー スレッドを使用してエンドポイントでリッスンします。 データは、サーバーに送信される、たびに、スレッドは、データを取得し、受信した要求を決定します。 要求の接続を作成する場合、接続オブジェクトを作成すると、およびサービスの接続上のすべての呼び出し、このオブジェクト。 接続で RPC 呼び出しが行われる接続オブジェクトは、クライアントの呼び出し (CCALL) オブジェクトに対応するサーバーを呼び出す (SCALL) オブジェクトをインスタンス化します。 このサーバーを呼び出すオブジェクトは、この特定の呼び出しを処理します。

**RPC クライアントが実行されている**、RPC ランタイムは呼び出しが行われるたびにクライアントを呼び出すオブジェクトを作成します。 このクライアントを呼び出すオブジェクトには、この特定の呼び出しに関する情報が含まれています。

### <a name="span-idendpointcellsspanspan-idendpointcellsspanendpoint-cells"></a><span id="endpoint_cells"></span><span id="ENDPOINT_CELLS"></span>エンドポイントのセル

エンドポイントと、RPC ランタイムの観点から、特定のサーバーに接続できるエントリ ポイントです。 エンドポイントは、指定された RPC トランスポートに関連付けられては常にします。 エンドポイントの状態情報は、クライアント呼び出しを関連付ける、サーバー上の特定のプロセスに使用されます。

エンドポイントのセルにフィールドは次のとおりです。

<span id="ProtseqType"></span><span id="protseqtype"></span><span id="PROTSEQTYPE"></span>**ProtseqType**  
このエンドポイントのプロトコル順序を指定します。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状態**  
状態値:*割り当て*、 *active*、または*非アクティブな*します。 ほとんどのエンドポイントがアクティブです。 エンドポイントが*割り当て*ステータス作成プロセスが開始されると、まだ完了がない場合。 エンドポイントが*非アクティブな*(たとえば、プロトコルがアンインストールされている) 場合は使用で不要になった場合。

<span id="EndpointName"></span><span id="endpointname"></span><span id="ENDPOINTNAME"></span>**EndpointName**  
エンドポイント名の最初の 28 文字。

### <a name="span-idthreadcellsspanspan-idthreadcellsspanthread-cells"></a><span id="thread_cells"></span><span id="THREAD_CELLS"></span>スレッドのセル

サーバーのスレッドはワーカー スレッド (RPC が使用する標準の Win32 スレッドです)。

スレッドのセルにフィールドは次のとおりです。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状態**  
状態値:*処理*、*ディスパッチ*、*割り当て*、または*アイドル*します。 A*処理*スレッドがあり、ランタイム内で情報を処理します。 A*ディスパッチ*スレッドが既にディスパッチ (と呼ばれる) サーバーによって提供された manager ルーチンに (通常は単と呼ばれる、 *server ルーチン*)。 *割り当て*スレッドがキャッシュされています。 *アイドル*スレッドがサービス要求に使用できます。

<span id="LastUpdateTime"></span><span id="lastupdatetime"></span><span id="LASTUPDATETIME"></span>**LastUpdateTime**  
(ブート後のミリ秒単位) で情報が最後に更新された時刻。

<span id="TID"></span><span id="tid"></span>**TID**  
このスレッドのスレッド ID。 これは、機能は、デバッガーでスレッドの一覧と関連付けるためにしようとしたときに便利です。

### <a name="span-idconnectionobjectcellsspanspan-idconnectionobjectcellsspanconnection-object-cells"></a><span id="connection_object_cells"></span><span id="CONNECTION_OBJECT_CELLS"></span>接続オブジェクトのセル

接続オブジェクトのセル内のフィールドは次のとおりです。

<span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>**フラグ**  
フラグの値が含まれます*排他*/*非排他的な*、*認証レベル*、および*認証サービス*します。

<span id="LastTransmitFragmentSize"></span><span id="lasttransmitfragmentsize"></span><span id="LASTTRANSMITFRAGMENTSIZE"></span>**LastTransmitFragmentSize**  
接続で送信された最後のフラグメントのサイズ。

<span id="Endpoint"></span><span id="endpoint"></span><span id="ENDPOINT"></span>**エンドポイント**  
この接続から取得されたエンドポイントのセルの ID。

<span id="LastSendTime"></span><span id="lastsendtime"></span><span id="LASTSENDTIME"></span>**LastSendTime**  
接続で最後にデータが送信されました。

<span id="LastReceiveTime"></span><span id="lastreceivetime"></span><span id="LASTRECEIVETIME"></span>**LastReceiveTime**  
接続で最後にデータを受信しました。

### <a name="span-idservercallobjectcellsspanspan-idservercallobjectcellsspanserver-call-object-cells"></a><span id="server_call_object_cells"></span><span id="SERVER_CALL_OBJECT_CELLS"></span>サーバーの呼び出しオブジェクトのセル

サーバーを呼び出す (SCALL) オブジェクトのセル内のフィールドは次のとおりです。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状態**  
状態値:*割り当て*、 *active*、または*ディスパッチ*します。 *割り当て*呼び出しがアクティブでないと、キャッシュされました。 呼び出しがあるときに*active*、RPC ランタイムがこの呼び出しに関連する情報を処理します。 呼び出しがあるときに*ディスパッチ*、manager ルーチン (server ルーチン) が呼び出され、まだが返されません。

<span id="ProcNum"></span><span id="procnum"></span><span id="PROCNUM"></span>**ProcNum**  
この呼び出しのプロシージャ番号 (netmon キャプチャ ファイルの場合は操作数)。 RPC ランタイムは、IDL ファイル内の位置番号で、インターフェイスから個々 のルーチンを識別します。 インターフェイスでは、最初のルーチンは、数字の 0、1、2 つ目および具合になります。

<span id="InterfaceUUIDStart"></span><span id="interfaceuuidstart"></span><span id="INTERFACEUUIDSTART"></span>**InterfaceUUIDStart**  
インターフェイスの UUID の最初の dword 値です。

<span id="ServicingTID"></span><span id="servicingtid"></span><span id="SERVICINGTID"></span>**ServicingTID**  
この呼び出しを処理するスレッドのセルの ID。 呼び出しがない場合*active*または*ディスパッチ*、これには、古い情報が含まれます。

<span id="CallFlags"></span><span id="callflags"></span><span id="CALLFLAGS"></span>**CallFlags**  
これらのフラグ値では、排他的な接続でキャッシュされた呼び出しは、これは、これは、パイプ呼び出しかどうかの非同期呼び出し、かどうかと、これは LRPC または OSF 呼び出しかどうかがこのかどうかを示します。

<span id="LastUpdateTime"></span><span id="lastupdatetime"></span><span id="LASTUPDATETIME"></span>**LastUpdateTime**  
最後の時間 (ミリ秒単位に起動した後) と呼び出しオブジェクトの状態情報に更新されました。

<span id="PID"></span><span id="pid"></span>**PID**  
呼び出し元のプロセス ID。 LRPC 呼び出しに対してのみ有効です。

<span id="TID"></span><span id="tid"></span>**TID**  
呼び出し元のスレッド ID。 LRPC 呼び出しに対してのみ有効です。

### <a name="span-idclientcallobjectcellsspanspan-idclientcallobjectcellsspanclient-call-object-cells"></a><span id="client_call_object_cells"></span><span id="CLIENT_CALL_OBJECT_CELLS"></span>クライアント呼び出しオブジェクトのセル

クライアントの呼び出し (CCALL) オブジェクトは、1 つのセルに収まるようにクライアントの呼び出しに関する情報が大きすぎるために、2 つのセルに分割されます。 最初のセルと呼ばれる*クライアント呼び出し情報*、され、2 つ目が呼び出されます*呼び出しターゲット情報*します。 ほとんどのツールが情報をまとめて、表示されるため、それらを区別する必要はありません。

完全な状態情報を収集している場合を除き、クライアントの呼び出しに関する情報は保持されません。 このルールを 1 つの例外があります。 サーバーの状態情報のみが収集されている場合でも、サーバー呼び出し内でクライアントの呼び出しに関する情報が保持されます。 これにより、複数のホップのまたがりメモリ割り当て呼び出しを追跡することができます。

クライアント呼び出し情報のセルにフィールドは次のとおりです。

<span id="ProcNum"></span><span id="procnum"></span><span id="PROCNUM"></span>**ProcNum**  
メソッドが呼び出されるプロシージャ番号 (netmon キャプチャ ファイルの場合は操作数)。 RPC ランタイムは、IDL ファイル内の位置番号で、インターフェイスから個々 のルーチンを識別します。 インターフェイスでは、最初のルーチンは、数字の 0、1、2 つ目および具合になります。

<span id="ServicingThread"></span><span id="servicingthread"></span><span id="SERVICINGTHREAD"></span>**ServicingThread**  
この呼び出しが行われますが、スレッドのセルの ID。

<span id="IfStart"></span><span id="ifstart"></span><span id="IFSTART"></span>**IfStart**  
通話が行わインターフェイス UUID の最初の dword 値です。

<span id="Endpoint"></span><span id="endpoint"></span><span id="ENDPOINT"></span>**エンドポイント**  
呼び出しが行われる、サーバー上のエンドポイントの最初の 12 文字。

呼び出しターゲット情報セル内のフィールドは次のとおりです。

<span id="ProtocolSequence"></span><span id="protocolsequence"></span><span id="PROTOCOLSEQUENCE"></span>**ProtocolSequence**  
この呼び出しのプロトコル順序を指定します。

<span id="LastUpdateTime"></span><span id="lastupdatetime"></span><span id="LASTUPDATETIME"></span>**LastUpdateTime**  
時間 (ミリ秒単位の起動後)、クライアントの呼び出しまたは呼び出しの対象に関する情報が更新された日時。

<span id="TargetServer"></span><span id="targetserver"></span><span id="TARGETSERVER"></span>**TargetServer**  
呼び出しが実行されるサーバーの名前の最初の 24 文字です。

 

 





