---
title: フレームワーク レジストリ キー オブジェクトの使用
description: フレームワーク レジストリ キー オブジェクトの使用
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
ms.openlocfilehash: 948145d0768ac32ab1e3f02252abe1ac1612e20e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372254"
---
# <a name="using-framework-registry-key-objects"></a>フレームワーク レジストリ キー オブジェクトの使用


フレームワーク ベースのドライバーを使用して、レジストリにアクセス*framework レジストリ キー オブジェクト*します。 レジストリ キー オブジェクトを作成し、開き、レジストリ キーを閉じるには、ドライバーを有効にするメソッドを定義します。追加し、削除レジストリ値です。読み取りまたはレジストリ値に割り当てられているデータの書き込み。

レジストリ キーを開くには、ドライバーを呼び出す必要があります[ **WdfRegistryOpenKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryopenkey)します。 キーが存在しない場合、ドライバーを呼び出す必要があります[ **WdfRegistryCreateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistrycreatekey)を新しいキーを作成して開きます。

ドライバーでは、レジストリ キーが開いたら、フレームワークは開いているキーを表し、ドライバーにオブジェクト ハンドルを返しますレジストリ キー オブジェクトを作成します。 ドライバーは、オブジェクト ハンドルを使用して、キー、キーの下に存在するすべてのサブキーと、キーまたはサブキーの下に存在する値にアクセスする必要があります。

レジストリ値の名前に現在割り当てられているデータを読み取り、ドライバーは次のオブジェクトのメソッドのいずれかを呼び出すことができます。

<a href="" id="---------wdfregistryquerymemory--------"></a>[**WdfRegistryQueryMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryquerymemory)  
値の名前に現在割り当てられているが、フレームワークに割り当てられたバッファーでデータを格納、バッファーを表す framework メモリ オブジェクトを作成してデータを取得します。

<a href="" id="---------wdfregistryquerymultistring--------"></a>[**WdfRegistryQueryMultiString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryquerymultistring)  
マルチ string-型の値名に現在割り当てられている framework の各文字列では、文字列オブジェクトを作成、オブジェクトのコレクションに文字列の各オブジェクトを追加する文字列データを取得します。

<a href="" id="---------wdfregistryquerystring--------"></a>[**WdfRegistryQueryString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryquerystring)  
文字列に型指定された値の名前に現在割り当てられているし、文字列を指定のフレームワークの文字列オブジェクトに割り当てます、文字列データを取得します。

<a href="" id="---------wdfregistryqueryunicodestring--------"></a>[**WdfRegistryQueryUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryqueryunicodestring)  
文字列に型指定された値の名前に現在割り当てられているし、指定された文字列をコピーする文字列データを取得[ **UNICODE\_文字列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfwdm/ns-wudfwdm-_unicode_string)構造体。

<a href="" id="---------wdfregistryqueryulong--------"></a>[**WdfRegistryQueryULong**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryqueryulong)  
符号なしの長い単語を取得します (REG\_DWORD) 値の名前に現在割り当てられているし、指定した場所に、データをコピーするデータ。

<a href="" id="---------wdfregistryqueryvalue--------"></a>[**WdfRegistryQueryValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryqueryvalue)  
値の名前に現在割り当てられているし、ドライバーによって提供されるバッファーにデータをコピーするデータを取得します。

レジストリ値にデータの書き込みには、ドライバーは、次のメソッドのいずれかで呼び出すことができます。 値の名前が既に存在する場合、オペレーティング システムは、値のデータを更新します。

<a href="" id="---------wdfregistryassignmemory--------"></a>[**WdfRegistryAssignMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryassignmemory)  
レジストリで指定された値の名前をメモリ バッファーに格納されているデータを割り当てます。

<a href="" id="---------wdfregistryassignmultistring--------"></a>[**WdfRegistryAssignMultiString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryassignmultistring)  
レジストリで指定された値の名前には、一連の文字列を割り当てます。 文字列は、framework の string オブジェクトのドライバーが指定したコレクション内に格納されます。

<a href="" id="---------wdfregistryassignstring--------"></a>[**WdfRegistryAssignString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryassignstring)  
レジストリで指定された値の名前には、文字列を割り当てます。 文字列は、framework の文字列オブジェクトに含まれます。

<a href="" id="---------wdfregistryassignunicodestring--------"></a>[**WdfRegistryAssignUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryassignunicodestring)  
レジストリで指定された値の名前を指定した Unicode 文字列を割り当てます。

<a href="" id="---------wdfregistryassignulong--------"></a>[**WdfRegistryAssignULong**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryassignulong)  
レジストリで指定された値の名前には、署名されていない長い単語が指定された値を割り当てます。

<a href="" id="---------wdfregistryassignvalue--------"></a>[**WdfRegistryAssignValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryassignvalue)  
レジストリで指定された値の名前には、ドライバーが提供するデータ バッファーの内容を割り当てます。

レジストリ値を削除するドライバーを呼び出す必要があります[ **WdfRegistryRemoveValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryremovevalue)します。 キーを削除するドライバーを呼び出す必要があります[ **WdfRegistryRemoveKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryremovekey)します。

WDM のレジストリに関する情報を取得するドライバーを呼び出すことができます[ **WdfRegistryWdmGetHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistrywdmgethandle)framework のレジストリ キー オブジェクトが表すレジストリ キーに WDM ハンドルを返します。

呼び出す必要がありますが、ドライバーは、レジストリ キーへのアクセスが終了したら、 [ **WdfRegistryClose** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfregistry/nf-wdfregistry-wdfregistryclose)または[ **WdfObjectDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)をキーを閉じるレジストリ キー オブジェクトを削除してください。

 

 





