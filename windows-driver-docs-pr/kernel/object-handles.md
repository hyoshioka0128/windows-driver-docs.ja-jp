---
title: オブジェクトハンドル
description: オブジェクトハンドル
ms.assetid: deeeb3c0-54e4-4727-ac43-6da79be515d7
keywords:
- オブジェクトが WDK ユーザーモードを処理する
- オブジェクトは WDK カーネルを処理します
- WDK ユーザーモードを処理する
- WDK カーネルを処理します
- プライベートオブジェクトが WDK を処理する
- WDK を処理する共有オブジェクト
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 500ff5f6c66aa2bac7a3dced8f3eabbd0b3387d0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838529"
---
# <a name="object-handles"></a>オブジェクトハンドル





ドライバーとユーザーモードコンポーネントは、*ハンドル*を通じて、システム定義のほとんどのオブジェクトにアクセスします。 ハンドルは、HANDLE 不透明データ型によって表されます。 (ハンドルは、デバイスオブジェクトやドライバーオブジェクトへのアクセスには使用されないことに注意してください)。

ほとんどのオブジェクトの種類では、オブジェクトを作成または開くカーネルモードルーチンによって、呼び出し元へのハンドルが提供されます。 その後、呼び出し元は、オブジェクトに対する後続の操作で、そのハンドルを使用します。

ドライバーが通常使用するオブジェクトの種類と、その型のオブジェクトにハンドルを提供するルーチンの一覧を次に示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>オブジェクトの種類</th>
<th>対応する作成/オープンルーチン</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ファイル</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatefile" data-raw-source="[&lt;strong&gt;IoCreateFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatefile)"><strong>Iocreatefile</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile" data-raw-source="[&lt;strong&gt;ZwCreateFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)"><strong>zwcreatefile</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntopenfile" data-raw-source="[&lt;strong&gt;ZwOpenFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntopenfile)"><strong>zwcreatefile</strong></a></p></td>
</tr>
<tr class="even">
<td><p>レジストリキー</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceinterfaceregistrykey" data-raw-source="[&lt;strong&gt;IoOpenDeviceInterfaceRegistryKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceinterfaceregistrykey)"><strong>IoOpenDeviceInterfaceRegistryKey</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey" data-raw-source="[&lt;strong&gt;IoOpenDeviceRegistryKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey)"><strong>IoOpenDeviceRegistryKey</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekey" data-raw-source="[&lt;strong&gt;ZwCreateKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekey)"><strong>ZwCreateKey</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkey" data-raw-source="[&lt;strong&gt;ZwOpenKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkey)"><strong>zwopenkey</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>Threads</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pscreatesystemthread" data-raw-source="[&lt;strong&gt;PsCreateSystemThread&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pscreatesystemthread)"><strong>PsCreateSystemThread</strong></a></p></td>
</tr>
<tr class="even">
<td><p>イベント</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatesynchronizationevent" data-raw-source="[&lt;strong&gt;IoCreateSynchronizationEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatesynchronizationevent)"><strong>IoCreateSynchronizationEvent</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatenotificationevent" data-raw-source="[&lt;strong&gt;IoCreateNotificationEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatenotificationevent)"> <strong>IoCreateNotificationEvent</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>シンボリック リンク</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopensymboliclinkobject" data-raw-source="[&lt;strong&gt;ZwOpenSymbolicLinkObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopensymboliclinkobject)"><strong>ZwOpenSymbolicLinkObject</strong></a></p></td>
</tr>
<tr class="even">
<td><p>ディレクトリ オブジェクト</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatedirectoryobject" data-raw-source="[&lt;strong&gt;ZwCreateDirectoryObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatedirectoryobject)"><strong>ZwCreateDirectoryObject</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>Section オブジェクト</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopensection" data-raw-source="[&lt;strong&gt;ZwOpenSection&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopensection)"><strong>ZwOpenSection</strong></a></p></td>
</tr>
</tbody>
</table>

 

ドライバーがオブジェクトへのアクセスを必要としなくなった場合は、 [**Zwclose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)ルーチンを呼び出してハンドルを閉じます。 これは、上の表に一覧表示されているすべてのオブジェクトの種類に対して機能します。

ハンドルを提供するルーチンのほとんどは、[**オブジェクト\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/ns-wudfwdm-_object_attributes)構造をパラメーターとして受け取ります。 この構造体を使用して、ハンドルの属性を指定できます。

ドライバーでは、次のハンドル属性を指定できます。

-   OBJ\_カーネル\_ハンドル

    ハンドルには、カーネルモードからのみアクセスできます。

-   OBJ\_継承

    現在のプロセスのすべての子は、ハンドルのコピーを作成時に受け取ります。

-   OBJ\_強制的に\_アクセス\_チェック

    この属性は、システムがハンドルに対するすべてのアクセスチェックを実行することを指定します。 既定では、カーネルモードで作成されたハンドルのすべてのアクセスチェックをバイパスします。

[**Initializeobjectattributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/nf-wudfwdm-initializeobjectattributes)ルーチンを使用して、**オブジェクト\_属性**構造でこれらの属性を設定します。

オブジェクトハンドルの検証の詳細については、「[オブジェクトハンドルの検証エラー](failure-to-validate-object-handles.md)」を参照してください。

### <a name="private-object-handles"></a>プライベートオブジェクトハンドル

ドライバーがプライベートに使用するオブジェクトハンドルを作成するたびに、ドライバーは、OBJ\_KERNEL\_HANDLE 属性を指定する必要があります。 これにより、ユーザーモードアプリケーションがハンドルにアクセスできなくなります。

### <a name="shared-object-handles"></a>共有オブジェクトハンドル

カーネルモードとユーザーモードの間でオブジェクトハンドルを共有するドライバーは、誤ってセキュリティホールを作成しないように注意して記述する必要があります。 いくつかのガイドラインを次に示します。

1.  カーネルモードでハンドルを作成し、他の方法ではなくユーザーモードに渡します。 ユーザーモードコンポーネントによって作成され、ドライバーに渡されるハンドルは信頼できません。

2.  ドライバーがユーザーモードアプリケーションの代わりにハンドルを操作する必要がある場合は、OBJ\_FORCE\_ACCESS\_CHECK 属性を使用して、アプリケーションに必要なアクセス権があることを確認します。

3.  共有ハンドルにカーネルモードの参照を保持するには、 [**Obreferenceobjectbypointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbypointer)を使用します。 それ以外の場合、ユーザーモードコンポーネントがハンドルを閉じると、参照カウントはゼロになり、ドライバーがハンドルを使用または終了しようとすると、システムがクラッシュします。

ユーザーモードアプリケーションでイベントオブジェクトを作成した場合、ドライバーはそのイベントがシグナル状態になるまで安全に待機できますが、アプリケーションが IOCTL 経由でイベントオブジェクトへのハンドルをドライバーに渡す場合に限られます。 ドライバーは、イベントを作成したプロセスのコンテキストで IOCTL を処理する必要があり、 [**Obreferenceobjectbyhandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)を呼び出すことによってハンドルがイベントハンドルであることを検証する必要があります。

 

 




