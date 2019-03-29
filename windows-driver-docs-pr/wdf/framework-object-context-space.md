---
title: フレームワーク オブジェクトのコンテキスト領域
description: フレームワーク オブジェクトのコンテキスト領域
ms.assetid: 21a46e04-2330-4a3d-ba72-c04295bfbb3c
keywords:
- framework オブジェクト WDK KMDF、コンテキストの領域
- コンテキスト領域 WDK KMDF
- オブジェクト コンテキスト空間 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a0462ec2c152cca8c51ff36625a57b80535555c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573088"
---
# <a name="framework-object-context-space"></a>フレームワーク オブジェクトのコンテキスト領域





*オブジェクト コンテキスト領域*余分な非ページング、メモリ容量、ドライバーの割り当てとオブジェクトに割り当てることができます。 各フレームワーク ベースのドライバーがドライバーの受信または作成するすべての framework オブジェクトの 1 つまたは複数のオブジェクト固有のコンテキストのスペースを作成できます。

フレームワーク ベースのドライバーは、値またはポインターの場合、データが所属するオブジェクトのコンテキスト空間内のいずれか、すべてのオブジェクトに固有のデータを格納する必要があります。

たとえば、USB デバイス用のドライバーでは、そのフレームワークのデバイス オブジェクトのコンテキストの領域を作成します。 コンテキストの領域で、ドライバーは、デバイスのとしてこのようなデバイスに固有の情報を格納可能性があります[ **USB\_デバイス\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff539280)と[ **USB\_構成\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff539241)構造体とを識別するハンドルを[コレクション オブジェクト](framework-object-collections.md)デバイス インターフェイスのパイプを表します。

フレームワークは渡さない framework オブジェクト 1 つのドライバーから、ために 2 つのドライバーの間でデータを渡すオブジェクトのコンテキストの領域を使用することはできません。

オブジェクトのコンテキストの領域を定義するには、1 つまたは複数の構造を作成する必要があります。 各構造体は、別のコンテキストの領域を表します。 ドライバーでは、各構造体メンバーを使用して、特定のオブジェクトに固有の情報を格納します。 さらに、ドライバーが生成するためにフレームワークを求める必要があります、*アクセサー メソッド*の各構造体。 このアクセサー メソッドは、入力としてオブジェクトのハンドルを受け取り、オブジェクトのコンテキストの領域のアドレスを返します。

たびに、オブジェクトの作成メソッドを呼び出すには、ドライバーなど[ **WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)メソッドは、コンテキストの領域を必要に応じて割り当てます。 省略可能なすべてのオブジェクトの作成方法を受け入れる[ **WDF\_オブジェクト\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552400)入力として構造体します。 この構造体には、コンテキストの空間オブジェクトを割り当てるために、フレームワークですがについて説明します。

