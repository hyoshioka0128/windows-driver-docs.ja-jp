---
title: カーネル ネットワーク ミニリダイレクター ドライバー
description: カーネル ネットワーク ミニリダイレクター ドライバー
ms.assetid: 13236e5f-1261-4cf1-9c3d-3f1a5ccb3323
keywords:
- ネットワークリダイレクター WDK、ミニリダイレクタードライバー
- リダイレクタードライバー WDK、ミニリダイレクタードライバー
- カーネルネットワークリダイレクター WDK、ミニリダイレクタードライバー
- ミニリダイレクター WDK
- ミニリダイレクター WDK、カーネルネットワークミニリダイレクタードライバーについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b3c970eaf61f7d6017eb965f6b5a0dcf30836cb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840952"
---
# <a name="the-kernel-network-mini-redirector-driver"></a>カーネル ネットワーク ミニリダイレクター ドライバー


## <span id="ddk_the_kernel_network_mini_redirector_driver_if"></span><span id="DDK_THE_KERNEL_NETWORK_MINI_REDIRECTOR_DRIVER_IF"></span>


カーネルネットワークミニリダイレクタードライバーは、リダイレクトされたドライブバッファリングサブシステム (RDBSS) がドライバーと通信するために使用する多数のコールバックルーチンを実装します。 このドキュメントの残りの部分では、カーネルネットワークミニリダイレクタードライバーをネットワークミニリダイレクタードライバーと呼びます。

ネットワークミニリダイレクタードライバーが最初に起動したとき (その**Driverentry**ルーチン内)、ドライバーは RDBSS [**RxRegisterMinirdr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxregisterminirdr)ルーチンを呼び出して、ネットワークミニリダイレクタードライバーを RDBSS に登録します。 ネットワークミニリダイレクタードライバーは、MINIRDR\_ディスパッチ構造体を渡します。これには、構成データと、ネットワークミニリダイレクタードライバーによって実装されるルーチンへのポインター (ディスパッチテーブル) が含まれます。

ネットワークミニリダイレクターは、これらのルーチンの一部のみを実装することを選択できます。 ネットワークミニリダイレクターによって実装されていないルーチンは、 **RxRegisterMinirdr**に渡される minirdr\_ディスパッチ構造体内の**NULL**ポインターに設定する必要があります。 RDBSS は、ネットワークミニリダイレクターによって実装されたルーチンのみを呼び出します。

