---
title: BinPlace のマクロと環境変数
description: BinPlace のマクロと環境変数
ms.assetid: f990e132-f6d7-46e1-8c86-6ae3f0483bd5
keywords:
- BinPlace WDK、環境変数
- WDK BinPlace の環境変数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 926bc755dc2ed14f40d030aa894fc7de215101f3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573941"
---
# <a name="binplace-macros-and-environment-variables"></a>BinPlace のマクロと環境変数


## <span id="ddk_binplace_environment_variables_tools"></span><span id="DDK_BINPLACE_ENVIRONMENT_VARIABLES_TOOLS"></span>


BinPlace では、次のマクロと環境変数の値を読み取ります。

<span id="BINPLACE_OVERRIDE_FLAGS"></span><span id="binplace_override_flags"></span>BINPLACE\_オーバーライド\_フラグ  
追加のコマンド ライン パラメーターを含むファイルを指定します。 これらのスイッチにも、実際のコマンド ラインで BinPlace が使用されます。 このオーバーライド ファイル内のスイッチは、実際のコマンド ライン スイッチの前に解析されます。

<span id="________BINPLACE_LOG_______"></span><span id="________binplace_log_______"></span> BINPLACE\_ログ   
ログ ファイルのパスとファイル名を指定します。 すべての BinPlace アクションは、このログ ファイルに記録されます。

<span id="BINPLACE_MESSAGE_LOG"></span><span id="binplace_message_log"></span>BINPLACE\_メッセージ\_ログ  
メッセージのログ ファイルのパスとファイル名を指定します。 BinPlace が実行されるたびに、コマンドラインは、メッセージのログ ファイルに記録されます。 付いたファイルを使用して、コマンドラインが展開されている場合、アット マーク ( **@** )、展開されたコマンド ライン テキストは、メッセージ ログに格納されます。 ただし、パラメーター、BINPLACE から発信される\_オーバーライド\_フラグ ファイルは、メッセージのログ ファイルには記録されません。

<span id="BINPLACE_EXCLUDE_FILE"></span><span id="binplace_exclude_file"></span>BINPLACE\_除外\_ファイル  
除外するファイルのパスとファイル名を指定します。 これが存在しない場合、既定値は\\ツール\\symbad.txt します。 このファイルは SymChk の引数の場合と同様、SymChk で使用が **/ea**スイッチします。 (SymChk は Windows のツールをデバッグ パッケージの一部です。 参照してください[Windows デバッグ](https://msdn.microsoft.com/library/windows/hardware/ff551063)詳細についてはします)。

<span id="TRACE_FORMAT_PATH"></span><span id="trace_format_path"></span>トレース\_形式\_パス  
トレースに使用するパスを指定時に、このファイル形式、 **-: TMF**スイッチを使用します。

<span id="_________NTTREE_______"></span><span id="_________nttree_______"></span> \_NTTREE   
場合、すべてのファイルを配置するルート インストール先ディレクトリを指定します、 **-r**スイッチは使用されません。 詳細については、[BinPlace コピー先のディレクトリ](binplace-destination-directories.md)を参照してください。

 

 





