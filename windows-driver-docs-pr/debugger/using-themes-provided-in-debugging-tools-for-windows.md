---
title: Debugging Tools for Windows で提供されているテーマの使用
description: Debugging Tools for Windows で提供されているテーマの使用
ms.assetid: d3571a7a-cdab-4a17-b4e0-ffb1690de642
keywords:
- 指定されたテーマ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8469e0ad441e7f3c67763e4a5d9330f11c475aa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390574"
---
# <a name="using-themes-provided-in-debugging-tools-for-windows"></a>Debugging Tools for Windows で提供されているテーマの使用


## <span id="ddk_creating_and_opening_a_workspace_dbg"></span><span id="DDK_CREATING_AND_OPENING_A_WORKSPACE_DBG"></span>


このトピックでは、各ツールを Windows のデバッグで提供される 4 つのテーマの構成のスクリーン ショットを示します。 これらのテーマは、Standard.reg、Standardvs.reg、Srcdisassembly.reg、Multimon.reg です。

### <a name="span-idstandardregspanspan-idstandardregspanstandardreg"></a><span id="standard_reg"></span><span id="STANDARD_REG"></span>Standard.reg

Standard.reg テーマは、ほとんどのデバッグ目的で使用できます。 これにより、WinDbg ウィンドウの下の 3 つ目は、デバッガー コマンド ウィンドウで取得されます。 上位 3 分 2 が約半分に分かれています。 左半分は、タブ付きのコレクションで、ソース ウィンドウを開く場所を示すプレース ホルダー ウィンドウで占められています。 さらに、部分的には右半分は垂直方向に分割されます。 上半分には、ウォッチ、ローカル変数、レジスタ、および [逆アセンブル] ウィンドウを含むタブ付きのコレクションが含まれています。 下半分には、windows の呼び出しとプロセスとスレッドを含むタブ付きのコレクションが含まれています。

ドッキング場所ごとに、プレース ホルダー ウィンドウは、他のウィンドウの参照のポイントとして含まれるもです。 Windows の構成を変更が終了するため、windows のプレース ホルダーを閉じることができません必要があります。 この配置では、windows のすべてドッキングされます。次のスクリーン ショットでは、Standard.reg テーマを示します。

![standard.reg テーマのスクリーン ショット](images/theme-standard.jpg)

### <a name="span-idstandardvsregspanspan-idstandardvsregspanstandardvsreg"></a><span id="standardvs_reg"></span><span id="STANDARDVS_REG"></span>Standardvs.reg

Standardvs.reg テーマは、ほとんどのデバッグ目的で使用できますが、Visual Studio にレイアウトに似ています。 これにより、WinDbg ウィンドウは 3 分に水平方向に分割します。 上にある 3 つ目はさらに分割垂直方向の部分に。 第 3 に、上の左半分には、ウォッチ、ローカル変数、レジスタ、メモリ、逆アセンブル、およびスクラッチ パッドの windows を含むタブ付きのコレクションが含まれています。 上の右半分には、3 つ目の呼び出しとプロセスとスレッドの windows を含むタブ付きのコレクションが含まれています。 WinDbg のウィンドウの下の 3 つ目は、デバッガー コマンド ウィンドウで取得されます。 中央の 3 つ目は、タブ付きのコレクションで、ソース ウィンドウを開く場所を示すプレース ホルダーのウィンドウで塗りつぶされます。

ドッキング場所ごとに、プレース ホルダー ウィンドウは、他のウィンドウの参照のポイントとして含まれるもです。 Windows の構成を変更が終了するため、windows のプレース ホルダーを閉じることができません必要があります。 この配置では、windows のすべてドッキングされます。 次のスクリーン ショットでは、Standardvs.reg テーマを示します。

![standardvs.reg テーマのスクリーン ショット](images/theme-standardvs.jpg)

### <a name="span-idsrcdisassemblyregspanspan-idsrcdisassemblyregspansrcdisassemblyreg"></a><span id="srcdisassembly_reg"></span><span id="SRCDISASSEMBLY_REG"></span>Srcdisassembly.reg

Srcdisassembly.reg テーマには、デバッグ モードのアセンブリでの逆アセンブル ウィンドウが含まれています。 これにより、WinDbg ウィンドウは半分に垂直方向に分割されます形成される各半分はさらに分割され 3 分の水平方向にします。 右側には、上にあるが、ローカル変数のタブ付きのコレクションを 3 つ目し、ウォッチ ウィンドウ、中央は、デバッガー コマンド ウィンドウを 3 つ目は、小さい値は、プロセスとスレッドの呼び出しのウィンドウのタブ付きコレクションを 3 つ目が。 左の半分に上限の 2/3 はタブ付きコレクションのソース ウィンドウを開く場所を示すプレース ホルダー ウィンドウによって実行されます。下 3 つ目はによって使用される逆アセンブル ウィンドウ。

ドッキング場所ごとに、プレース ホルダー ウィンドウは、他のウィンドウの参照のポイントとして含まれるもです。 Windows の構成を変更が終了するため、windows のプレース ホルダーを閉じることができません必要があります。 この配置では、windows のすべてドッキングされます。 次のスクリーン ショットでは、Srcdisassembly.reg テーマを示します。

![srcdisassembly.reg テーマのスクリーン ショット](images/theme-srcdisassembly.jpg)

### <a name="span-idmultimonregspanspan-idmultimonregspanmultimonreg"></a><span id="multimon_reg"></span><span id="MULTIMON_REG"></span>Multimon.reg

Multimon.reg テーマは、複数のモニターでのデバッグを設定します。 これにより、ように 1 つのモニター、WinDbg ウィンドウを表示することや、新しいドッキング ステーションを他のモニターに表示できます、新しいドッキング ステーションが作成されます。 WinDbg ウィンドウはタブ付きのコレクションで、ソース ウィンドウを開く場所を示すプレース ホルダー ウィンドウによって入力されます。 新しいドッキング ステーションは、4 分に分けられます。 左上には、ウォッチやローカルの windows を含むタブ付きのコレクションが含まれています。 右上には、レジスタ、メモリ、逆アセンブル、スクラッチ パッド、およびプロセスおよびスレッドの windows を含むタブ付きのコレクションが含まれています。 左下には、デバッガー コマンド ウィンドウが含まれています。 右下には、コール スタック ウィンドウが含まれています。

ドッキング場所ごとに、プレース ホルダー ウィンドウは、他のウィンドウの参照のポイントとして含まれるもです。 Windows の構成を変更が終了するため、windows のプレース ホルダーを閉じることができません必要があります。 この配置では、windows のすべてドッキングされます。 次のスクリーン ショットでは、Multimon.reg テーマを示します。

![multimon.reg テーマのスクリーン ショット](images/theme-multimon.jpg)

 

 





