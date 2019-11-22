---
title: フレームワーク オブジェクトのコンテキスト領域
description: フレームワーク オブジェクトのコンテキスト領域
ms.assetid: 21a46e04-2330-4a3d-ba72-c04295bfbb3c
keywords:
- フレームワークオブジェクト WDK KMDF、コンテキスト空間
- コンテキスト空間 WDK KMDF
- オブジェクトコンテキスト空間 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af45e878f07d08e7b7f5c190870d06b901216498
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845303"
---
# <a name="framework-object-context-space"></a>フレームワーク オブジェクトのコンテキスト領域





*オブジェクトコンテキスト空間*は、ドライバーが割り当ててオブジェクトに割り当てることができる、追加の非ページングのメモリ領域です。 各フレームワークベースのドライバーは、ドライバーが受信または作成するすべてのフレームワークオブジェクトに対して、1つまたは複数のオブジェクト固有のコンテキストスペースを作成できます。

フレームワークベースのドライバーは、データが属するオブジェクトのコンテキスト空間内で、オブジェクト固有のすべてのデータを値またはポインターによって格納する必要があります。

たとえば、USB デバイスのドライバーによって、フレームワークのデバイスオブジェクトのコンテキスト空間が作成する場合があります。 コンテキスト空間では、デバイスの[**usb\_デバイス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_device_descriptor)と[**usb\_構成\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_configuration_descriptor)の構造体、デバイスインターフェイスのパイプを表す[コレクションオブジェクト](framework-object-collections.md)へのハンドルといった、デバイス固有の情報がドライバーに格納される場合があります。

フレームワークは、あるドライバーから別のドライバーにフレームワークオブジェクトを渡すのではなく、オブジェクトのコンテキスト空間を使用して2つのドライバー間でデータを渡すことはできません。

オブジェクトのコンテキスト空間を定義するには、1つまたは複数の構造体を作成する必要があります。 各構造体は、個別のコンテキスト空間を表します。 ドライバーは、各構造体メンバーを使用して、オブジェクト固有の情報の一部を格納します。 また、ドライバーは、各構造体の*アクセサーメソッド*を生成するようにフレームワークに要求する必要があります。 このアクセサーメソッドは、入力としてオブジェクトハンドルを受け取り、オブジェクトのコンテキスト空間のアドレスを返します。

[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)などのオブジェクトの作成方法をドライバーが呼び出すたびに、メソッドは必要に応じてコンテキスト空間を割り当てることができます。 すべてのオブジェクト作成メソッドは、省略可能な[**WDF\_オブジェクト\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)構造を入力として受け取ります。 この構造体は、フレームワークがオブジェクトに割り当てるコンテキスト空間を記述します。

ドライバーがオブジェクトの作成メソッドを呼び出した後、オブジェクトにコンテキスト空間を追加するには、ドライバーは[**WdfObjectAllocateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectallocatecontext)メソッドを呼び出すことができます。このメソッドは、オブジェクトの作成メソッドと同様に、 [**WDF\_オブジェクトを受け取り\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)入力としての属性の構造。

フレームワークは、オブジェクトのコンテキスト空間を割り当てるときに、コンテキスト空間をゼロ初期化します。

フレームワークまたはドライバーがフレームワークオブジェクトを削除すると、フレームワークによって、オブジェクトのすべてのコンテキスト空間が削除されます。

ドライバーがオブジェクトの作成時にドライバーによって割り当てられるバッファーへのポインターを格納するためにコンテキスト空間を使用する場合、ドライバーは、オブジェクトが削除されたときにバッファーを解放する[*Evtcleanupcallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)関数を提供する必要があります。

ドライバーが作成するオブジェクトのコンテキスト空間構造とアクセサーメソッドを定義するには、ドライバーで次の手順を実行する必要があります。

1.  格納するデータを記述する構造体を定義します。 たとえば、ドライバーのデバイスオブジェクトのコンテキストデータを作成する場合は、ドライバーが "MY\_DEVICE\_CONTEXT" という構造を定義することがあります。

