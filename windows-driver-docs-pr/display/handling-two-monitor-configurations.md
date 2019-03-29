---
title: 2 つのモニター構成の処理
description: 2 つのモニター構成の処理
ms.assetid: 224ebc3f-dace-4b41-bfc8-6fd81c8b309d
keywords:
- TMM WDK の表示、2 つのモニターの構成
- モニターの構成の WDK 表示、2 つのモニター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 193c4aec148cdc4b5a1d92410aae083e2a0ad58d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572036"
---
# <a name="handling-two-monitor-configurations"></a>2 つのモニター構成の処理


2 つのモニターの構成には、TMM ダイアログが生成されます。 2 つのターゲットが同じグラフィックス アダプターの一部である場合は、TMM は両方のターゲットにターゲットのいずれかに現在割り当てられている 1 つのソースにマップします。 TMM がマッピングを実行した後、TMM ダイアログ ボックスがポップアップ表示します。 ターゲットがさまざまなグラフィックス アダプターである場合は、TMM ダイアログが 2 つ目のモニターをアクティブ化しないまま表示されます。 このような状況では、TMM ダイアログは複製のオプションはありませんまたは拡張できます。

次の順序は、TMM がのメソッドを呼び出す順序を示しています。 [IViewHelper](https://msdn.microsoft.com/library/windows/hardware/ff568164)このような状況で他の操作を実行します。

1.  TMM 呼び出し、 **EnumDisplayDevices**アダプター、表示、およびモニターが含まれています、現在の表示構成を取得します。 詳細については**EnumDisplayDevices**、Microsoft Windows SDK のドキュメントを参照してください。

2.  TMM は、以前に記録された表示の構成に対して表示の構成を比較します。

3.  表示構成に拡張表示情報のデータを 1 つまたは 2 つのモニターがある場合 (*EDID*) TMM が実行する前に、TMM TMM ダイアログ ボックスを表示に発生していないこと。

4.  表示構成の各アダプタ TMM への呼び出しは、 [ **IViewHelper::GetConnectedIDs** ](https://msdn.microsoft.com/library/windows/hardware/ff568171)ソースがマップされるかどうかは、すべてのアダプターのソースを取得します。

5.  TMM に対して呼び出しを行う、 [ **IViewHelper::GetConnectedIDs** ](https://msdn.microsoft.com/library/windows/hardware/ff568171)ターゲットがマップされるかどうかは、すべてのアダプターのターゲットを取得するメソッド。 各ターゲットは、接続する必要がありますが、アクティブにする必要はありません。

6.  TMM グラフィックス アダプターの各ソースへの呼び出しは、 [ **IViewHelper::GetActiveTopology** ](https://msdn.microsoft.com/library/windows/hardware/ff568169)ソースのアクティブなターゲットを取得します。

7.  TMM をターゲットにマップされているソースを持つグラフィックス アダプターを検索します。 このソース識別子は"CloneSource"と呼ばれる TMM が 2 つのエントリの配列を作成する場合は、アダプターは、2 つのターゲットには、(ULONG targetArray\[2\])。 TMM では、最初の要素として既存のターゲットの識別子と 2 番目の要素として 2 つ目のターゲットの識別子を配置します。

8.  TMM 呼び出し、 [ **IViewHelper::SetActiveTopology**](https://msdn.microsoft.com/library/windows/hardware/ff568174)(adapterName、CloneSource、2、targetArray) 指定されたパラメーターを持つメソッド。

9.  TMM 呼び出し、 [ **IViewHelper::Commit** ](https://msdn.microsoft.com/library/windows/hardware/ff568167)メソッド。

いずれかから、エラーの結果が返された場合、 [IViewHelper](https://msdn.microsoft.com/library/windows/hardware/ff568164)メソッドでは、コンピューターが複製のビューを入力しないと、複製ビューおよび外部専用のオプションを無効になっている TMM ダイアログがポップアップします。

場合は、コンピューターが複製のビューに入るし、TMM ダイアログから拡張表示を選択 (クリックして**OK**または**適用**)、TMM が次のようの複製の表示をオフにする必要があります。

1.  TMM 呼び出し、 [ **IViewHelper::SetActiveTopology**](https://msdn.microsoft.com/library/windows/hardware/ff568174)(adapterName、CloneSource、1、targetArray) 指定されたパラメーターを持つメソッド。

2.  TMM 呼び出し、 [ **IViewHelper::Commit** ](https://msdn.microsoft.com/library/windows/hardware/ff568167)メソッド。

上記の「 **SetActiveTopology**呼び出し、パラメーター 3 に設定されている 1 と 2 ではありません。 このような状況で**SetActiveTopology**解釈*targetArray*として 1 つの要素の配列。 **SetActiveTopology** 2 つ目のターゲットをオフにし、1 つのビューを入力します。 次に、TMM を使用して、 **ChangeDisplaySettingsEx**表示を拡張する関数。 詳細については**ChangeDisplaySettingsEx**、Microsoft Windows SDK のドキュメントを参照してください。

次の図は、TMM モニターが構成の 2 つのモニターに追加されると、状況を処理するときに発生する操作の流れを示しています。

![構成の 2 つのモニターのモニターを追加することを示す図](images/tmm-newconfig.png)

 

 





