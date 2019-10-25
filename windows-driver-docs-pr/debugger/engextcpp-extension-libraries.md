---
title: EngExtCpp 拡張機能ライブラリ
description: EngExtCpp 拡張機能ライブラリ
ms.assetid: 8c7ce3f8-46c4-408c-aab5-00d654bddfcd
keywords:
- EngExtCpp 拡張機能、ライブラリ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f345fb6d9e66cf21e706c1b5f510618f2befb3f3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837760"
---
# <a name="engextcpp-extension-libraries"></a>EngExtCpp 拡張機能ライブラリ


## <span id="ddk_anatomy_of_a_dbgeng_extension_dll_dbx"></span><span id="DDK_ANATOMY_OF_A_DBGENG_EXTENSION_DLL_DBX"></span>


EngExtCpp 拡張ライブラリは、EngExtCpp で見つかった EngExtCpp extension フレームワークを使用する DLL です。 このライブラリがデバッガーエンジンによって読み込まれると、そのメソッドと関数は、Microsoft Windows でユーザーモードまたはカーネルモードのデバッグを実行しているときに、追加の機能を提供したりタスクを自動化したりすることができます。

EngExtCpp extension framework は、 [Dbgeng 拡張機能フレームワーク](writing-dbgeng-extension-code.md)の上に構築されています。 デバッガーエンジンとの対話には、同じデバッガーエンジン API が用意されています。 ただし、一般的なタスクをより簡単にするための追加機能も用意されています。

Windows 用デバッグツールの完全インストールを実行した場合、"extcpp" という名前のサンプル EngExtCpp 拡張機能は、インストールディレクトリの [sdk\\samples]\\extcpp サブディレクトリにあります。

### <a name="span-idext_class_and_extextensionspanspan-idext_class_and_extextensionspanext_class-and-extextension"></a><span id="ext_class_and_extextension"></span><span id="EXT_CLASS_AND_EXTEXTENSION"></span>EXT\_クラスと ExtExtension

EngExtCpp 拡張ライブラリの中核となるのは、 [**EXT\_クラス**](https://docs.microsoft.com/previous-versions/ff544508(v=vs.85))クラスの1つのインスタンスです。 EngExtCpp 拡張ライブラリは、このクラスの実装を提供します。このクラスには、ライブラリによってエクスポートされる構造体を書式設定するためのすべての拡張コマンドとメソッドが含まれています。

EXT\_クラスは、 [**Extextension**](https://msdn.microsoft.com/library/windows/hardware/ff543981)のサブクラスです。 このクラスの単一のインスタンスは、 [**EXT\_DECLARE\_GLOBALS**](https://docs.microsoft.com/previous-versions/ff544527(v=vs.85))マクロを使用して作成されます。このマクロは、拡張ライブラリのソースファイルに1回だけ記述する必要があります。

拡張ライブラリが読み込まれると、クラスの[**Initialize**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff550945(v=vs.85))メソッドがエンジンによって呼び出され、クラスのアンロード前に[**初期化**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff558961(v=vs.85))解除メソッドが呼び出されます。 さらに、 [**Onsessionactive**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff552312(v=vs.85))、 [**onsessionactive**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff552318(v=vs.85))、 [**onsessionactive 可能**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff552310(v=vs.85))、および[**onsessionactive アクセスでき**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff552315(v=vs.85))ないメソッドがエンジンによって呼び出され、デバッグセッションの状態が拡張ライブラリに通知されます。

### <a name="span-idextension_commandsspanspan-idextension_commandsspanextension-commands"></a><span id="extension_commands"></span><span id="EXTENSION_COMMANDS"></span>拡張機能コマンド

[**EXT\_クラス**](https://docs.microsoft.com/previous-versions/ff544508(v=vs.85))クラスには、拡張コマンドを実行するために使用されるいくつかのメソッドを含めることができます。 各拡張機能コマンドは、ext [ **\_コマンド\_メソッド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/engextcpp/nf-engextcpp-ext_command_method)マクロを使用して、EXT\_クラスクラスで宣言します。 コマンドの実装は、 [**EXT\_コマンド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/engextcpp/nf-engextcpp-ext_command)マクロを使用して定義します。

### <a name="span-idknown_structuresspanspan-idknown_structuresspanknown-structures"></a><span id="known_structures"></span><span id="KNOWN_STRUCTURES"></span>既知の構造体

[**EXT\_クラス**](https://docs.microsoft.com/previous-versions/ff544508(v=vs.85))クラスには、 [*ExtKnownStructMethod*](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))プロトタイプを使用するいくつかのメソッドを含めることができます。 メソッドは、特定の構造体型のインスタンスを出力用に書式設定するためにエンジンによって使用できます。

### <a name="span-idprovided_valuesspanspan-idprovided_valuesspanprovided-values"></a><span id="provided_values"></span><span id="PROVIDED_VALUES"></span>指定された値

[**EXT\_クラス**](https://docs.microsoft.com/previous-versions/ff544508(v=vs.85))クラスには、 **ExtProvideValueMethod**プロトタイプを使用するいくつかのメソッドを含めることができます。 メソッドは、拡張機能によって提供されるいくつかの擬似レジスタを評価するためにエンジンによって使用できます。

 

 





