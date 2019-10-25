---
title: 2つのモニター構成の処理
description: 2つのモニター構成の処理
ms.assetid: 224ebc3f-dace-4b41-bfc8-6fd81c8b309d
keywords:
- TMM WDK display、2つのモニター構成
- 監視構成 WDK ディスプレイ、2台のモニター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c07b20dc1161c65ed1962a9b7db7406f4baac23
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838903"
---
# <a name="handling-two-monitor-configurations"></a>2つのモニター構成の処理


2つのモニターの構成によって、TMM ダイアログが生成されます。 2つのターゲットが同じグラフィックスアダプターの一部である場合、TMM はターゲットのいずれかに現在マップされている1つのソースを両方のターゲットにマップします。 TMM がマッピングを実行すると、TMM ダイアログがポップアップ表示されます。 ターゲットが異なるグラフィックスアダプターにある場合は、2番目のモニターをアクティブにしなくても TMM ダイアログがポップアップ表示されます。 このような状況では、[TMM] ダイアログは [複製] または [拡張] のオプションを備えていません。

次のシーケンスは、TMM が[IViewHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)のメソッドを呼び出し、この状況で他の操作を実行する順序を示しています。

1.  TMM は、アダプター、ディスプレイ、モニターなど、現在のディスプレイ構成を取得するために、 **Enumdisplaydevices**関数を呼び出します。 **Enumdisplaydevices**の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

2.  TMM は、以前に記録された表示構成と表示構成を比較します。

3.  ディスプレイの構成に、拡張された表示情報データ (*EDID*) を持つモニターが1つまたは2つあり、tmm がそれ以前に検出されていない場合、TMM は tmm ダイアログを表示します。

4.  ディスプレイ構成内のアダプターごとに、TMM は[**IViewHelper:: GetConnectedIDs**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568171(v=vs.85))メソッドを呼び出して、ソースがマップされているかどうかにかかわらず、アダプター上のすべてのソースを取得します。

5.  TMM は[**IViewHelper:: GetConnectedIDs**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568171(v=vs.85))メソッドへの呼び出しを行い、ターゲットがマップされているかどうかにかかわらず、アダプター上のすべてのターゲットを取得します。 各ターゲットは接続されている必要がありますが、アクティブである必要はありません。

6.  TMM は、グラフィックスアダプター内の各ソースに対して[**IViewHelper:: GetActiveTopology**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568169(v=vs.85))メソッドを呼び出して、ソースのアクティブなターゲットを取得します。

7.  TMM は、ターゲットにマップされているソースを持つグラフィックスアダプターを検索します。 このソース識別子は "CloneSource" と呼ばれます。 アダプターに2つのターゲットがある場合、TMM は2つのエントリの配列を作成します (ULONG targetArray\[2\])。 TMM によって、既存のターゲット識別子が最初の要素として、2番目のターゲット識別子が2番目の要素として配置されます。

8.  TMM は、指定されたパラメーターを使用して、 [**IViewHelper:: SetActiveTopology**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568174(v=vs.85))(Adaptername, CloneSource, 2, targetarray) メソッドを呼び出します。

9.  TMM は[**IViewHelper:: Commit**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568167(v=vs.85))メソッドを呼び出します。

[IViewHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)のいずれかの方法でエラー結果が返された場合、コンピューターは複製ビューには入りません。また、[tmm] ダイアログは、複製ビューと外部専用オプションが無効になっています。

コンピューターが複製ビューに入り、ユーザーが TMM ダイアログから拡張ビューを選択し ([ **OK]** または **[適用]** をクリックした場合)、tmm は次のように複製ビューを無効にする必要があります。

1.  TMM は、指定されたパラメーターを使用して、 [**IViewHelper:: SetActiveTopology**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568174(v=vs.85))(Adaptername, CloneSource, 1, targetarray) メソッドを呼び出します。

2.  TMM は[**IViewHelper:: Commit**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568167(v=vs.85))メソッドを呼び出します。

上記の**Setactivetopology**呼び出しでは、パラメーター3が2ではなく1に設定されています。 この場合、 **Setactivetopology**は*targetarray*を1つの要素を含む配列として解釈します。 **Setactivetopology**は2番目のターゲットをオフにし、単一ビューに入ります。 次に、TMM は**Changedisplaysettingsex**関数を使用して、表示を拡張します。 **Changedisplaysettingsex**の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

次の図は、2つのモニター構成を行うためにモニターを追加したときに TMM が処理を行う場合に発生する操作の流れを示しています。

![2台のモニター構成を行うためのモニターの追加を示す図](images/tmm-newconfig.png)

 

 