ネットワークミニリダイレクターによって実装されるルーチンの特別なカテゴリの1つに、読み取り、書き込み、およびその他のファイル操作のための従来のファイル i/o 呼び出しを表す低 i/o 操作があります。 すべての低 i/o ルーチンは、RDBSS によって非同期的に呼び出すことができます。 ネットワークミニリダイレクター用のカーネルドライバーは、実装されているすべての低 i/o ルーチンを安全に非同期的に呼び出すことができるようにする必要があります。 Low i/o ルーチンは、 [**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンからの minirdr\_ディスパッチ構造体の一部として、ルーチンポインターの配列として渡されます。 配列エントリの値は、実行する低 i/o 操作です。 すべての低 i/o ルーチンは、RX\_コンテキスト構造体へのポインターをパラメーターとして渡すことを想定しています。 RX\_コンテキストデータ構造体には、実行する低 i/o 操作を指定する**Lowiocontext (操作**) メンバーがあります。 この**Lowiocontext**は、要求された低 i/o 操作を指定するために使用できる、低 i/o ルーチンのいくつかが、ネットワークミニリダイレクタードライバーで同じルーチンを指している可能性があります。 たとえば、ファイルロックに関連するすべての低 i/o 呼び出しで、ネットワークミニリダイレクターで同じ低 i/o ルーチンを呼び出すことができます。また、このルーチンでは、要求されたロックまたはロック解除操作を指定するために**Lowiocontext. operation**メンバーを使用できます。

また、RDBSS は、ネットワークミニリダイレクターによって実装される他のいくつかのルーチンの非同期操作も想定しています。 これらのルーチンは、リモートリソースとの接続を確立するために使用されます。 接続操作の完了にはかなりの時間がかかるため、RDBSS はこれらのルーチンが非同期操作として実装されていると想定しています。

RDBSS は、低 i/o と接続関連のルーチン以外のネットワークミニリダイレクターによって実装されたすべてのルーチンが、同期呼び出しに基づいていることを前提としています。 ただし、これは Windows オペレーティングシステムの将来のリリースで変更される可能性があります。

ネットワークミニリダイレクターによって実装されるすべてのルーチンは、完了時に NTSTATUS 値を返します。 ほとんどのルーチンは、正常に完了したか、適切な NTSTATUS 値を\_状態を返します。 特定のルーチンに固有の戻り値に加えて、ほとんどのルーチンで返すことができるエラーの汎用カテゴリが2つあります。

-   ネットワーク エラー

-   認証エラー

次のようなネットワークエラーが考えられます。

<span id="STATUS_IO_TIMEOUT"></span><span id="status_io_timeout"></span>状態\_IO\_タイムアウト  
リモートサーバーへの i/o 要求がタイムアウトしました。

<span id="STATUS_BAD_NETWORK_PATH"></span><span id="status_bad_network_path"></span>状態\_無効\_ネットワーク\_パス  
I/o 要求が、存在しないネットワークパスに対して行われました。 このエラーは、ディレクトリの名前が変更されたか、削除された場合に発生する可能性があります。

<span id="STATUS_NETWORK_UNREACHABLE"></span><span id="status_network_unreachable"></span>ネットワーク\_到達できない状態\_  
クライアントからネットワークに到達できません。

<span id="STATUS_REMOTE_NOT_LISTENING"></span><span id="status_remote_not_listening"></span>リモート\_\_リッスンしていない状態\_  
リモートサーバーが接続をリッスンしていません。

<span id="STATUS_USER_SESSION_DELETED"></span><span id="status_user_session_deleted"></span>\_ユーザー\_セッション\_削除された状態  
サーバー上のユーザーセッションが削除されました。 セッションがタイムアウトしたか、サーバーが再起動されたため、既存のすべてのユーザーセッションが削除されたか、またはサーバーの管理者がユーザーセッションを強制的に削除した可能性があります。

<span id="STATUS_CONNECTION_DISCONNECTED"></span><span id="status_connection_disconnected"></span>状態\_接続\_切断  
リモートサーバーへの接続が切断されました。

<span id="STATUS_NETWORK_NAME_DELETED"></span><span id="status_network_name_deleted"></span>状態\_ネットワーク\_名\_削除されました  
I/o 要求は、削除されたネットワーク名を対象としています。

次のような認証エラーが発生する可能性があります。

<span id="STATUS_LOGON_FAILURE"></span><span id="status_logon_failure"></span>ステータス\_ログオン\_失敗  
リモートサーバーへのログイン要求が失敗しました。

<span id="STATUS_NETWORK_CREDENTIAL_CONFLICT"></span><span id="status_network_credential_conflict"></span>状態\_ネットワーク\_の資格情報\_競合  
提示されたネットワーク資格情報と競合が発生しました。

<span id="STATUS_DOWNGRADE_DETECTED"></span><span id="status_downgrade_detected"></span>ステータス\_ダウングレード\_検出されました  
サーバーとの通信にクライアントが使用するネットワークプロトコルの変更がサーバーによって検出され、変更が古いバージョンのプロトコルに変更されました。

<span id="STATUS_LOGIN_WKSTA_RESTRICTION"></span><span id="status_login_wksta_restriction"></span>ステータス\_ログイン\_WKSTA\_制限  
サーバーへのワークステーションログインには制限があります。

次のセクションでは、ネットワークミニリダイレクターで実装できるルーチンの詳細について説明します。

[カーネルネットワークミニリダイレクターによって実装されるルーチン](routines-implemented-by-the-kernel-network-mini-redirector.md)

[RDBSS によって使用されないルーチン](routines-not-used-by-rdbss.md)

ネットワークミニリダイレクターによって実装されるルーチンは、機能に基づいて次のカテゴリに分類できます。

[接続と名前解決](connection-and-name-resolution.md)

[ドライバーの開始、停止、デバイス制御](driver-start--stop--and-device-control.md)

[ファイルシステムオブジェクトの作成と削除](file-system-object-creation-and-deletion.md)

[ファイルシステムオブジェクトの i/o ルーチン](file-system-object-i-o-routines.md)

[ファイルシステムオブジェクトのクエリと Set ルーチン](file-system-object-query-and-set-routines.md)

[その他のネットワークミニリダイレクタールーチン](miscellaneous-network-mini-redirector-routines.md)

 

 




