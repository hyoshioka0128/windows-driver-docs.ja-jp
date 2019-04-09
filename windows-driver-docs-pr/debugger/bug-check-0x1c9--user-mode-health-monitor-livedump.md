---
title: バグ チェック 0x1C9 USER_MODE_HEALTH_MONITOR_LIVEDUMP
description: USER_MODE_HEALTH_MONITOR_LIVEDUMP のバグ チェックでは、0x000001C9 の値を持ちます。 1 つまたは複数の重要なユーザー モード コンポーネントが正常性チェックを満たすために失敗したことを示します。
keywords:
- バグ チェック 0x1C9 USER_MODE_HEALTH_MONITOR_LIVEDUMP
- USER_MODE_HEALTH_MONITOR_LIVEDUMP
ms.date: 01/10/2019
topic_type:
- apiref
api_name:
- USER_MODE_HEALTH_MONITOR_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 890058b3e990d1a96312070fe7fe3e55f8416c08
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239709"
---
# <a name="bug-check-0x1c9-usermodehealthmonitorlivedump"></a>バグ チェック 0x1C9:ユーザー\_モード\_ヘルス\_モニター\_LIVEDUMP

ユーザー\_モード\_ヘルス\_モニター\_LIVEDUMP バグ チェックが 0x000001C9 の値を持ちます。 1 つまたは複数の重要なユーザー モード コンポーネントが正常性チェックを満たすために失敗したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

 

## <a name="usermodehealthmonitorlivedump-parameters"></a>ユーザー\_モード\_ヘルス\_モニター\_LIVEDUMP パラメーター

|パラメーター|説明|
|--- |--- |
|1| 構成されたタイムアウト内で正常性チェックを満たすために失敗したプロセスです。| 
|2| 正常性のタイムアウト (秒) を監視します。| 
|3| ウォッチドッグのソース。 プロセスのアドレスと組み合わせてこれは、ソースの識別に役立ちます。 使用できる値については後述します。 これらの値が共有[USER_MODE_HEALTH_MONITOR](bug-check-0x9e--user-mode-health-monitor.md)します。| 
|4| 予約済み。 |

**ウォッチドッグのソースの値**

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

## <a name="cause"></a>原因
-----
1 つまたは複数の重要なユーザー モード コンポーネントは、正常性チェックを満たすために失敗しました。
 
ウォッチドッグのタイマーなどのハードウェア メカニズムでは、カーネルの基本的なサービスが実行されていないことを検出できます。 ただし、リソースの枯渇問題は、メモリ リーク、ロックの競合、およびスケジューリング優先順位の構成が正しくない可能性がありますブロックの重要なユーザー モード コンポーネントせずに、Dpc または非ページ プールのドレインなど。 

カーネル コンポーネントは、重要なアプリケーションを定期的に監視することによってユーザー モードにウォッチドッグ タイマー機能を拡張できます。 この livedump では、このアプリケーションの終了を試みるし、時間で終了が完了した場合の監視が保持されますになるような方法でユーザー モードの正常性チェックが失敗したことを示します。 時間内に終了が完了しない場合、マシンは重要なサービスの再起動やその他のサーバーにアプリケーションのフェールオーバーを許可して復元 bugchecked になります。 

(このコードは、実際のバグチェックには使用されません。 ライブ ダンプの識別に使用されます)。


## <a name="see-also"></a>関連項目
----------

[バグ チェック コード リファレンス](bug-check-code-reference2.md)

