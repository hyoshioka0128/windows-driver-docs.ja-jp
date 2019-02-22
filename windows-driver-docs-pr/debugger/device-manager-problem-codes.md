---
title: デバイス マネージャーの問題のコード
description: デバイス マネージャーの問題のコード
ms.assetid: d08c3dd1-ab2e-4ce6-8bf7-9634c0a5be1f
keywords:
- プラグ アンド プレイ (PnP) デバイス マネージャーの問題のコード
- デバイス マネージャーの問題のコード
- CM_PROB_XXX
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: afa8b4fb0a8e88d71b3e8fe56cee8acf79bb0f84
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549883"
---
# <a name="device-manager-problem-codes"></a>デバイス マネージャーの問題のコード


デバイス マネージャーは、デバイスに問題があるときに、黄色の感嘆符 (!) を使用したデバイスをマークします。 問題のコードは形式 CM\_確率\_*XXX*ヘッダー ファイルの cfg.h に定義されています。 最も重要なは、次に説明へのマッピングと共に、[デバイス ノードの状態フラグ](device-node-status-flags.md)します。 詳細についてを参照してください[デバイス マネージャーのエラー メッセージ](../install/device-manager-error-messages.md)します。

<span id="Code_1__CM_PROB_NOT_CONFIGURED_"></span><span id="code_1__cm_prob_not_configured_"></span><span id="CODE_1__CM_PROB_NOT_CONFIGURED_"></span>**コードの 1 (CM\_確率\_いない\_構成済み)**  
デバイスがインストールされていない、以前にインストールされていないことを示します。 (DNF に対応する\_いない\_構成済みです)。

<span id="Code_10__CM_PROB_FAILED_START_"></span><span id="code_10__cm_prob_failed_start_"></span><span id="CODE_10__CM_PROB_FAILED_START_"></span>**コードの 10 (CM\_確率\_FAILED\_開始)**  
何らかの理由で、デバイスが開始されませんでしたが、I/O マネージャーが、一連のリソースで開始しようとしています。 ことを示します。 (DNF に対応する\_開始\_できませんでした)。

<span id="Code_12__CM_PROB_NORMAL_CONFLICT_"></span><span id="code_12__cm_prob_normal_conflict_"></span><span id="CODE_12__CM_PROB_NORMAL_CONFLICT_"></span>**12 のコード (CM\_確率\_標準\_競合)**  
このデバイスを開始するのに十分なリソースがないことを示します。 (DNF に対応する\_不十分\_リソースです)。

<span id="Code_14__CM_PROB_NEED_RESTART_"></span><span id="code_14__cm_prob_need_restart_"></span><span id="CODE_14__CM_PROB_NEED_RESTART_"></span>**コード 14 (CM\_確率\_必要\_再起動)**  
ユーザー モード デバイスの再構成、再起動が必要、変更を有効にすることを示します。 (DNF に対応する\_必要\_を再起動します)。

<span id="Code_18__CM_PROB_REINSTALL_"></span><span id="code_18__cm_prob_reinstall_"></span><span id="CODE_18__CM_PROB_REINSTALL_"></span>**18 のコード (CM\_確率\_を再インストール)**  
デバイスをインストールする必要があることを示しがインストールされています。 (DNF に対応する\_再インストールします)。

<span id="Code_21__CM_PROB_WILL_BE_REMOVED_"></span><span id="code_21__cm_prob_will_be_removed_"></span><span id="CODE_21__CM_PROB_WILL_BE_REMOVED_"></span>**21 のコード (CM\_確率\_は\_BE\_削除済み)**  
ユーザー モードがこのデバイスをアンインストールすることを示します。 (DNF に対応する\_は\_BE\_削除しました)。

<span id="Code_22__CM_PROB_DISABLED_"></span><span id="code_22__cm_prob_disabled_"></span><span id="CODE_22__CM_PROB_DISABLED_"></span>**コードの 22 (CM\_確率\_無効)**  
デバイスが無効になっていることを示します。 (DNF に対応する\_無効になっている)。

<span id="Code_28__CM_PROB_FAILED_INSTALL_"></span><span id="code_28__cm_prob_failed_install_"></span><span id="CODE_28__CM_PROB_FAILED_INSTALL_"></span>**コードの 28 (CM\_確率\_FAILED\_インストール)**  
存在して失敗したインストールがないこと、このデバイスを選択したドライバーが、カーネルが問題を報告しなかったことを示します (DNF がないと\_XXX がこの問題を一致)。 この問題は、INF ファイルはまだを内蔵型のシステム デバイス (ISA タイマー、ISA RTC、Ram、およびなど) の結果であることができます。

<span id="Code_31__CM_FAILED_ADD_"></span><span id="code_31__cm_failed_add_"></span><span id="CODE_31__CM_FAILED_ADD_"></span>**コード 31 (CM\_FAILED\_追加)**  
デバイスが追加されていないことを示します。 理由としては、エラーを含めることができます。 ドライバーの**AddDevice**ルーチンがエラーを返しました、サービスがレジストリにデバイスの一覧はありません、一覧には、複数のサービスがある、または制御するドライバーを読み込むことができませんでした。 (DNF に対応する\_追加\_できませんでした)。

 

 





