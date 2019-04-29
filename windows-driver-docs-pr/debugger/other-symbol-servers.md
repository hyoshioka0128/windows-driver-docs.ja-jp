---
title: その他のシンボル サーバー
description: その他のシンボル サーバー
ms.assetid: 69d88a60-88b6-4118-9f8b-0d7b80bad1ab
keywords:
- シンボル サーバー、シンボル サーバーの作成
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d87721e74cbf37f9aa17eacca34ebd2db30be2f0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330950"
---
# <a name="other-symbol-servers"></a>その他のシンボル サーバー


## <span id="ddk_using_other_symbol_servers_dbg"></span><span id="DDK_USING_OTHER_SYMBOL_SERVERS_DBG"></span>


独自のシンボル サーバー DLL を行うことができます、シンボルの検索のさまざまなメソッドを使用する場合は、SymSrv を使用するのではなく。

### <a name="span-idsettingthesymbolpathspanspan-idsettingthesymbolpathspansetting-the-symbol-path"></a><span id="setting_the_symbol_path"></span><span id="SETTING_THE_SYMBOL_PATH"></span>シンボル パスを設定します。

SymSrv 以外のシンボル サーバーを実装する場合、デバッガーのシンボル パスは、SymSrv のと同じように設定されます。 参照してください[SymSrv](symsrv.md)シンボル パスの構文の詳細についてはします。 文字列を置換する必要がある唯一の違いは、 **symsrv.dll**独自のシンボル サーバー DLL の名前に置き換えます。

場合は、自由に UNC パス、SQL データベースの識別子、またはインターネット仕様などさまざまなテクノロジの使用を示すパラメーター内で別の構文を使用しています。

### <a name="span-idimplementingyourownsymbolserverspanspan-idimplementingyourownsymbolserverspanimplementing-your-own-symbol-server"></a><span id="implementing_your_own_symbol_server"></span><span id="IMPLEMENTING_YOUR_OWN_SYMBOL_SERVER"></span>シンボル サーバーを実装します。

サーバーの中央部分は、シンボルを検索する DbgHelp と通信するコードを示します。 DbgHelp では、新しく読み込まれたモジュールのシンボルが必要とするたびに、適切なシンボル ファイルを検索するシンボル サーバーを呼び出します。 シンボル サーバーは、各ファイルでは、タイム スタンプやイメージのサイズなどの固有のパラメーターを検索します。 サーバーは、要求されたファイルを検証済みのパスを返します。 サーバーのエクスポートを実装する必要があります、 **SymbolServer**関数。

サーバーをサポートする必要がありますも、 **SymbolServerSetOptions**と**SymbolServerGetOptions**関数。 DbgHelp を呼び出すと、 **SymbolServerClose**関数は、サーバーがエクスポートした場合。 参照してください[シンボル サーバー API](symbol-server-api.md)についてはこれらのルーチンが記載されています。

シンボル サーバーによって返される実際の記号ファイル名を変更する必要があります。 DbgHelp は、複数の場所でシンボル ファイルの名前を格納します。 そのため、サーバーは、シンボルが要求されたときに、指定されているように、同じ名前のファイルを返す必要があります。 シンボルの読み込み中に表示されるシンボルの名前が、プログラマが認識されるようにするのには、この制限が必要です。

### <a name="span-idrestrictionsonmultiplesymbolserversspanspan-idrestrictionsonmultiplesymbolserversspanrestrictions-on-multiple-symbol-servers"></a><span id="restrictions_on_multiple_symbol_servers"></span><span id="RESTRICTIONS_ON_MULTIPLE_SYMBOL_SERVERS"></span>複数のシンボル サーバーの制限

DbgHelp では、一度に 1 つだけのシンボル サーバーの使用をサポートします。 シンボル パスには、同じシンボル サーバー DLL の複数のインスタンスが 2 つ異なるシンボル サーバーではなく Dll を含めることができます。 これは、制限の多くはまだを自由にシンボル サーバーの複数のインスタンスを別のシンボル ストアを指す各シンボル パスに含めるため。 2 つの異なるシンボル サーバー Dll 間で切り替えるたびに、シンボル パスを変更する必要があります。

### <a name="span-idinstallingyoursymbolserverspanspan-idinstallingyoursymbolserverspaninstalling-your-symbol-server"></a><span id="installing_your_symbol_server"></span><span id="INSTALLING_YOUR_SYMBOL_SERVER"></span>シンボル サーバーをインストールします。

シンボル サーバーのインストールの詳細については、状況によって異なります。 シンボル サーバー DLL をコピーするインストール プロセスを設定する設定と、 \_NT\_シンボル\_PATH 環境変数に自動的にします。

によっては、サーバーで使用されるテクノロジ、インストールまたは自体のシンボル データにアクセスする可能性がありますも必要です。

 

 





