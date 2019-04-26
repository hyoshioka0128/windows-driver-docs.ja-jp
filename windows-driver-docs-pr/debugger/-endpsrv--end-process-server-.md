---
title: .endpsrv (プロセス サーバーの終了)
description: .Endpsrv コマンドでは、現在のプロセス サーバー、または閉じる KD 接続のサーバーを実行します。
ms.assetid: 3f8d0a85-f0f4-4c13-ab52-e4d99ba3599c
keywords:
- .endpsrv (エンド プロセス サーバー) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .endpsrv (End Process Server)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9339a9aaf2d51e9b7f9a2d13b1ee0685543f660b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337219"
---
# <a name="endpsrv-end-process-server"></a>.endpsrv (プロセス サーバーの終了)


**.Endpsrv**コマンドにより、現在のプロセス サーバー、または KD 接続のサーバーを閉じます。

```dbgcmd
.endpsrv 
```

## <span id="ddk_meta_end_process_server_dbg"></span><span id="DDK_META_END_PROCESS_SERVER_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

このコマンドは、リモート デバッグのプロセス サーバー、または KD 接続のサーバーを実行している場合にのみ使用できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

これらのサーバーの詳細については、次を参照してください[プロセス サーバー (ユーザー モード)](process-servers--user-mode-.md)または[KD 接続サーバー (カーネル モード)。](kd-connection-servers--kernel-mode-.md)

<a name="remarks"></a>注釈
-------

**.Endpsrv**プロセス サーバー、または KD 接続のサーバーが現在、スマート クライアントに接続して、コマンドが終了します。

プロセス サーバー、またはが実行されているコンピューターから KD 接続のサーバーを終了する場合は、タスク マネージャーを使用して、(dbgsrv.exe または kdsrv.exe) プロセスを終了します。

**.Endpsrv**コマンドは、プロセス サーバー、または KD 接続のサーバーを終了できますが、デバッグ サーバーを終了できません。 その方法については、次を参照してください。[リモート デバッグ セッションを制御する](controlling-a-remote-debugging-session.md)します。

 

 





