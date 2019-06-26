---
title: カーネル ネットワーク ミニリダイレクター ドライバー
description: カーネル ネットワーク ミニリダイレクター ドライバー
ms.assetid: 13236e5f-1261-4cf1-9c3d-3f1a5ccb3323
keywords:
- ネットワーク リダイレクター WDK、ミニ リダイレクター ドライバー
- リダイレクター ドライバー WDK、ミニ リダイレクター ドライバー
- カーネル ネットワーク リダイレクター WDK、ミニ リダイレクター ドライバー
- ミニ リダイレクター WDK
- ミニ リダイレクター WDK、カーネル ネットワーク ミニ リダイレクター ドライバーについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e1e5466e526e58b9c261b68cdb2d541df3f669e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354669"
---
# <a name="the-kernel-network-mini-redirector-driver"></a>カーネル ネットワーク ミニリダイレクター ドライバー


## <span id="ddk_the_kernel_network_mini_redirector_driver_if"></span><span id="DDK_THE_KERNEL_NETWORK_MINI_REDIRECTOR_DRIVER_IF"></span>


カーネル ネットワーク ミニ リダイレクター ドライバーでは、数によって、リダイレクトされたドライブのバッファリング サブシステム (RDBSS) ドライバーとの通信に使用されるコールバック ルーチンを実装します。 このドキュメントの残りの部分でカーネル ネットワーク ミニ リダイレクター ドライバーをネットワークのミニ リダイレクター ドライバーとして指す場合は。

ネットワークのミニ リダイレクター ドライバーを最初に起動すると (でその**DriverEntry**ルーチン)、ドライバーの呼び出し、RDBSS [ **RxRegisterMinirdr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxregisterminirdr)ルーチンをネットワークに登録RDBSS とミニ リダイレクター ドライバー。 ネットワークのミニ リダイレクター ドライバーが、MINIRDR で合格\_ディスパッチ構造は、ネットワークのミニ リダイレクター ドライバー (ディスパッチ テーブル) を実装するルーチンへのポインターと共に構成データが含まれています。

ネットワークのミニ リダイレクターは、これらのルーチンの一部のみを実装するために選択できます。 ネットワークのミニ リダイレクターが実装されていない任意のルーチンに設定する必要があります、 **NULL** 、MINIRDR でポインター\_にディスパッチ構造体が渡される**RxRegisterMinirdr**します。 RDBSS だけネットワーク ミニリダイレクターによって実装されるルーチンを呼び出します。

