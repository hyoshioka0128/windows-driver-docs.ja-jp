---
title: バグ チェック 0x9E USER_MODE_HEALTH_MONITOR
description: USER_MODE_HEALTH_MONITOR のバグ チェックでは、エラー 0x0000009e が発生の値を持ちます。 このバグ チェックでは、1 つまたは複数の重要なユーザー モード コンポーネントが正常性チェックを満たすために失敗したことを示します。
ms.assetid: 5ad56234-5150-4acb-828d-198c2e5fb9b6
keywords:
- バグ チェック 0x9E USER_MODE_HEALTH_MONITOR
- USER_MODE_HEALTH_MONITOR
ms.date: 12/26/2018
topic_type:
- apiref
api_name:
- USER_MODE_HEALTH_MONITOR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 18c711a3024b804c88c7375617ed3a00f2264da9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324673"
---
# <a name="bug-check-0x9e-usermodehealthmonitor"></a>バグ チェック 0x9E:ユーザー\_モード\_ヘルス\_モニター


ユーザー\_モード\_ヘルス\_モニターのバグ チェックがエラー 0x0000009e が発生の値を持ちます。 このバグ チェックでは、1 つまたは複数の重要なユーザー モード コンポーネントが正常性チェックを満たすために失敗したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="usermodehealthmonitor-parameters"></a>ユーザー\_モード\_ヘルス\_モニタのパラメータ


|パラメーター|説明|
|--- |--- |
|1|指定されたタイムアウトの正常性チェックを満たすために失敗したプロセス|
|2|タイムアウトを秒単位で監視の正常性|
|3|ウォッチドッグのソース。 プロセスと組み合わせてアドレスはどのようなサブコンポーネントがこのウォッチドッグを作成したを識別するために役立ちます。 以下に示す値。|
|4|予約済み|
 

**VALUES** 

```text
        0  : WatchdogSourceDefault
              Source was not specified
        1  : WatchdogSourceRhsCleanup
              Monitors that RHS process goes away when
              terminating on graceful exit
        2  : WatchdogSourceRhsResourceDeadlockBugcheckNow
              RHS was asked to immediately bugcheck machine
              on resource deadlock
        3  : WatchdogSourceRhsExceptionFromResource
              Resource has leaked unhandled exception from an entry point,
              RHS is terminating and this watchdog monitors that
              process will go away
        4  : WatchdogSourceRhsUnhandledException
              Unhandled exception in RHS.
              RHS is terminating and this watchdog monitors that
              process will go away
        5  : WatchdogSourceRhsResourceDeadlock
              Monitors that RHS process goes away when
              terminating on resource deadlock
        6  : WatchdogSourceRhsResourceTypeDeadlock
              Monitors that RHS process goes away when
              terminating on resource type deadlock
        7  : WatchdogSourceClussvcUnhandledException
              Unhandled exception in clussvc.
              clussvc is terminating and this watchdog monitors that
              process will go away
        8  : WatchdogSourceClussvcBugcheckMessageRecieved
              Another cluster node has sent message asking to bugcheck this node.
        9  : WatchdogSourceClussvcWatchdogBugcheck
              User mode watchdog has expired and created netft watchdog
              to bugchecked the node.
       0xA : WatchdogSourceClussvcIsAlive
              Cluster service sends heartbeat to netft every 500 millseconds.
              By default, netft expects at least 1 heartbeat per second.
              If this watchdog was triggered that means clussvc is not getting
              CPU to send heartbeats.
      0x65 : WatchdogSourceRhsResourceDeadlockPhysicalDisk
               A subclass of WatchdogSourceRhsResourceDeadlock.
      0x66 : WatchdogSourceRhsResourceDeadlockStoragePool
               A subclass of WatchdogSourceRhsResourceDeadlock.
      0x67 : WatchdogSourceRhsResourceDeadlockFileServer
               A subclass of WatchdogSourceRhsResourceDeadlock.
      0x68 : WatchdogSourceRhsResourceDeadlockSODAFileServer
               A subclass of WatchdogSourceRhsResourceDeadlock.
      0x69 : WatchdogSourceRhsResourceDeadlockStorageReplica
               A subclass of WatchdogSourceRhsResourceDeadlock.
      0x6A : WatchdogSourceRhsResourceDeadlockStorageQOS
               A subclass of WatchdogSourceRhsResourceDeadlock.
      0x6B : WatchdogSourceRhsResourceDeadlockStorageNFSV2
               A subclass of WatchdogSourceRhsResourceDeadlock.
      0xC9 : WatchdogSourceRhsResourceTypeDeadlockPhysicalDisk
               A subclass of WatchdogSourceRhsResourceTypeDeadlock.
      0xCA : WatchdogSourceRhsResourceTypeDeadlockStoragePool
               A subclass of WatchdogSourceRhsResourceTypeDeadlock.
      0xCB : WatchdogSourceRhsResourceTypeDeadlockFileServer
               A subclass of WatchdogSourceRhsResourceTypeDeadlock.
      0xCC : WatchdogSourceRhsResourceTypeDeadlockSODAFileServer
               A subclass of WatchdogSourceRhsResourceTypeDeadlock.
      0xCD : WatchdogSourceRhsResourceTypeDeadlockStorageReplica
               A subclass of WatchdogSourceRhsResourceTypeDeadlock.
      0xCE : WatchdogSourceRhsResourceTypeDeadlockStorageQOS
               A subclass of WatchdogSourceRhsResourceTypeDeadlock.
      0xCF : WatchdogSourceRhsResourceTypeDeadlockStorageNFSV2
               A subclass of WatchdogSourceRhsResourceTypeDeadlock.
```

<a name="cause"></a>原因
-----

ウォッチドッグのタイマーなどのハードウェアのメカニズムでは、カーネルの基本的なサービスが実行されていないことを検出できます。 ただし、リソースの枯渇を (メモリ リーク、ロックの競合、および優先順位の構成の誤りをスケジュール設定) を含む発行呼び出し (Dpc) の遅延プロシージャをブロックせずに、重要なユーザー モード コンポーネントをブロックできますか、非ページ プールをドレインします。

カーネル コンポーネントは、重要なアプリケーションを定期的に監視することによってユーザー モードにウォッチドッグ タイマー機能を拡張できます。 このバグ チェックでは、正常なシャット ダウンを妨げる方法でユーザー モードの正常性チェックが失敗したことを示します。 このバグ チェックでは、再起動するか、他のサーバーにアプリケーションのフェールオーバーを有効にする重要なサービスを復元します。



 

 




