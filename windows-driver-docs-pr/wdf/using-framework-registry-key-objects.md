---
title: Framework のレジストリ キー オブジェクトを使用します。
description: Framework のレジストリ キー オブジェクトを使用します。
ms.assetid: 2236b4e1-2e17-4e59-b12e-70fff5fd7513
keywords:
- レジストリ WDK KMDF
- レジストリ キー オブジェクト WDK KMDF
- フレームワーク ベースのドライバー WDK KMDF、レジストリ
- カーネル モード ドライバー WDK KMDF、レジストリ
- KMDF WDK、レジストリ
- カーネル モード ドライバー フレームワーク WDK、レジストリ
- WDK KMDF キー
- WDK KMDF キーのレジストリを開く
- WDK KMDF キーのレジストリを削除します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c21a9983f14ab9992d7001e1698b50ab677a8bfb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553551"
---
# <a name="using-framework-registry-key-objects"></a>Framework のレジストリ キー オブジェクトを使用します。


フレームワーク ベースのドライバーを使用して、レジストリにアクセス*framework レジストリ キー オブジェクト*します。 レジストリ キー オブジェクトを作成し、開き、レジストリ キーを閉じるには、ドライバーを有効にするメソッドを定義します。追加し、削除レジストリ値です。読み取りまたはレジストリ値に割り当てられているデータの書き込み。

レジストリ キーを開くには、ドライバーを呼び出す必要があります[ **WdfRegistryOpenKey**](https://msdn.microsoft.com/library/windows/hardware/ff549919)します。 キーが存在しない場合、ドライバーを呼び出す必要があります[ **WdfRegistryCreateKey**](https://msdn.microsoft.com/library/windows/hardware/ff549917)を新しいキーを作成して開きます。

ドライバーでは、レジストリ キーが開いたら、フレームワークは開いているキーを表し、ドライバーにオブジェクト ハンドルを返しますレジストリ キー オブジェクトを作成します。 ドライバーは、オブジェクト ハンドルを使用して、キー、キーの下に存在するすべてのサブキーと、キーまたはサブキーの下に存在する値にアクセスする必要があります。

レジストリ値の名前に現在割り当てられているデータを読み取り、ドライバーは次のオブジェクトのメソッドのいずれかを呼び出すことができます。

<a href="" id="---------wdfregistryquerymemory--------"></a>[**WdfRegistryQueryMemory**](https://msdn.microsoft.com/library/windows/hardware/ff549920)  
値の名前に現在割り当てられているが、フレームワークに割り当てられたバッファーでデータを格納、バッファーを表す framework メモリ オブジェクトを作成してデータを取得します。

<a href="" id="---------wdfregistryquerymultistring--------"></a>[**WdfRegistryQueryMultiString**](https://msdn.microsoft.com/library/windows/hardware/ff549921)  
マルチ string-型の値名に現在割り当てられている framework の各文字列では、文字列オブジェクトを作成、オブジェクトのコレクションに文字列の各オブジェクトを追加する文字列データを取得します。

<a href="" id="---------wdfregistryquerystring--------"></a>[**WdfRegistryQueryString**](https://msdn.microsoft.com/library/windows/hardware/ff549923)  
文字列に型指定された値の名前に現在割り当てられているし、文字列を指定のフレームワークの文字列オブジェクトに割り当てます、文字列データを取得します。

<a href="" id="---------wdfregistryqueryunicodestring--------"></a>[**WdfRegistryQueryUnicodeString**](https://msdn.microsoft.com/library/windows/hardware/ff549927)  
文字列に型指定された値の名前に現在割り当てられているし、指定された文字列をコピーする文字列データを取得[ **UNICODE\_文字列**](https://msdn.microsoft.com/library/windows/hardware/ff564879)構造体。

<a href="" id="---------wdfregistryqueryulong--------"></a>[**WdfRegistryQueryULong**](https://msdn.microsoft.com/library/windows/hardware/ff549925)  
符号なしの長い単語を取得します (REG\_DWORD) 値の名前に現在割り当てられているし、指定した場所に、データをコピーするデータ。

<a href="" id="---------wdfregistryqueryvalue--------"></a>[**WdfRegistryQueryValue**](https://msdn.microsoft.com/library/windows/hardware/ff549928)  
値の名前に現在割り当てられているし、ドライバーによって提供されるバッファーにデータをコピーするデータを取得します。

レジストリ値にデータの書き込みには、ドライバーは、次のメソッドのいずれかで呼び出すことができます。 値の名前が既に存在する場合、オペレーティング システムは、値のデータを更新します。

<a href="" id="---------wdfregistryassignmemory--------"></a>[**WdfRegistryAssignMemory**](https://msdn.microsoft.com/library/windows/hardware/ff549901)  
レジストリで指定された値の名前をメモリ バッファーに格納されているデータを割り当てます。

<a href="" id="---------wdfregistryassignmultistring--------"></a>[**WdfRegistryAssignMultiString**](https://msdn.microsoft.com/library/windows/hardware/ff549903)  
レジストリで指定された値の名前には、一連の文字列を割り当てます。 文字列は、framework の string オブジェクトのドライバーが指定したコレクション内に格納されます。

<a href="" id="---------wdfregistryassignstring--------"></a>[**WdfRegistryAssignString**](https://msdn.microsoft.com/library/windows/hardware/ff549906)  
レジストリで指定された値の名前には、文字列を割り当てます。 文字列は、framework の文字列オブジェクトに含まれます。

<a href="" id="---------wdfregistryassignunicodestring--------"></a>[**WdfRegistryAssignUnicodeString**](https://msdn.microsoft.com/library/windows/hardware/ff549912)  
レジストリで指定された値の名前を指定した Unicode 文字列を割り当てます。

<a href="" id="---------wdfregistryassignulong--------"></a>[**WdfRegistryAssignULong**](https://msdn.microsoft.com/library/windows/hardware/ff549910)  
レジストリで指定された値の名前には、署名されていない長い単語が指定された値を割り当てます。

<a href="" id="---------wdfregistryassignvalue--------"></a>[**WdfRegistryAssignValue**](https://msdn.microsoft.com/library/windows/hardware/ff549913)  
レジストリで指定された値の名前には、ドライバーが提供するデータ バッファーの内容を割り当てます。

レジストリ値を削除するドライバーを呼び出す必要があります[ **WdfRegistryRemoveValue**](https://msdn.microsoft.com/library/windows/hardware/ff549932)します。 キーを削除するドライバーを呼び出す必要があります[ **WdfRegistryRemoveKey**](https://msdn.microsoft.com/library/windows/hardware/ff549930)します。

WDM のレジストリに関する情報を取得するドライバーを呼び出すことができます[ **WdfRegistryWdmGetHandle**](https://msdn.microsoft.com/library/windows/hardware/ff549935)framework のレジストリ キー オブジェクトが表すレジストリ キーに WDM ハンドルを返します。

呼び出す必要がありますが、ドライバーは、レジストリ キーへのアクセスが終了したら、 [ **WdfRegistryClose** ](https://msdn.microsoft.com/library/windows/hardware/ff549914)または[ **WdfObjectDelete** ](https://msdn.microsoft.com/library/windows/hardware/ff548734)をキーを閉じるレジストリ キー オブジェクトを削除してください。

 

 





