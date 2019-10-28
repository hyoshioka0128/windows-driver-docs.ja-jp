---
title: フレームワーク レジストリ キー オブジェクトの使用
description: フレームワーク レジストリ キー オブジェクトの使用
ms.assetid: 2236b4e1-2e17-4e59-b12e-70fff5fd7513
keywords:
- レジストリ WDK KMDF
- レジストリキーオブジェクト WDK KMDF
- フレームワークベースのドライバー WDK KMDF、レジストリ
- カーネルモードドライバー WDK KMDF、レジストリ
- KMDF WDK、レジストリ
- カーネルモードドライバーフレームワーク WDK、レジストリ
- キー WDK KMDF
- レジストリキー WDK KMDF を開いています
- レジストリキーの削除 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d22d8e77838dc8dc80fa64bab3602587d5b92fdc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843081"
---
# <a name="using-framework-registry-key-objects"></a>フレームワーク レジストリ キー オブジェクトの使用


フレームワークベースのドライバーは、*フレームワークのレジストリキーオブジェクト*を使用してレジストリにアクセスします。 レジストリキーオブジェクトは、ドライバーによるレジストリキーの作成、オープン、および終了を可能にするメソッドを定義します。レジストリ値を追加および削除します。レジストリ値に割り当てられているデータの読み取りまたは書き込みを行います。

レジストリキーを開くには、ドライバーが[**Wdfregistryopenkey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryopenkey)を呼び出す必要があります。 キーが存在しない場合、ドライバーは[**WdfRegistryCreateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistrycreatekey)を呼び出す必要があります。これにより、新しいキーが作成されて開きます。

ドライバーがレジストリキーを開くと、フレームワークは、開かれたキーを表すレジストリキーオブジェクトを作成し、ドライバーへのオブジェクトハンドルを返します。 ドライバーは、キー、キーの下に存在するサブキー、およびキーまたはサブキーの下に存在する任意の値にアクセスするために、オブジェクトハンドルを使用する必要があります。

現在レジストリ値の名前に割り当てられているデータを読み取るには、ドライバーは次のいずれかのオブジェクトメソッドを呼び出すことができます。

<a href="" id="---------wdfregistryquerymemory--------"></a>[**WdfRegistryQueryMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryquerymemory)  
値名に現在割り当てられているデータを取得し、フレームワークに割り当てられたバッファーにデータを格納し、そのバッファーを表すフレームワークメモリオブジェクトを作成します。

<a href="" id="---------wdfregistryquerymultistring--------"></a>[**WdfRegistryQueryMultiString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryquerymultistring)  
複数の文字列で型指定された値名に現在割り当てられている文字列データを取得し、各文字列のフレームワーク文字列オブジェクトを作成して、各文字列オブジェクトをオブジェクトコレクションに追加します。

<a href="" id="---------wdfregistryquerystring--------"></a>[**WdfRegistryQueryString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryquerystring)  
文字列型の値名に現在割り当てられている文字列データを取得し、その文字列を指定したフレームワーク文字列オブジェクトに割り当てます。

<a href="" id="---------wdfregistryqueryunicodestring--------"></a>[**WdfRegistryQueryUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryqueryunicodestring)  
文字列型の値名に現在割り当てられている文字列データを取得し、その文字列を指定した[**UNICODE\_文字列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/ns-wudfwdm-_unicode_string)構造体にコピーします。

<a href="" id="---------wdfregistryqueryulong--------"></a>[**WdfRegistryQueryULong**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryqueryulong)  
値名に現在割り当てられている unsigned long word (REG\_DWORD) データを取得し、そのデータを指定した場所にコピーします。

<a href="" id="---------wdfregistryqueryvalue--------"></a>[**WdfRegistryQueryValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryqueryvalue)  
値名に現在割り当てられているデータを取得し、そのデータをドライバーによって指定されたバッファーにコピーします。

レジストリ値にデータを書き込むために、ドライバーは次のいずれかのメソッドを呼び出すことができます。 値の名前が既に存在する場合、オペレーティングシステムは値のデータを更新します。

<a href="" id="---------wdfregistryassignmemory--------"></a>[**Wdfregistry割り当てメモリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryassignmemory)  
メモリバッファーに格納されているデータを、レジストリ内の指定した値の名前に割り当てます。

<a href="" id="---------wdfregistryassignmultistring--------"></a>[**Wdfregistry割り当ての文字列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryassignmultistring)  
レジストリ内の指定した値名に文字列のセットを割り当てます。 文字列は、ドライバーによって提供されるフレームワーク文字列オブジェクトのコレクションに含まれています。

<a href="" id="---------wdfregistryassignstring--------"></a>[**Wdfregistry割り当て文字列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryassignstring)  
レジストリ内の指定した値の名前に文字列を割り当てます。 文字列は、フレームワークの文字列オブジェクトに含まれています。

<a href="" id="---------wdfregistryassignunicodestring--------"></a>[**WdfRegistryAssignUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryassignunicodestring)  
指定された Unicode 文字列をレジストリ内の指定した値の名前に割り当てます。

<a href="" id="---------wdfregistryassignulong--------"></a>[**Wdfregistry割り当て Ulong**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryassignulong)  
指定した符号なし長い単語の値をレジストリ内の指定した値の名前に割り当てます。

<a href="" id="---------wdfregistryassignvalue--------"></a>[**Wdfregistry割り当て値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryassignvalue)  
ドライバーによって提供されるデータバッファーの内容を、レジストリ内の指定した値の名前に割り当てます。

レジストリ値を削除するには、ドライバーが[**Wdfregistryremovevalue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryremovevalue)を呼び出す必要があります。 キーを削除するには、ドライバーが[**Wdfregistryremovekey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryremovekey)を呼び出す必要があります。

レジストリに関する WDM 情報を取得するために、ドライバーは[**WdfRegistryWdmGetHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistrywdmgethandle)を呼び出すことができます。これにより、フレームワークのレジストリキーオブジェクトが表すレジストリキーへの wdm ハンドルが返されます。

ドライバーがレジストリキーへのアクセスを終了したら、 [**Wdfregistryclose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfregistry/nf-wdfregistry-wdfregistryclose)または[**Wdfregistryclose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)を呼び出してキーを閉じ、レジストリキーオブジェクトを削除する必要があります。

 

 





