---
title: NT カーネル ロガーのトレース セッションを作成します。
description: NT カーネル ロガーのトレース セッションを作成します。
ms.assetid: 606156b9-8ad9-4510-9929-4f0e3b7a3134
keywords:
- WDK、NT Kernel Logger のセッションをトレースします。
- トレース セッションの NT Kernel Logger WDK
- Windows カーネル トレース プロバイダー WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 977319c35e40e713e6cbe02cc4b569d1aeee0369
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551909"
---
# <a name="creating-an-nt-kernel-logger-trace-session"></a>NT カーネル ロガーのトレース セッションを作成します。

## <span id="ddk_create_a_real_time_nt_kernel_logger_trace_session_tools"></span><span id="DDK_CREATE_A_REAL_TIME_NT_KERNEL_LOGGER_TRACE_SESSION_TOOLS"></span>

Traceview では、作成に使用できる、[トレース セッションの NT Kernel Logger](nt-kernel-logger-trace-session.md)、トレース セッションが、Windows カーネルによって生成されるイベントを記録する Windows に組み込まれています。

NT Kernel Logger のトレース セッションを作成するときに"Process"などのシステム イベントのカテゴリを選択することができます。 Traceview では、そのカテゴリ内のすべてのシステム イベントを記録するトレース セッションを構成します。

### <a name="span-idtocreateanntkernelloggertracesessionspanspan-idtocreateanntkernelloggertracesessionspanto-create-an-nt-kernel-logger-trace-session"></a><span id="to_create_an_nt_kernel_logger_trace_session"></span><span id="TO_CREATE_AN_NT_KERNEL_LOGGER_TRACE_SESSION"></span>NT カーネル ロガーのトレース セッションを作成するには

1.  [Traceview で開始](starting-and-exiting-traceview.md)します。

2.  **ファイル** メニューのをクリックして**Create New Log Session**します。

3.  クリックして**プロバイダーを追加する**します。

4.  をクリックして**Kernel Logger**、NT Kernel Logger セッションのイベントの種類を特定し、をクリックするチェック ボックスを 1 つ以上選択**OK**します。

5.  **オープン** ダイアログ ボックスで System.tmf、システムのイベントのトレース メッセージの形式 (TMF) ファイルを見つけます。 ツールの WDK に含まれる System.tmf\\トレース サブディレクトリ。

6.  任意の型の追加のプロバイダーを追加するには、次のようにクリックします。**プロバイダーの追加**します。 この手順は省略可能です。

7.  **[次へ]** をクリックします。

8.  [基本的なトレース セッションのオプションを設定](setting-basic-trace-session-options.md)必要な場合、します。

9.  [詳細トレース セッションのオプションを設定する](setting-advanced-trace-session-options.md)必要な場合、します。

10. **[Finish]**(完了) をクリックします。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

NT Kernel Logger のトレース セッションの一覧に表示されます、**という名前のプロバイダーの選択**「Windows カーネル トレース」として ダイアログ ボックス いずれかを使用することができます、**という名前のプロバイダーの選択** ダイアログ ボックスまたは**Kernel Logger**オプション、**プロバイダー コントロールの GUID セットアップ**NT Kernel Logger を作成する ダイアログ ボックストレース セッションです。 ただし、のみ、**プロバイダー コントロールの GUID セットアップ** ダイアログ ボックスを使用してトレース対象のカーネル コンポーネントを選択できます。 使用しての詳細については、**という名前のプロバイダーの選択**ダイアログ ボックスを参照してください[登録済みのプロバイダーのトレース セッションを作成する](creating-a-trace-session-for-a-registered-provider.md)します。
