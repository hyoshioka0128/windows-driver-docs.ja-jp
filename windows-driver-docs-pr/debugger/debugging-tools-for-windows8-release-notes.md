---
title: Debugging Tools for Windows 8 リリース ノート
description: Debugging Tools for Windows 8 リリース ノート
ms.assetid: 15776778-691F-4F76-92CE-2DB266AD31E8
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1761adeaf561a6063544d0fdf9419ce6961f33f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346351"
---
# <a name="debugging-tools-for-windows8-release-notes"></a>Debugging Tools for Windows 8 リリース ノート


## <a name="span-idchannelnumberfor1394debugginginvisualstudiospanspan-idchannelnumberfor1394debugginginvisualstudiospanspan-idchannelnumberfor1394debugginginvisualstudiospanchannel-number-for-1394-debugging-in-visual-studio"></a><span id="Channel_number_for_1394_debugging_in_Visual_Studio"></span><span id="channel_number_for_1394_debugging_in_visual_studio"></span><span id="CHANNEL_NUMBER_FOR_1394_DEBUGGING_IN_VISUAL_STUDIO"></span>Visual Studio で 1394 デバッグ チャネルの数


1394 ケーブル経由でのカーネル モードのデバッグを実行する Microsoft Visual Studio を使用する場合は、1 ~ 62 包括的な 10 進数の整数にチャネルを設定します。 最初のデバッグを設定するときに、チャネルを 0 に設定しないでください。 既定のチャネルの値が 0 の場合、ソフトウェアがあると仮定するための変更はなく、設定を更新できません。 0 のチャネルを使用する必要がありますまず別のチャネル (1 ~ 62) を使用してし、し、チャネル 0 に切り替えます。

## <a name="span-idinlinefunctiondebuggingisonbydefaultspanspan-idinlinefunctiondebuggingisonbydefaultspanspan-idinlinefunctiondebuggingisonbydefaultspaninline-function-debugging-is-on-by-default"></a><span id="Inline_function_debugging_is_on_by_default"></span><span id="inline_function_debugging_is_on_by_default"></span><span id="INLINE_FUNCTION_DEBUGGING_IS_ON_BY_DEFAULT"></span>既定ではインライン関数のデバッグ


Windows 8 でのインライン関数のデバッグは既定でオンです。 コマンドは、 **.inline 0**インライン関数のデバッグ、およびコマンドをオフに **.inline 1**インライン関数のデバッグを有効にします。

## <a name="span-idinvalidportnumberinconfigurationpagefornetworkdebuggingspanspan-idinvalidportnumberinconfigurationpagefornetworkdebuggingspanspan-idinvalidportnumberinconfigurationpagefornetworkdebuggingspaninvalid-port-number-in-configuration-page-for-network-debugging"></a><span id="Invalid_port_number_in_configuration_page_for_network_debugging"></span><span id="invalid_port_number_in_configuration_page_for_network_debugging"></span><span id="INVALID_PORT_NUMBER_IN_CONFIGURATION_PAGE_FOR_NETWORK_DEBUGGING"></span>ネットワークのデバッグの構成 ページで無効なポート番号


**問題点:** カーネル モードのネットワークのデバッグの構成 ページで、無効なポート番号が入力された場合、構成は成功しますが、デバッガー ホスト コンピューターでは、ターゲット コンピューターに接続できません。

**対応策 :** 有効では、ポート番号を確認します。 有効なポート番号の範囲 49152 ~ 65535 です。 また、会社をポートを使用してネットワークのデバッグの制限があります。 有効なポート番号が入力されていることを確認するには、内部 IP セキュリティ ポリシーを確認してください。

## <a name="span-iduseofremotetoolincommandlinespanspan-iduseofremotetoolincommandlinespanuse-of-remote-tool-in-command-line"></a><span id="use_of_.remote_tool_in_command_line"></span><span id="USE_OF_.REMOTE_TOOL_IN_COMMAND_LINE"></span>コマンドラインで .remote ツールの使用


**問題点:** 使用 **.remote** npipe を使用して以前のスタイル remote.exe を作成するときにコマンド ライン ツールのインターフェイスがクラッシュします。

**対応策 :** 使用して、 **.server**コマンドを代わりにします。

## <a name="span-iddesignfeaturesforvisualstudiospanspan-iddesignfeaturesforvisualstudiospanspan-iddesignfeaturesforvisualstudiospandesign-features-for-visual-studio"></a><span id="Design_features_for_Visual_Studio"></span><span id="design_features_for_visual_studio"></span><span id="DESIGN_FEATURES_FOR_VISUAL_STUDIO"></span>Visual Studio のデザイン機能


-   マシンの自動プロビジョニングが含まれていますユーザー モードとカーネル モードのブートス トラップの両方に関係なく 1 つ選択されます。 これは、2 つのプロビジョニングが再起動され、8 ~ 20 分間かかりますが必要です。
-   一度に 1 つだけのプロセスのアタッチをサポートします。
-   Windows デバッガー Extension for Visual Studio でのデバッグ セッション中に例外は、コマンドラインを使用して管理されます。

## <a name="span-idglobaldesignfeaturesspanspan-idglobaldesignfeaturesspanspan-idglobaldesignfeaturesspanglobal-design-features"></a><span id="Global_design_features"></span><span id="global_design_features"></span><span id="GLOBAL_DESIGN_FEATURES"></span>グローバル デザイン機能


-   ユーザーは、USB 3.0 XHCI フィルター ドライバーをインストールするには、管理者特権でのコンテキストで実行する必要があります。 ユーザーが管理者特権で実行されていない場合、PnP マネージャーには、ユーザーを通知しません昇格に問題があるエラー メッセージが返されます。
-   カーネル デバッグが有効になっている場合のカーネルのデバッグに使用するデバイス必要があるシステムから削除されません、デバイスがまだオンにします。 デバイスが削除された場合、システムがハングおよび再起動する必要があります。

 

 





