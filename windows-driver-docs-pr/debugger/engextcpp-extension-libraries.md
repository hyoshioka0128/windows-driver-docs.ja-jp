---
title: EngExtCpp 拡張機能ライブラリ
description: EngExtCpp 拡張機能ライブラリ
ms.assetid: 8c7ce3f8-46c4-408c-aab5-00d654bddfcd
keywords:
- EngExtCpp 拡張機能ライブラリ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 681047814d353cc91177bf04ad324b143f1f905e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366894"
---
# <a name="engextcpp-extension-libraries"></a>EngExtCpp 拡張機能ライブラリ


## <span id="ddk_anatomy_of_a_dbgeng_extension_dll_dbx"></span><span id="DDK_ANATOMY_OF_A_DBGENG_EXTENSION_DLL_DBX"></span>


EngExtCpp 拡張ライブラリは、EngExtCpp.h で見つかった EngExtCpp 拡張機能フレームワークを使用する DLL です。 デバッガー エンジンによってこのライブラリが読み込まれると、そのメソッドおよび関数を提供できます余分な機能やユーザー モードまたはカーネル モードの Microsoft Windows のデバッグの実行中にタスクの自動化。

EngExtCpp 拡張機能フレームワークがの上に構築された、 [DbgEng 拡張フレームワーク](writing-dbgeng-extension-code.md)します。 デバッガー エンジンとの対話のと同じデバッガー エンジン API を提供します。 一般的なタスクを簡素化する追加機能も用意されています。

"Extcpp"と呼ばれる EngExtCpp 拡張子のサンプルは sdk にありますツールを Windows のデバッグのフル インストールを実行した場合\\サンプル\\インストール ディレクトリの extcpp サブディレクトリ。

### <a name="span-idextclassandextextensionspanspan-idextclassandextextensionspanextclass-and-extextension"></a><span id="ext_class_and_extextension"></span><span id="EXT_CLASS_AND_EXTEXTENSION"></span>EXT\_クラスと ExtExtension

ライブラリは 1 つのインスタンスを EngExtCpp 拡張機能の中核に、 [ **EXT\_クラス**](https://docs.microsoft.com/previous-versions/ff544508(v=vs.85))クラス。 EngExtCpp 拡張ライブラリには、すべての拡張機能コマンドと、ライブラリによってエクスポートされる構造体を書式設定するためのメソッドが含まれていますが、このクラスの実装が提供されます。

EXT\_クラスのサブクラスは、 [ **ExtExtension**](https://msdn.microsoft.com/library/windows/hardware/ff543981)します。 使用してこのクラスの 1 つのインスタンスを作成、 [ **EXT\_DECLARE\_GLOBALS** ](https://docs.microsoft.com/previous-versions/ff544527(v=vs.85))マクロ拡張機能ライブラリのソース ファイルに 1 回だけ表示する必要があります。

拡張ライブラリが読み込まれるときに、 [**初期化**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff550945(v=vs.85))クラスのメソッドは、エンジンによって呼び出されます、 [**非**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff558961(v=vs.85))メソッドは、クラスのアンロードの前に呼び出されます。 メソッドではさらに、 [ **OnSessionActive**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff552312(v=vs.85))、 [ **OnSessionInactive**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff552318(v=vs.85))、 [ **OnSessionAccessible**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff552310(v=vs.85))、および[ **OnSessionInaccessible** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff552315(v=vs.85))デバッグ セッションの状態の拡張機能ライブラリに通知する、エンジンによって呼び出されます。

### <a name="span-idextensioncommandsspanspan-idextensioncommandsspanextension-commands"></a><span id="extension_commands"></span><span id="EXTENSION_COMMANDS"></span>拡張コマンド

[ **EXT\_クラス**](https://docs.microsoft.com/previous-versions/ff544508(v=vs.85))クラスは、多数の拡張機能コマンドの実行に使用されるメソッドを含めることができます。 各拡張機能のコマンドは、外部で宣言されて\_クラスを使用して、 [ **EXT\_コマンド\_メソッド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/engextcpp/nf-engextcpp-ext_command_method)マクロ。 使用して、コマンドの実装が定義されている、 [ **EXT\_コマンド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/engextcpp/nf-engextcpp-ext_command)マクロ。

### <a name="span-idknownstructuresspanspan-idknownstructuresspanknown-structures"></a><span id="known_structures"></span><span id="KNOWN_STRUCTURES"></span>既知の構造

[ **EXT\_クラス**](https://docs.microsoft.com/previous-versions/ff544508(v=vs.85))クラスは、さまざまな使用方法を含めることができます、 [ *ExtKnownStructMethod* ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))プロトタイプ。 メソッドは、特定の構造体の型の形式のインスタンスにエンジンが出力に使用できます。

### <a name="span-idprovidedvaluesspanspan-idprovidedvaluesspanprovided-values"></a><span id="provided_values"></span><span id="PROVIDED_VALUES"></span>値を指定

[ **EXT\_クラス**](https://docs.microsoft.com/previous-versions/ff544508(v=vs.85))クラスは、さまざまな使用方法を含めることができます、 **ExtProvideValueMethod**プロトタイプ。 メソッドは、拡張機能によって提供される一部の擬似レジスタを評価するエンジンで使用できます。

 

 





