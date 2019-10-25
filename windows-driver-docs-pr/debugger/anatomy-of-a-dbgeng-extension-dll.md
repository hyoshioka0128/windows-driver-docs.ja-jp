---
title: DbgEng 拡張機能 DLL の構造
description: DbgEng 拡張機能 DLL の構造
ms.assetid: 5131115b-b9a0-479b-9391-7ab384633d92
keywords:
- DbgEng 拡張機能、DLL の構造
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d937c8e406f6b4b628269e0283f32bd1cb6b1209
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837837"
---
# <a name="anatomy-of-a-dbgeng-extension-dll"></a>DbgEng 拡張機能 DLL の構造


## <span id="ddk_anatomy_of_a_dbgeng_extension_dll_dbx"></span><span id="DDK_ANATOMY_OF_A_DBGENG_EXTENSION_DLL_DBX"></span>


DbgEng 拡張 DLL では、いくつかのコールバック関数がエクスポートされますが、その一部は拡張コマンドの実装である場合があります。

これらの拡張 Dll は[デバッガーエンジン](introduction.md#debugger-engine)によって読み込まれ、Microsoft Windows でユーザーモードまたはカーネルモードのデバッグを実行しながら、追加の機能やタスクの自動化を提供できます。

Windows 用デバッグツールの完全インストールを実行した場合、"exts" という名前のサンプル DbgEng 拡張機能は、インストールディレクトリの sdk\\samples\\exts サブディレクトリにあります。

### <a name="span-idextension_commandsspanspan-idextension_commandsspanextension-commands"></a><span id="extension_commands"></span><span id="EXTENSION_COMMANDS"></span>拡張機能コマンド

拡張 DLL は、拡張コマンドを実行するために使用される任意の数の関数をエクスポートできます。 各関数は、.def ファイルでエクスポートとして明示的に宣言され、その名前はすべて小文字で構成されている必要があります。

拡張コマンドを実装するために使用される関数は、プロトタイプ[**Pdebug\_拡張機能\_呼び出し**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nc-dbgeng-pdebug_extension_call)に一致する必要があります。

これらの関数には、標準C++規則に従って名前が付けられます。ただし、大文字は使用できません。 エクスポートされた関数名と拡張コマンド名は同じですが、拡張コマンドが感嘆符 (!) で始まっている点が異なります。 たとえば、デバッガーに myextension .dll を読み込み、コマンドウィンドウデバッガーに「 **! stack** 」と入力すると、デバッガーは**スタック**という名前のエクスポート関数を myextension .dll で検索します。

Myextension .dll がまだ読み込まれていない場合、または他の拡張 Dll で同じ名前を持つ他の拡張コマンドが存在する場合は、コマンドウィンドウデバッガーに「 **! myextension. stack** 」と入力して、拡張 dll およびの extension コマンドを示すことができます。その DLL。

### <a name="span-idother_exported_functionsspanspan-idother_exported_functionsspanother-exported-functions"></a><span id="other_exported_functions"></span><span id="OTHER_EXPORTED_FUNCTIONS"></span>エクスポートされたその他の関数

DbgEng 拡張 DLL は[*Debugextensioninitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nc-dbgeng-pdebug_extension_initialize)をエクスポートする必要があります。 Dll が読み込まれるときに呼び出され、DLL を初期化します。 これは、グローバル変数を初期化するために DLL によって使用される場合があります。

拡張 DLL は[*Debugextensionuninitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nc-dbgeng-pdebug_extension_uninitialize)をエクスポートできます。 エクスポートされた場合は、拡張 DLL がアンロードされる前に呼び出されます。 これは、アンロードする前に DLL によって使用される場合があります。

拡張 DLL は[*Debugextensionnotify*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nc-dbgeng-pdebug_extension_notify)をエクスポートできます。 エクスポートされた場合は、セッションの開始または終了時、およびターゲットの開始または停止時に呼び出されます。 これらの通知は、クライアントに登録されている[IDebugEventCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugeventcallbacks)オブジェクトにも用意されています。

拡張 DLL は、 [*KnownStructOutput*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nc-dbgeng-pdebug_extension_known_struct)をエクスポートできます。 エクスポートされた場合は、DLL が読み込まれるときに呼び出されます。 この関数は、DLL が1行に印刷する方法を認識している構造体の一覧を返します。 これらの構造体のインスタンスを書式設定するために後で呼び出すことができます。

### <a name="span-idengine_procedure_for_loading_a_dbgeng_extension_dllspanspan-idengine_procedure_for_loading_a_dbgeng_extension_dllspanengine-procedure-for-loading-a-dbgeng-extension-dll"></a><span id="engine_procedure_for_loading_a_dbgeng_extension_dll"></span><span id="ENGINE_PROCEDURE_FOR_LOADING_A_DBGENG_EXTENSION_DLL"></span>DbgEng 拡張 DLL を読み込むためのエンジンプロシージャ

拡張 DLL が読み込まれると、コールバック関数は、次の順序でエンジンによって呼び出されます。

1.  **Debugextensioninitialize**が呼び出され、拡張 DLL を初期化できるようになりました。

2.  エクスポートされた場合、エンジンにアクティブなセッションがある場合は**Debugextensionnotify**が呼び出され、セッションが中断され、アクセス可能であれば、再度呼び出されます。

3.  エクスポートされた場合、 **KnownStructOutput**は、DLL が1行に印刷する方法を認識している構造体の一覧を要求するために呼び出されます。

デバッガーを使用して拡張 DLL を読み込んでアンロードする方法については、「デバッガー拡張機能の[dll の読み込み](loading-debugger-extension-dlls.md)」を参照してください。拡張機能コマンドの実行については、「[デバッガー拡張機能のコマンドの使用](using-debugger-extension-commands.md)」を参照してください。

デバッガーエンジンでは、拡張 DLL への呼び出しの周囲に**try/except**ブロックが配置されます。 これにより、拡張機能のコードの一部の種類のバグからエンジンが保護されます。ただし、拡張機能の呼び出しは、エンジンと同じスレッドで実行されるため、クラッシュする可能性があります。

 

 





