---
title: 保護モードの機能
description: 保護モードの機能
ms.assetid: bf40d018-7804-47df-9064-fb6f86da4b33
keywords:
- モードでは、セキュリティで保護の概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d19327f671ac067d8703d8f454b6d4c0b0e3898
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379734"
---
# <a name="features-of-secure-mode"></a>保護モードの機能


## <span id="ddk_features_of_secure_mode_dbg"></span><span id="DDK_FEATURES_OF_SECURE_MODE_DBG"></span>


セキュリティで保護モードがアクティブの場合、すべてのコマンドに影響するために使用する、*ホスト*コンピューターが非アクティブ化し、シンボル サーバーとデバッガー拡張機能の制限があります。

保護モードの特定の効果は次のとおりです。

-   [ **.Attach (プロセスにアタッチ)**](-attach--attach-to-process-.md)、 [**に関する (プロセスの作成)**](-create--create-process-.md)、 [ **.detach (からデタッチします。プロセス)**](-detach--detach-from-process-.md)、 [ **.abandon (電話放棄呼プロセス)**](-abandon--abandon-process-.md)、 [ **.kill (Kill プロセス)**](-kill--kill-process-.md)、[ **.tlist (プロセス Id の一覧)**](-tlist--list-process-ids-.md)、 [ **.dump (ダンプ ファイルの作成)**](-dump--create-dump-file-.md)、 [ **.opendump (ダンプ ファイルを開く)**](-opendump--open-dump-file-.md)、 [ **.writemem (ファイルに書き込みメモリ)**](-writemem--write-memory-to-file-.md)、 [ **.netuse (コントロール ネットワーク接続)** ](-netuse--control-network-connections-.md)、および[ **.quit\_(ように偶発的な終了) ロック**](-quit-lock--prevent-accidental-quit-.md)コマンドは利用できません。

-   [ファイル |プロセスにアタッチする](file---attach-to-a-process.md)、[ファイル |実行可能ファイルを開く](file---open-executable.md)、[デバッグ |デバッグ対象をデタッチ](debug---detach-debuggee.md)、[デバッグ |デバッグを停止](debug---stop-debugging.md)、[ファイル |クラッシュ ダンプを開く](file---open-crash-dump.md)WinDbg メニュー コマンドは利用できません。

-   [ **.Shell (コマンド シェル)** ](-shell--command-shell-.md)コマンドは使用できません。

-   拡張 Dll は、ローカル ディスクから読み込む必要があります。これらは、UNC パスから読み込まれたにすることはできません。

-   拡張機能の 2 つの標準的な型のみの Dll (wdbgexts.h および dbgeng.h) が許可されます。 拡張機能としては、他の種類の Dll を読み込むことができません。

-   シンボル サーバーを使用している場合はいくつかの制限です。 SymSrv (symsrv.dll) のみが許可されます。その他のシンボル サーバー Dll は受け入れられません。 シンボルでは、ダウン ストリームのストアを使用できませんし、任意の既存のダウン ストリーム ストアは無視されます。 HTTP および HTTPS 接続が許可されていません。

アクティブになった後、保護モードをオフにすることはできません。 詳細については、「[をセキュリティで保護モードのアクティブ化する](activating-secure-mode.md)します。

 

 





