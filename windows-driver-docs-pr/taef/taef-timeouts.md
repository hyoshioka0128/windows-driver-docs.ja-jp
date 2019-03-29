---
title: TAEF タイムアウト
description: TAEF タイムアウト
ms.assetid: 43FE81A2-71DF-4e3a-998E-1B1F8C1398AC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19b4aa6ed9f767e57cfeff6c1f2a65d76c00febb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581008"
---
# <a name="taef-timeouts"></a>TAEF タイムアウト


TAEF タイムアウトは、次の形式で指定します。*\[1 日です。\]時間\[: 分\[: 2 つ目\[します。FractionalSeconds\]\]\]* します。

例:

*0:0:0.5*  
.5 秒のタイムアウトを指定します。

<span id="0_0_45"></span>*0:0:45*  
45 秒のタイムアウトを指定します。

<span id="0_20_or_0_20_0"></span><span id="0_20_OR_0_20_0"></span>*0:20*または*0:20:0*  
20 分のタイムアウトを指定します。

<span id="5_or_5_0_or_5_0_0"></span><span id="5_OR_5_0_OR_5_0_0"></span>*5*または*5:0*または*5:0:0*  
5 つの時間のタイムアウトを指定します。

<span id="1.2_or_1.2_0_or_1.2_0_0"></span><span id="1.2_OR_1.2_0_OR_1.2_0_0"></span>*1.2*または*1.2:0*または*1.2:0:0*  
1 日 2 時間のタイムアウトを指定します。

## <a name="span-idsessiontime-outsspanspan-idsessiontime-outsspanspan-idsessiontime-outsspansession-time-outs"></a><span id="Session_Time-outs"></span><span id="session_time-outs"></span><span id="SESSION_TIME-OUTS"></span>セッションのタイムアウト


使用する場合、Te.exe の実行全体のセッションのタイムアウトを指定できます、 **/sessionTimeout**オプション。 タイムアウトに達すると、テスト セッションが正常に停止、および[プロセス終了コード](exit-codes-for-taef.md)タイムアウトが発生したことを示します。

<span id="te.exe_test1.dll__sessionTimeout_0_20"></span><span id="te.exe_test1.dll__sessiontimeout_0_20"></span><span id="TE.EXE_TEST1.DLL__SESSIONTIMEOUT_0_20"></span>te.exe test1.dll /sessionTimeout:0:20  
テスト全体のセッションが 20 分後にタイムアウトになります。

## <a name="span-idtesttime-outsspanspan-idtesttime-outsspanspan-idtesttime-outsspantest-time-outs"></a><span id="Test_Time-outs"></span><span id="test_time-outs"></span><span id="TEST_TIME-OUTS"></span>テストのタイムアウト


指定されたテスト アセンブリ、クラスまたはメソッドにタイムアウトのメタデータを適用することで、テストのタイムアウトを指定できます。

さらに、メタデータのタイムアウト値は/testTimeout オプションを使用するときに、実行時にオーバーライドできます。 指定した場合、/testTimeout は Te.exe の実行全体のグローバルのテストのタイムアウトを設定します。

**注:** 組み合わせて使用すると、テストのタイムアウトは無視されます[/inproc](te-exe-command-line-parameters.md#inproc)します。

<span id="te.exe_test1.dll__testTimeout_0_0_45"></span><span id="te.exe_test1.dll__testtimeout_0_0_45"></span><span id="TE.EXE_TEST1.DLL__TESTTIMEOUT_0_0_45"></span>te.exe test1.dll/testTimeout:0:0:45  
すべてのテストとセットアップ/クリーンアップ メソッドは、45 秒後にタイムアウトします。

 

 