ネットワークのミニ リダイレクターによって実装されるルーチンの 1 つの特殊なカテゴリは、従来のファイル I/O を読み取り、書き込み、およびその他のファイル操作の呼び出しを表す低い I/O 操作を示します。 すべて低い I/O ルーチンは、RDBSS から非同期的に呼び出すことができます。 ネットワークのミニ リダイレクターのカーネル ドライバーに実装されている、低い I/O ルーチン呼び出すことができますに安全に非同期的に特定ください。 低い I/O ルーチンは、日常的なポインターの配列としての MINIRDR の一部としてに渡されるで\_からディスパッチ構造、 [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチン。 配列エントリの値は、低の I/O 操作を実行します。 RX へのポインターを期待すべて低い I/O ルーチンの\_をパラメーターとして渡されるコンテキストの構造体。 RX\_コンテキスト データ構造には、 **LowIoContext.Operation**メンバーも、低の I/O 操作を実行するを指定します。 このネットワーク ミニ リダイレクター ドライバーに同じルーチンを指す低い I/O ルーチンのいくつかの可能性が**LowIoContext.Operation**メンバーを使用して、要求された低い I/O 操作を指定することができます。 たとえば、ネットワーク ミニリダイレクターで同じ低い I/O ルーチンを呼び出すすべてのファイルのロックに関連した低い I/O 呼び出しの可能性があり、このルーチンを使用できます、 **LowIoContext.Operation**ロックを指定するか、操作のロックを解除するにはメンバー要求されました。

RDBSS には、ネットワークのミニ リダイレクターによって実装されるその他のいくつかのルーチンの非同期操作も前提としています。 これらのルーチンは、リモート リソースへの接続を確立するために使用されます。 所要時間の非常に長い時間がかかる場合、接続操作であるために、これらのルーチンは、非同期操作として実装 RDBSS が前提とします。

RDBSS では、低い I/O と接続関連のルーチン以外、ネットワーク ミニ リダイレクターによって実装されるすべてのルーチンが同期呼び出しに基づくことを前提としています。 ただし、これは、Windows オペレーティング システムの将来のリリースで変更します。

すべてのネットワークのミニ リダイレクターによって実装されるルーチンは、完了時に NTSTATUS 値を返します。 ルーチンのほとんどが状態を返す\_成功または適切な NTSTATUS 値に成功しました。 特定のルーチンに固有の戻り値、だけでなく、ほとんどのルーチンに対して返されるエラーの一般的な 2 つのカテゴリがあります。

-   ネットワーク エラー

-   認証エラー

可能なネットワーク エラーを以下に示します。

<span id="STATUS_IO_TIMEOUT"></span><span id="status_io_timeout"></span>ステータス\_IO\_タイムアウト  
リモート サーバーへの I/O 要求がタイムアウトしました。

<span id="STATUS_BAD_NETWORK_PATH"></span><span id="status_bad_network_path"></span>ステータス\_不良\_ネットワーク\_パス  
I/O 要求が存在しないネットワーク パスにしました。 このエラーは、ディレクトリが名前を変更または削除された場合に発生することができます。

<span id="STATUS_NETWORK_UNREACHABLE"></span><span id="status_network_unreachable"></span>ステータス\_ネットワーク\_到達不能  
ネットワークでは、クライアントから到達できません。

<span id="STATUS_REMOTE_NOT_LISTENING"></span><span id="status_remote_not_listening"></span>ステータス\_リモート\_いない\_リッスン中  
リモート サーバーが接続をリッスンしていません。

<span id="STATUS_USER_SESSION_DELETED"></span><span id="status_user_session_deleted"></span>ステータス\_ユーザー\_セッション\_削除済み  
サーバー上のユーザー セッションが削除されました。 セッションがタイムアウトしたか、サーバーが再起動されていない既存のすべてのユーザー セッションが削除される原因とまたはユーザー セッションを削除してから、サーバーの管理者を強制がある場合があります。

<span id="STATUS_CONNECTION_DISCONNECTED"></span><span id="status_connection_disconnected"></span>ステータス\_接続\_切断  
リモート サーバーへの接続が切断されました。

<span id="STATUS_NETWORK_NAME_DELETED"></span><span id="status_network_name_deleted"></span>ステータス\_ネットワーク\_名前\_削除済み  
I/O 要求が削除されているネットワーク名の要求です。

認証エラーを以下に示します。

<span id="STATUS_LOGON_FAILURE"></span><span id="status_logon_failure"></span>ステータス\_ログオン\_エラー  
リモート サーバーにログイン要求が失敗しました。

<span id="STATUS_NETWORK_CREDENTIAL_CONFLICT"></span><span id="status_network_credential_conflict"></span>ステータス\_ネットワーク\_資格情報\_競合  
示されているネットワーク資格情報との競合が発生しました。

<span id="STATUS_DOWNGRADE_DETECTED"></span><span id="status_downgrade_detected"></span>ステータス\_ダウン グレード\_検出  
サーバーによって、クライアント サーバーとの通信に使用するネットワーク プロトコルの変更が検出されましたし、プロトコルの古いバージョンに変更が元にします。

<span id="STATUS_LOGIN_WKSTA_RESTRICTION"></span><span id="status_login_wksta_restriction"></span>ステータス\_ログイン\_WKSTA\_制限  
サーバーへのログインのワークステーション上の制限があります。

次のセクションでは、ネットワーク ミニ リダイレクターで実装できるルーチンの詳細について説明します。

[カーネル ネットワーク Mini-redirector によって実装されるルーチン](routines-implemented-by-the-kernel-network-mini-redirector.md)

[ルーチン RDBSS では使用されません。](routines-not-used-by-rdbss.md)

ネットワークのミニ リダイレクターによって実装されるルーチンは、関数に基づいて、次のカテゴリに整理できます。

[接続と名前解決](connection-and-name-resolution.md)

[ドライバーの起動、停止、およびデバイスの制御](driver-start--stop--and-device-control.md)

[ファイル システム オブジェクトの作成と削除](file-system-object-creation-and-deletion.md)

[ファイル システム オブジェクト I/O ルーチン](file-system-object-i-o-routines.md)

[ファイル システム オブジェクトのクエリおよび Set ルーチン](file-system-object-query-and-set-routines.md)

[その他のネットワーク Mini-redirector ルーチン](miscellaneous-network-mini-redirector-routines.md)

 

 




