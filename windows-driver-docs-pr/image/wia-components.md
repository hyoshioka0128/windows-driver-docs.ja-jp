---
title: WIA コンポーネント
description: WIA コンポーネント
ms.assetid: e75b8929-c16a-4c7a-9064-4fcb104bfa41
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18fa5f16f719f8b6c154e827ae496c9748ddd5fb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840721"
---
# <a name="wia-components"></a>WIA コンポーネント





WIA は、ユーザーとハードウェアの間を仲裁複数のレイヤーで構成されています。 ユーザーは、オプションのユーザーインターフェイスを持つことができる WIA アプリケーションと対話します。 このアプリケーションは、ユーザーの要求をミニドライバーに送信する WIA サービスと通信します。 ミニドライバーは、関連するカーネルモードバスドライバーと通信します。 最後に、バスドライバーはハードウェアと通信します。 次の図は、WIA インターフェイスを構成するソフトウェアコンポーネントを示しています。

![wia インターフェイスを構成するソフトウェアコンポーネントを示す図](images/art-1.png)

### <a name="imaging-applications"></a>アプリケーションのイメージング

イメージングアプリケーションはミニドライバーと直接通信しませんが、wia アプリケーションプログラミングインターフェイス (WIA API) を介して wia サービスと通信して、イメージにアクセスし、WIA デバイスからデータを取得します。 これらのアプリケーションでは、システムによって提供されるユーザーインターフェイス (UI) またはデバイスの製造元が提供するものを使用できます。 UI は、転送する項目を選択し、関連するプロパティを設定するために使用されます。 UI が破棄された後に選択した項目が転送されるのは、ドライバーではなくアプリケーションであることに注意してください。 アプリケーションのイメージング用の WIA API の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

### <a name="wia-service"></a>WIA サービス

WIA サービスは、イメージングアプリケーションと WIA ミニドライバーと通信するシステム提供のコンポーネントです。 WIA サービスは、次の表に記載されている COM インターフェイスのコレクションです。これらのインターフェイスについては、Microsoft Windows SDK のドキュメントを参照してください。 WIA サービスは、アプリケーションとは異なるプロセスで、WIA ミニドライバーと同じプロセスで実行されます。 アプリケーションは、デバイスの要求を WIA サービスに送信します。 次に、wia サービスは、wia デバイスドライバーインターフェイス (WIA DDI) を使用して、これらの要求を適切なミニドライバーに送信します。 次の表に、WIA アプリケーションで実装できる Api を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>WIA API</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>IEnumWIA_DEV_CAPS</strong></p></td>
<td><p>WIA ハードウェアデバイスの機能を列挙します。 デバイス機能には、デバイスがサポートするコマンドとイベントが含まれます。</p></td>
</tr>
<tr class="even">
<td><p><strong>IEnumWIA_DEV_INFO</strong></p></td>
<td><p>WIA ハードウェアデバイスとそのプロパティを列挙します。 デバイス情報のプロパティは、WIA ハードウェアデバイスのインストールと構成について説明します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IEnumWIA_FORMAT_INFO</strong></p></td>
<td><p>デバイスの形式とメディアタイプ情報を列挙します。</p></td>
</tr>
<tr class="even">
<td><p><strong>IEnumWiaItem</strong></p></td>
<td><p>ツリーの現在のフォルダー内の<strong>Iwiaitem</strong>オブジェクトを列挙します。 WIA ランタイムシステムは、すべての WIA ハードウェアデバイスを、 <strong>Iwiaitem</strong>オブジェクトの階層ツリーとしてアプリケーションに対して表します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IWiaDataCallback</strong></p></td>
<td><p>WIA ハードウェアデバイスからアプリケーションへのデータ転送中に、アプリケーションコールバックメカニズムを提供します。</p></td>
</tr>
<tr class="even">
<td><p><strong>IWiaDataTransfer</strong></p></td>
<td><p>は、デバイスオブジェクトからアプリケーションにデータを転送する共有メモリウィンドウをサポートし、マーシャリング中に不要なデータコピーを排除します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IWiaDevMgr</strong></p></td>
<td><p>イメージ取得デバイスを作成および管理するためにアプリケーションによって使用されます。 また、デバイスイベントを受信するための登録にも使用します。</p></td>
</tr>
<tr class="even">
<td><p><strong>IWiaEventCallback</strong></p></td>
<td><p>アプリケーションが WIA ハードウェアデバイスイベントの通知を受信するために使用されます。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IWiaItem</strong></p></td>
<td><p>アプリケーションがデバイスの機能を照会できるようにします。 <strong>Iwiaitem</strong>は、データ転送インターフェイスおよび項目プロパティへのアクセスも提供します。 また、このインターフェイスには、アプリケーションがデバイスを制御できるようにするメソッドが用意されています。</p></td>
</tr>
<tr class="even">
<td><p><strong>IWiaPropertyStorage</strong></p></td>
<td><p><strong>Iwiaitem</strong>オブジェクトのプロパティに関する情報へのアクセスを提供します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="wia-driver-services-library"></a>WIA ドライバー サービス ライブラリ