ドライバーが、オブジェクトの作成メソッドを呼び出した後、オブジェクトに追加のコンテキストの領域を追加するにはドライバーを呼び出すことができます、 [ **WdfObjectAllocateContext** ](https://msdn.microsoft.com/library/windows/hardware/ff548723)メソッド--などのオブジェクトを作成します。メソッドは、 [ **WDF\_オブジェクト\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552400)入力として構造体します。

フレームワークは、オブジェクト コンテキストの領域を割り当てますときに、も 0 に初期化コンテキスト領域。

フレームワークまたはドライバー フレームワーク オブジェクトを削除したときに、フレームワークはすべてのオブジェクトのコンテキストの領域を削除します。

ドライバー、ドライバーを提供する必要があります、オブジェクトの作成時に、ドライバーによって割り当てられるバッファーへのポインターを格納するコンテキストの領域を使用している場合、 [ *EvtCleanupCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540840)の割り当てを解除する関数、オブジェクトが削除された場合のバッファー。

オブジェクトのコンテキストの領域の構造とをドライバーで作成されるオブジェクトのアクセサー メソッドを定義するには、ドライバーは、次の手順を使用する必要があります。

1.  保存するデータを記述する構造体を定義します。 たとえば、ドライバーのデバイス オブジェクトのコンテキスト データを作成する場合は、ドライバー定義 MY と呼ばれる構造体\_デバイス\_コンテキスト。

2.  いずれかを使用して、 [ **WDF\_DECLARE\_コンテキスト\_型**](https://msdn.microsoft.com/library/windows/hardware/ff551250)マクロまたは[ **WDF\_DECLARE\_コンテキスト\_型\_WITH\_名前**](https://msdn.microsoft.com/library/windows/hardware/ff551252)マクロ。 これらのマクロの両方を以下に示します。

    -   作成し、初期化、 [ **WDF\_オブジェクト\_コンテキスト\_型\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff552407)構造体。
    -   オブジェクトのコンテキストの領域にアクセスするには、ドライバーを後で使用するアクセサー メソッドを定義します。 アクセサー メソッドの戻り値は、オブジェクトのコンテキストの領域へのポインターです。

    WDF\_DECLARE\_コンテキスト\_マクロは、構造体の名前からアクセサー メソッドの名前を作成します。 たとえば、コンテキスト構造体の名前は MY\_デバイス\_コンテキスト、マクロを作成するアクセサー メソッドの名前は**WdfObjectGet\_MY\_デバイス\_コンテキスト**.

    WDF\_DECLARE\_コンテキスト\_型\_WITH\_名マクロを使用して、アクセサー メソッドの名前を指定できます。 たとえば、指定する場合があります**GetMyDeviceContext**デバイス オブジェクトのコンテキストのアクセサー メソッドの名前として。

3.  呼び出す[ **WDF\_オブジェクト\_属性\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/ff552402)オブジェクトの初期化に[ **WDF\_オブジェクト\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552400)構造体。

4.  使用して、 [ **WDF\_オブジェクト\_属性\_設定\_コンテキスト\_型**](https://msdn.microsoft.com/library/windows/hardware/ff552405)マクロを設定する、 **ContextTypeInfo** 、WDF のメンバー\_オブジェクト\_属性の構造体、WDF のアドレスに\_オブジェクト\_コンテキスト\_型\_情報構造体。

5.  など、オブジェクトの作成メソッドを呼び出す[ **WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)します。

ドライバーを呼び出すことができます、ドライバーには、オブジェクトが作成、 [ **WdfObjectAllocateContext** ](https://msdn.microsoft.com/library/windows/hardware/ff548723)いつでも、オブジェクトに追加のコンテキストの領域を追加します。

手順 1. および 2. では、グローバル データ構造を定義し、ドライバーから呼び出し可能なルーチンを作成、ためには、ドライバーは--ヘッダー ファイルでは通常のグローバルなデータを宣言するドライバーの領域で手順を完了する必要があります。 ドライバーのルーチン内から、これらの手順を完了しない必要があります。

ドライバーは、3、4、およびなど、オブジェクトを作成するドライバー ルーチン内から 5 の手順を完了する必要があります、 [ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック関数を呼び出す[ **WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)します。

フレームワークには、2 種類のドライバーに代わって--framework 要求オブジェクトと framework ファイル オブジェクト - のオブジェクトを作成できます。 ドライバーは、呼び出すことによってこれらのオブジェクト コンテキストの領域を登録できます[ **WdfDeviceInitSetRequestAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff546786)と[ **WdfDeviceInitSetFileObjectConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff546107)、それぞれします。 ドライバーを呼び出すことも[ **WdfObjectAllocateContext** ](https://msdn.microsoft.com/library/windows/hardware/ff548723)にこれらのオブジェクトをコンテキストの領域を割り当てられません。

オブジェクトが作成された後、ドライバーは、次の手法のいずれかを使用して、オブジェクトのコンテキストの領域へのポインターを取得できます。

-   いずれかを使用して、前の手順では、手順 2. で作成したコンテキストのアクセサー メソッドを呼び出して、 [ **WDF\_DECLARE\_コンテキスト\_型**](https://msdn.microsoft.com/library/windows/hardware/ff551250)または、 [**WDF\_DECLARE\_コンテキスト\_型\_WITH\_名前**](https://msdn.microsoft.com/library/windows/hardware/ff551252)マクロ。

-   呼び出す[ **WdfObjectGetTypedContext**](https://msdn.microsoft.com/library/windows/hardware/ff548749)、ドライバーによって定義されたコンテキストの構造の名前を指定します。

呼び出してコンテキスト領域が属するオブジェクトを見つけることができます、ドライバーに領域のコンテキスト ポインターがある場合は、 [ **WdfObjectContextGetObject**](https://msdn.microsoft.com/library/windows/hardware/ff548727)します。

 

 





