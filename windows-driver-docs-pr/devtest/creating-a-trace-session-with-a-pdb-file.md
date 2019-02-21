---
title: PDB ファイルを使用してトレース セッションを作成します。
description: PDB ファイルを使用してトレース セッションを作成します。
ms.assetid: dae78674-3563-4fd5-869b-abd4c13aa202
keywords:
- プログラム データベース シンボル ファイル WDK
- PDB シンボル ファイルの WDK
- シンボル ファイルの WDK ソフトウェア トレース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d08ac7b33e8fcc72ee185f9ff7ad9d96e40d481
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538781"
---
# <a name="creating-a-trace-session-with-a-pdb-file"></a>PDB ファイルを使用してトレース セッションを作成します。


## <span id="ddk_create_a_trace_session_with_a_pdb_file_tools"></span><span id="DDK_CREATE_A_TRACE_SESSION_WITH_A_PDB_FILE_TOOLS"></span>


トレース プロバイダーを指定する最も簡単な方法が検索するには、 [PDB シンボル ファイル](pdb-symbol-files.md)トレース プロバイダーを含むソース コード。 Traceview では、すべてのトレース セッションに PDB ファイルから必要な情報を抽出できます。

### <a name="span-idtocreateatracesessionwithapdbfilespanspan-idtocreateatracesessionwithapdbfilespanto-create-a-trace-session-with-a-pdb-file"></a><span id="to_create_a_trace_session_with_a_pdb_file"></span><span id="TO_CREATE_A_TRACE_SESSION_WITH_A_PDB_FILE"></span>PDB ファイルを使用してトレース セッションを作成するには

1.  [Traceview で開始](starting-and-exiting-traceview.md)します。

2.  **ファイル** メニューのをクリックして**Create New Log Session**します。

3.  クリックして**プロバイダーを追加する**します。

4.  をクリックして**PDB (Debug Information) ファイル**へのパスを入力し、 [PDB シンボル ファイル](pdb-symbol-files.md)はトレース プロバイダーのまたは、省略記号ボタンをクリックします (**.**)、ファイルに移動します。

5.  追加のプロバイダーを追加するには、クリックして**プロバイダーの追加**します。 この手順は省略可能です。

6.  **[次へ]** をクリックします。

7.  [フラグとレベルを選択します。](selecting-flags-and-levels.md)必要な場合、します。

8.  [基本的なトレース セッションのオプションを設定](setting-basic-trace-session-options.md)必要な場合、します。

9.  [詳細トレース セッションのオプションを設定する](setting-advanced-trace-session-options.md)必要な場合、します。

10. **[Finish]**(完了) をクリックします。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

指定した PDB ファイルに必要なトレース要素が含まれていない場合は traceview でに「PDB ファイルが見つかりません」エラー メッセージが表示されます。

Traceview でを使用して、Windows Server 2003 を実行しているコンピューター上の PDB ファイルを開き、traceview で自動的に終了します。

 