[Wia ドライバーサービスライブラリ](wia-driver-services-library.md)は、wia ミニドライバーのヘルパー機能を提供するシステム提供のコンポーネントです。 ミニドライバーは、次のようなタスクを実行するヘルパー関数を呼び出すことができます。

-   [WIA ドライバーの項目ツリー](wia-driver-item-tree.md)を初期化します。

-   デバイスプロパティの読み取り、書き込み、および検証を行います。

-   データを転送します。

また、ミニドライバーはこのようなタスクを実行できます。 ヘルパー関数を使用すると、開発時間と WIA ミニドライバーのサイズを減らすことができ、さらに個々のソリューションを柔軟に開発できます。

### <a name="wia-utility-library"></a>WIA ユーティリティ ライブラリ

[WIA ユーティリティライブラリ](wia-utility-library.md)には、一連のデバッグ機能 (**wi/dbg * * * Xxx*)、一般的なユーティリティヘルパー関数のコレクション、および Cwi/ **Dbgfn**クラス、 **Cwi/Formatconverter**クラス、 **cwiて propertylist**クラスが含まれています。

### <a name="wia-minidrivers"></a>WIA ミニドライバー

[Wia ミニドライバー](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)は、モデル化されたユーザーモードのコンポーネントであり、wia プロパティの変更やコマンドをイメージングデバイスに転送します。 ミニドライバーは、wia サービスがミニドライバーと通信するために呼び出す WIA DDI を実装します。

WIA ミニドライバーは、デバイス固有のユーザーモードインターフェイスをカーネルモード静止イメージドライバーに提供します。これにより、USB ドライバーなどのドライバーを使用してイメージングデバイスが実行されます。 ミニドライバーは、 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)、 **ReadFile**、 **WriteFile**、および[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)の Microsoft Win32 関数 (Microsoft Windows SDK のドキュメントで説明されています) を呼び出すことによって、カーネルモードドライバーと通信します。

イメージングアプリケーションは、WIA ミニドライバーを直接呼び出すことはできません。 ドライバーを直接呼び出すことができるのは、WIA サービスだけです。

### <a name="kernel-io-drivers"></a>カーネル i/o ドライバー

カーネルモードのイメージドライバーは、システムによって提供されるか、または送信するデータをイメージデバイスにパッケージ化し、静止イメージデバイスから転送するコンポーネントです。 カーネルモードの静止イメージドライバーはバス固有です。

Microsoft では、USB、SCSI、シリアル、および IEEE 1394 バス用に、Microsoft Windows Driver Model (WDM) ベースのカーネルモードのイメージドライバーを提供しています。 これらのドライバーの詳細については、「[イメージデバイス用のカーネルモードドライバーへのアクセス](accessing-kernel-mode-drivers-for-still-image-devices.md)」を参照してください。

ベンダーは、イメージングデバイスが Microsoft が提供するカーネルモード i/o ドライバーと互換性がない場合にのみ、カーネルモードの静止イメージドライバーを提供する必要があります。

**注**   Windows XP 以降では、ドライバーからバージョン情報を取得できます。 Wia [ **\_dip\_wia\_version**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dip-wia-version)プロパティには、wia バージョンが含まれています。また、 [**wia\_DIP\_driver\_version**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dip-driver-version)プロパティには、ドライバーの DLL バージョンが含まれています。 これらのプロパティは、WIA サービスによって作成および管理されます。これらは、ドライバーが読み込まれるときに、WIA サービスによって自動的に追加されます。 Windows Me には、これらのプロパティは含まれていません。

 

 

 




