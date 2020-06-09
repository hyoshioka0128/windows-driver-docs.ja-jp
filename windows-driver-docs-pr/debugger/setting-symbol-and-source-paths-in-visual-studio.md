---
title: Visual Studio でのシンボルと実行可能イメージ パスの設定
description: この手順では、Visual Studio でシンボルと実行可能イメージのパスを設定します。
ms.assetid: BFFF9BBC-C926-4974-A43E-C3A2DDA74AA4
ms.date: 05/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9c2924f07e7d66238d0614b21ae48c19477f787c
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534769"
---
# <a name="setting-symbol-and-executable-image-paths-in-visual-studio"></a>Visual Studio でのシンボルと実行可能イメージ パスの設定

> [!IMPORTANT]
> この機能は、Windows 10 バージョン1507以降のバージョンの WDK では使用できません。
>


このトピックに記載されている手順では、Windows Driver Kit が Visual Studio に統合されている必要があります。 統合環境を利用するには、まず Microsoft Visual Studio をインストールしてから、Windows Driver Kit (WDK) をインストールします。 詳細については、「 [Visual Studio を使用したデバッグ](debugging-using-visual-studio.md)」を参照してください。

## <a name="span-idsetting_the_symbol_path_by_using_a_property_pagespanspan-idsetting_the_symbol_path_by_using_a_property_pagespanspan-idsetting_the_symbol_path_by_using_a_property_pagespansetting-the-symbol-path-by-using-a-property-page"></a><span id="Setting_the_Symbol_Path_by_Using_a_Property_Page"></span><span id="setting_the_symbol_path_by_using_a_property_page"></span><span id="SETTING_THE_SYMBOL_PATH_BY_USING_A_PROPERTY_PAGE"></span>プロパティページを使用してシンボルパスを設定する


1.  ホストコンピューターの Visual Studio で、[**ツール**] メニューの [**オプション**] をクリックします。
2.  [**オプション**] プロパティボックスで、[**デバッグ &gt; シンボル**] に移動します。
3.  Microsoft シンボルサーバーからシンボルを取得する場合は、[ **Microsoft シンボルサーバー**] をオンにします。
4.  ホストコンピューター上のフォルダーからシンボルを取得する場合は、[**環境変数: \_ NT \_ シンボル \_ パス**] をオンにします。 次に、 \_ NT \_ シンボル \_ パス[環境変数](general-environment-variables.md)を設定します。

## <a name="span-idsetting_the_symbol_path_by_entering_a_commandspanspan-idsetting_the_symbol_path_by_entering_a_commandspanspan-idsetting_the_symbol_path_by_entering_a_commandspansetting-the-symbol-path-by-entering-a-command"></a><span id="Setting_the_Symbol_Path_by_Entering_a_Command"></span><span id="setting_the_symbol_path_by_entering_a_command"></span><span id="SETTING_THE_SYMBOL_PATH_BY_ENTERING_A_COMMAND"></span>コマンドを入力してシンボルパスを設定する


Visual Studio のデバッガーの [イミディエイト] ウィンドウで、 [**sympath (シンボルパスの設定)**](-sympath--set-symbol-path-.md)コマンドを入力します。

## <a name="span-idsetting_the_executable_image_path_by_entering_a_commandspanspan-idsetting_the_executable_image_path_by_entering_a_commandspanspan-idsetting_the_executable_image_path_by_entering_a_commandspansetting-the-executable-image-path-by-entering-a-command"></a><span id="Setting_the_Executable_Image_Path_by_Entering_a_Command"></span><span id="setting_the_executable_image_path_by_entering_a_command"></span><span id="SETTING_THE_EXECUTABLE_IMAGE_PATH_BY_ENTERING_A_COMMAND"></span>コマンドを入力して、実行可能イメージのパスを設定する


Visual Studio のデバッガーの [イミディエイト] ウィンドウで、 [**exepath (実行可能ファイルパスの設定)**](-exepath--set-executable-path-.md)コマンドを入力します。

 

 





