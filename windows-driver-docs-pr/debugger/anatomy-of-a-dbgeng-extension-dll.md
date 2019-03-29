---
title: DbgEng 拡張機能 DLL の構造
description: DbgEng 拡張機能 DLL の構造
ms.assetid: 5131115b-b9a0-479b-9391-7ab384633d92
keywords:
- DbgEng 拡張機能、DLL の構造
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24babd1fb7683107ab4858ef5a206d65e78a3351
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574095"
---
# <a name="anatomy-of-a-dbgeng-extension-dll"></a>DbgEng 拡張機能 DLL の構造


## <span id="ddk_anatomy_of_a_dbgeng_extension_dll_dbx"></span><span id="DDK_ANATOMY_OF_A_DBGENG_EXTENSION_DLL_DBX"></span>


DbgEng 拡張 DLL は、多数の拡張機能コマンドの実装のうちいくつかありますのコールバック関数をエクスポートします。

によってこれらの拡張 Dll が読み込まれる、[デバッガー エンジン](introduction.md#debugger-engine)余分な機能やユーザー モードまたはカーネル モードの Microsoft Windows のデバッグの実行中にタスクの自動化を提供できます。

"Exts"と呼ばれる DbgEng 拡張子のサンプルは sdk にありますツールを Windows のデバッグのフル インストールを実行した場合\\サンプル\\インストール ディレクトリの exts サブディレクトリ。

### <a name="span-idextensioncommandsspanspan-idextensioncommandsspanextension-commands"></a><span id="extension_commands"></span><span id="EXTENSION_COMMANDS"></span>拡張コマンド

拡張機能 DLL は任意の数の拡張機能コマンドの実行に使用される関数をエクスポートする可能性があります。 各関数は、.def ファイル内のエクスポートとして明示的に宣言され、その名が小文字アルファベットの完全で構成する必要があります。

拡張機能のコマンドを実装するために使用される関数は、プロトタイプと一致する必要があります[ **PDEBUG\_拡張子\_呼び出す**](https://msdn.microsoft.com/library/windows/hardware/ff553378)します。

これらの関数は、標準の C++ 規則に従ってという名前の大文字の使用が許可されていない点が異なります。 エクスポートされた関数名と拡張機能コマンドの名前は、感嘆符 (!) 拡張機能のコマンドを開始する点を除いて同じですは。 たとえばと myextension.dll をデバッガーに読み込むし、入力した **! スタック**デバッガー コマンド ウィンドウに、デバッガーがという名前のエクスポートされた関数を検索**スタック**myextension.dll で。

Myextension.dll が既に読み込まれていないかどうか、または入力することができる場合、その他の拡張 Dll で同じ名前を持つその他の拡張機能コマンドである可能性があります、 **! myextension.stack**拡張 DLL を示すデバッガー コマンド ウィンドウに、この DLL 内の拡張機能コマンド。

### <a name="span-idotherexportedfunctionsspanspan-idotherexportedfunctionsspanother-exported-functions"></a><span id="other_exported_functions"></span><span id="OTHER_EXPORTED_FUNCTIONS"></span>その他のエクスポート関数

DLL をエクスポートする必要があります DbgEng 拡張子[ *DebugExtensionInitialize*](https://msdn.microsoft.com/library/windows/hardware/ff540476)します。 これは、DLL を初期化するために、DLL が読み込まれるときに呼び出されます。 グローバル変数を初期化するために、DLL によって使用可能性があります。

拡張 DLL のエクスポートが[ *DebugExtensionUninitialize*](https://msdn.microsoft.com/library/windows/hardware/ff540495)します。 これをエクスポートする場合は、拡張 DLL が読み込まれる前に呼び出されます。 アンロードされる前に、クリーンアップする DLL によって使用可能性があります。

拡張 DLL のエクスポートが[ *DebugExtensionNotify*](https://msdn.microsoft.com/library/windows/hardware/ff540478)します。 これをエクスポートする場合は呼び出すことがセッションを開始または終了するときに、ターゲットが開始または実行を停止します。 これらの通知にも提供[IDebugEventCallbacks](https://msdn.microsoft.com/library/windows/hardware/ff550550)オブジェクトをクライアントに登録します。

拡張 DLL のエクスポートが[ *KnownStructOutput*](https://msdn.microsoft.com/library/windows/hardware/ff551934)します。 これをエクスポートする場合は、DLL が読み込まれるときに呼び出されます。 この関数は、DLL が 1 行に印刷する方法を認識している構造体のリストを返します。 これを印刷用のこれらの構造体のインスタンスを書式設定後で呼び出すことができます。

### <a name="span-idengineprocedureforloadingadbgengextensiondllspanspan-idengineprocedureforloadingadbgengextensiondllspanengine-procedure-for-loading-a-dbgeng-extension-dll"></a><span id="engine_procedure_for_loading_a_dbgeng_extension_dll"></span><span id="ENGINE_PROCEDURE_FOR_LOADING_A_DBGENG_EXTENSION_DLL"></span>DbgEng 拡張 DLL を読み込むためのエンジン プロシージャ

拡張 DLL が読み込まれるときに、次の順序でエンジンによってコールバック関数が呼び出されます。

1.  **DebugExtensionInitialize**呼び出されるので、拡張 DLL を初期化できます。

2.  エクスポートする場合**DebugExtensionNotify**エンジンにアクティブなセッションがある場合に呼び出され、もう一度呼び出すと、セッションが中断され、アクセス可能な場合。

3.  エクスポートする場合**KnownStructOutput** DLL が 1 行に印刷する方法を知っている構造体のリストを要求すると呼びます。

参照してください[デバッガー拡張 Dll の読み込み](loading-debugger-extension-dlls.md)ロードし、拡張 DLL のアンロードを参照してください、デバッガーを使用する方法については[デバッガー拡張機能コマンドの使用](using-debugger-extension-commands.md)実行については、拡張機能コマンド。

デバッガー エンジンは配置を**試用/を除く**拡張 DLL への呼び出しの周囲にブロックします。 これは拡張機能のコードでバグの一部の種類から、エンジンを保護します。ただし、拡張機能の呼び出しは、エンジンと同じスレッドで実行される、ため、まだ可能性がありますがクラッシュします。

 

 