2.  [**WDF\_declare\_context\_type**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdf-declare-context-type)マクロまたは\_WDF を使用して\_NAME マクロで\_\_[**型\_を宣言**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdf-declare-context-type-with-name)します。 これらのマクロはどちらも次のことを行います。

    -   [**コンテキスト\_型\_INFO 構造体\_、WDF\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_context_type_info)を作成し、初期化します。
    -   後でオブジェクトのコンテキスト空間にアクセスするためにドライバーが使用するアクセサーメソッドを定義します。 アクセサーメソッドの戻り値は、オブジェクトのコンテキスト空間へのポインターです。

    WDF\_DECLARE\_CONTEXT\_TYPE マクロは、構造体の名前からアクセサーメソッドの名前を作成します。 たとえば、コンテキスト構造の名前が MY\_DEVICE\_CONTEXT の場合、マクロは**Wdfobjectget\_my\_DEVICE\_context**という名前のアクセサーメソッドを作成します。

    WDF\_は、\_NAME マクロを使用して\_CONTEXT\_TYPE\_を宣言することで、アクセサーメソッドの名前を指定できます。 たとえば、デバイスオブジェクトのコンテキストアクセサーメソッドの名前として、 **Getmydevicecontext**を指定することができます。

3.  [**WDF\_オブジェクト\_\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdf_object_attributes_init)を呼び出して、オブジェクトの[**WDF\_オブジェクト\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)構造体を初期化します。

4.  [**WDF\_オブジェクト\_属性\_設定\_CONTEXT\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdf-object-attributes-set-context-type)マクロを使用して、WDF\_オブジェクト\_属性構造の**CONTEXTTYPEINFO**メンバーを WDF\_オブジェクトのアドレスに設定します。\_コンテキスト\_型\_INFO 構造体です。

5.  [**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)などのオブジェクトの作成メソッドを呼び出します。

ドライバーは、オブジェクトを作成した後、いつでも[**WdfObjectAllocateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectallocatecontext)を呼び出して、オブジェクトにコンテキスト空間を追加できます。

手順 1. と 2. では、グローバルデータ構造を定義し、ドライバー呼び出し可能ルーチンを作成するため、ドライバーは、グローバルデータを宣言するドライバーの領域 (通常はヘッダーファイル) でこれらの手順を完了する必要があります。 これらの手順は、ドライバーのルーチン内からは完了できません。

ドライバーは、 [**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出す[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数などのオブジェクトを作成するドライバールーチン内から、手順3、4、および5を完了する必要があります。

フレームワークでは、ドライバーに代わって、フレームワークの要求オブジェクトとフレームワークファイルオブジェクトという2種類のオブジェクトを作成できます。 ドライバーは、 [**Wdfdeviceinitsetrequestattributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetrequestattributes)と[**Wdfdeviceinitsetfileobjectconfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetfileobjectconfig)をそれぞれ呼び出して、これらのオブジェクトのコンテキスト空間を登録できます。 また、ドライバーは[**WdfObjectAllocateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectallocatecontext)を呼び出して、これらのオブジェクトのコンテキスト空間を割り当てることもできます。

オブジェクトが作成された後、ドライバーは、次のいずれかの方法を使用して、オブジェクトのコンテキスト空間へのポインターを取得できます。

-   前の手順の手順2で作成したコンテキストアクセサーメソッドを呼び出します。これには、 [**WDF\_declare\_context\_type**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdf-declare-context-type)または WDF を使用します。これにより、\_の\_[**型\_\_宣言\_NAME**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdf-declare-context-type-with-name)マクロ。

-   [**WdfObjectGetTypedContext**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectgettypedcontext)を呼び出して、ドライバーで定義されたコンテキスト構造の名前を指定します。

ドライバーにコンテキスト空間ポインターがある場合は、 [**Wdfobjectcontextgetobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectcontextgetobject)を呼び出すことによって、コンテキスト空間が属しているオブジェクトを見つけることができます。

 

 





