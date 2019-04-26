---
title: オブジェクト ハンドル
description: オブジェクト ハンドル
ms.assetid: deeeb3c0-54e4-4727-ac43-6da79be515d7
keywords:
- オブジェクトは、WDK のユーザー モードを処理します。
- オブジェクト ハンドル WDK カーネル
- WDK のユーザー モードを処理します。
- ハンドルの WDK カーネル
- プライベート オブジェクト ハンドル WDK
- 共有オブジェクト ハンドル WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0116e57bd1953033089eb766d5a4b1e325fc1328
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351068"
---
# <a name="object-handles"></a>オブジェクト ハンドル





ドライバーとユーザー モード コンポーネントを通じてほとんどのシステム定義オブジェクトへのアクセス*ハンドル*します。 ハンドルは、ハンドルの非透過データ型で表されます。 (ハンドルがデバイス オブジェクト、またはドライバーのオブジェクトへのアクセスに使用されないことに注意してください)。

ほとんどのオブジェクトの種類のカーネル モード ルーチンを作成するか、オブジェクトを開きますは呼び出し元にハンドルを提供します。 次に、呼び出し元は、オブジェクトに対する以降の操作でそのハンドルを使用してください。

ドライバーを使用して、通常、オブジェクトの種類とその型のオブジェクトへのハンドルを提供するルーチンの一覧を次に示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>オブジェクトの種類</th>
<th>対応する作成/オープン ルーチン</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ファイル</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548418" data-raw-source="[&lt;strong&gt;IoCreateFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548418)"><strong>IoCreateFile</strong></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566424" data-raw-source="[&lt;strong&gt;ZwCreateFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566424)"> <strong>ZwCreateFile</strong></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff567011" data-raw-source="[&lt;strong&gt;ZwOpenFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567011)"> <strong>ZwOpenFile</strong></a></p></td>
</tr>
<tr class="even">
<td><p>レジストリ キー</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549433" data-raw-source="[&lt;strong&gt;IoOpenDeviceInterfaceRegistryKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549433)"><strong>IoOpenDeviceInterfaceRegistryKey</strong></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff549443" data-raw-source="[&lt;strong&gt;IoOpenDeviceRegistryKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549443)"> <strong>IoOpenDeviceRegistryKey</strong></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566425" data-raw-source="[&lt;strong&gt;ZwCreateKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566425)"> <strong>ZwCreateKey</strong></a>、<a href="https://msdn.microsoft.com/library/windows/hardware/ff567014" data-raw-source="[&lt;strong&gt;ZwOpenKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567014)"> <strong>ZwOpenKey</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>スレッド数</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559932" data-raw-source="[&lt;strong&gt;PsCreateSystemThread&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559932)"><strong>PsCreateSystemThread</strong></a></p></td>
</tr>
<tr class="even">
<td><p>イベント</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549045" data-raw-source="[&lt;strong&gt;IoCreateSynchronizationEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549045)"><strong>IoCreateSynchronizationEvent</strong></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff549039" data-raw-source="[&lt;strong&gt;IoCreateNotificationEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549039)"> <strong>IoCreateNotificationEvent</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>シンボリック リンク</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567030" data-raw-source="[&lt;strong&gt;ZwOpenSymbolicLinkObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567030)"><strong>ZwOpenSymbolicLinkObject</strong></a></p></td>
</tr>
<tr class="even">
<td><p>ディレクトリ オブジェクト</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566421" data-raw-source="[&lt;strong&gt;ZwCreateDirectoryObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566421)"><strong>ZwCreateDirectoryObject</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>セクション オブジェクト</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567029" data-raw-source="[&lt;strong&gt;ZwOpenSection&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567029)"><strong>ZwOpenSection</strong></a></p></td>
</tr>
</tbody>
</table>

 

呼び出して不要になった、ドライバーには、オブジェクトへのアクセスが必要とする場合、 [ **ZwClose** ](https://msdn.microsoft.com/library/windows/hardware/ff566417)ルーチンをハンドルを終了します。 これは、上記の表に示すオブジェクトの種類のすべてに対して機能します。

ハンドルを提供するルーチンのほとんどを[**オブジェクト\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff557749)をパラメーターとして構造体。 ハンドルの属性を指定するのには、この構造体を使用できます。

ドライバーは、次のハンドルの属性を指定できます。

-   OBJ\_カーネル\_処理

    ハンドルは、カーネル モードからのみアクセスできます。

-   OBJ\_継承

    現在のプロセスのすべての子では、作成されるときに、ハンドルのコピーが表示されます。

-   OBJ\_FORCE\_アクセス\_チェック

    この属性は、システムがハンドルのすべてのアクセス チェックを実行することを指定します。 既定では、システムは、カーネル モードで作成されたハンドルに対するすべてのアクセス チェックをバイパスします。

使用して、 [ **InitializeObjectAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff547804)これらの属性を設定するルーチンを**オブジェクト\_属性**構造体。

オブジェクト ハンドルを検証する方法の詳細については、次を参照してください。[オブジェクト ハンドルの検証に失敗した](failure-to-validate-object-handles.md)します。

### <a name="private-object-handles"></a>プライベート オブジェクト ハンドル

ドライバーは、プライベート用オブジェクト ハンドルを作成、たびに、ドライバーが、OBJ を指定する必要があります\_カーネル\_ハンドルの属性。 これにより、ハンドルがユーザー モード アプリケーションにアクセスできること。

### <a name="shared-object-handles"></a>オブジェクト ハンドルを共有

カーネル モードとユーザー モードのオブジェクトのハンドルを共有するドライバーは、セキュリティ ホールを誤って作成しないようにする慎重に記述する必要があります。 いくつかのガイドラインを次に示します。

1.  カーネル モードでのハンドルを作成し、別の方法ではなく、ユーザー モードに渡したりします。 ユーザー モード コンポーネントによって作成され、ドライバーに渡されるハンドルを信頼することはできません。

2.  場合は、ドライバーは、ユーザー モード アプリケーションのためのハンドルを操作する必要があります、使用、OBJ\_FORCE\_アクセス\_アプリケーションに必要なアクセス権があることを確認する属性をチェックします。

3.  使用[ **ObReferenceObjectByPointer** ](https://msdn.microsoft.com/library/windows/hardware/ff558686)共有ハンドルでカーネル モードの参照を保持します。 それ以外の場合、参照カウントが 0 に、ユーザー モード コンポーネントは、ハンドルを閉じ場合と、システムがクラッシュし、ドライバーを使用して、またはハンドルを終了しようとするとします。

ユーザー モード アプリケーションでは、イベント オブジェクトを作成する場合、ドライバーがのみ場合、アプリケーションのハンドルをオブジェクトに渡すと、イベント IOCTL を使用してドライバーが、シグナルの状態にそのイベントの待機に安全にできます。 ドライバーは、イベントを作成したイベント ハンドルのハンドルは呼び出すことによって、検証する必要がありますプロセスのコンテキストでは、IOCTL を処理する必要があります[ **ObReferenceObjectByHandle**](https://msdn.microsoft.com/library/windows/hardware/ff558679)します。

 

 




