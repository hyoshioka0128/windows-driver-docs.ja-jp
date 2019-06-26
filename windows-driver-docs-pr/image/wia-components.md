---
title: WIA コンポーネント
description: WIA コンポーネント
ms.assetid: e75b8929-c16a-4c7a-9064-4fcb104bfa41
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30d6d474c1b2109f7fb7ba064e5fe60a8862ee35
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375368"
---
# <a name="wia-components"></a>WIA コンポーネント





WIA は、ユーザーと、ハードウェアの仲裁を複数のレイヤーで構成されます。 ユーザーは、省略可能なユーザー インターフェイスを持つことができる WIA アプリケーションと対話します。 このアプリケーションは、ミニドライバーにユーザーの要求を送信する、WIA サービスと通信します。 ミニドライバーは、関連するカーネル モードのバス ドライバーと通信します。 最後に、バス ドライバーは、ハードウェアと通信します。 次の図は、WIA インターフェイスを構成するソフトウェア コンポーネントを示しています。

![wia インターフェイスを構成するソフトウェア コンポーネントを示す図](images/art-1.png)

### <a name="imaging-applications"></a>イメージング アプリケーション

イメージング アプリケーションが、ミニドライバーと直接通信しないが、WIA イメージにアクセスし、WIA デバイスからのデータの取得 (WIA API) アプリケーション プログラミング インターフェイスを通じて WIA サービスと通信します。 これらのアプリケーションには、システム提供のユーザー インターフェイス (UI) またはデバイスの製造元が提供する 1 つを使用できます。 転送の項目を選択して、関連するプロパティを設定するのには、UI を使用します。 アプリケーション、ドライバーではなく、UI が消去された後に、選択した項目を転送することに注意してください。 イメージング アプリケーションの WIA API の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

### <a name="wia-service"></a>WIA サービス

WIA サービスは、イメージング アプリケーションと WIA ミニドライバーと通信するシステム提供のコンポーネントです。 WIA サービスには、Microsoft Windows SDK ドキュメントで説明されているは、次の表に記載されている COM インターフェイスのコレクションです。 WIA サービスは、WIA ミニドライバーと同じプロセスではアプリケーションから別のプロセスで実行されます。 アプリケーションでは、WIA サービスにデバイスの要求を送信します。 WIA サービスは、WIA デバイス ドライバー インターフェイス (WIA DDI) を使用し、これらの要求を適切なミニドライバーを指示します。 次の表では、WIA アプリケーションを実装できる Api を示します。

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
<td><p>WIA ハードウェア デバイスの機能を列挙します。 デバイスの機能には、コマンドと、デバイスをサポートするイベントが含まれます。</p></td>
</tr>
<tr class="even">
<td><p><strong>IEnumWIA_DEV_INFO</strong></p></td>
<td><p>WIA のハードウェア デバイスとそのプロパティを列挙します。 デバイス情報のプロパティは、インストールと WIA ハードウェア デバイスの構成について説明します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IEnumWIA_FORMAT_INFO</strong></p></td>
<td><p>デバイスの形式とメディアの種類の情報を列挙します。</p></td>
</tr>
<tr class="even">
<td><p><strong>IEnumWiaItem</strong></p></td>
<td><p>列挙<strong>IWiaItem</strong>ツリーの現在のフォルダー内のオブジェクト。 WIA 実行時のシステムをアプリケーションの階層ツリーにすべて WIA のハードウェア デバイスを表す<strong>IWiaItem</strong>オブジェクト。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IWiaDataCallback</strong></p></td>
<td><p>WIA ハードウェア デバイスからアプリケーションへのデータ転送中のアプリケーション コールバック機構を提供します。</p></td>
</tr>
<tr class="even">
<td><p><strong>IWiaDataTransfer</strong></p></td>
<td><p>デバイス オブジェクトから、アプリケーションにデータを転送する共有メモリ ウィンドウをサポートし、マーシャ リング中に不要なデータのコピーを排除します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IWiaDevMgr</strong></p></td>
<td><p>イメージの取得のデバイスを作成および管理アプリケーションで使用します。 デバイスのイベントを受け取るための登録を使用します。</p></td>
</tr>
<tr class="even">
<td><p><strong>IWiaEventCallback</strong></p></td>
<td><p>WIA ハードウェア デバイスのイベントの通知を受信するアプリケーションで使用します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IWiaItem</strong></p></td>
<td><p>その機能のクエリのデバイスにアプリケーションを有効にします。 <strong>IWiaItem</strong>データ転送インターフェイスおよびアイテム プロパティにもアクセスできます。 さらに、このインターフェイスは、デバイスを制御するアプリケーションを有効にするメソッドを提供します。</p></td>
</tr>
<tr class="even">
<td><p><strong>IWiaPropertyStorage</strong></p></td>
<td><p>に関する情報へのアクセスを提供します、 <strong>IWiaItem</strong>オブジェクトのプロパティ。</p></td>
</tr>
</tbody>
</table>

 

### <a name="wia-driver-services-library"></a>WIA ドライバー サービス ライブラリ

[WIA ドライバー サービス ライブラリ](wia-driver-services-library.md)WIA ミニドライバーのヘルパー関数を提供するシステム提供のコンポーネントです。 ミニドライバーは、次のタスクを実行するヘルパー関数を呼び出すことができます。

-   初期化、 [WIA ドライバー項目ツリー](wia-driver-item-tree.md)します。

-   読み取り、書き込み、およびデバイスのプロパティを検証します。

-   データを転送します。

また、ミニドライバーを実行できますなどのタスク自体。 ヘルパー関数を使用すると、開発時や WIA ミニドライバーのサイズを小さくし、個々 のソリューションを開発する柔軟性を備えていますができます。

### <a name="wia-utility-library"></a>WIA ユーティリティ ライブラリ

[WIA ユーティリティ ライブラリ](wia-utility-library.md)デバッグ用の関数のコレクションが含まれています (**wiauDbg * * * Xxx*)、一連の一般的なユーティリティのヘルパー関数と 3 つのクラス: **CWiauDbgFn**クラス、 **CWiauFormatConverter**クラス、および**CWiauPropertyList**クラス。

### <a name="wia-minidrivers"></a>WIA ミニドライバー

[WIA ミニドライバー](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)ベンダーから提供されたを WIA プロパティの変更と、イメージング デバイスにコマンドを直接ユーザー モード コンポーネント。 ミニドライバーは、WIA サービスを呼び出すようにミニドライバーとの通信に WIA DDI を実装します。

WIA ミニドライバーは、カーネル モード静止イメージ ドライバーにドライブを USB ドライバーなどのドライバーを介して、イメージング デバイスがデバイスに固有では、ユーザー モード インターフェイスを提供します。 ミニドライバーは、呼び出すことによって、カーネル モード ドライバーと通信する、 [ **CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)、 **ReadFile**、 **WriteFile**、および[ **DeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol) Microsoft Win32 関数 (これは、Microsoft Windows SDK ドキュメントで説明しています)。

イメージングのアプリケーションでは、WIA ミニドライバーを直接呼び出すことはできません。 WIA サービスのみでは、ドライバーを直接呼び出すことができます。

### <a name="kernel-io-drivers"></a>カーネル I/O ドライバー

静止画像のカーネル モード ドライバーは、静止画像デバイスへの配信、および静止画像デバイスからの転送データをパッケージ化するシステム提供または IHV 提供のコンポーネントです。 カーネル モードの静止イメージ ドライバーでは、bus 固有です。

Microsoft では Microsoft Windows Driver Model WDM ベースのカーネル モードもイメージのドライバー、SCSI、USB シリアル ポート、および IEEE 1394 バス。 これらのドライバーの詳細については、次を参照してください。[静止画像デバイスへのアクセスのカーネル モードのドライバー](accessing-kernel-mode-drivers-for-still-image-devices.md)します。

仕入先は、イメージング デバイスが I/O の Microsoft 提供のカーネル モード ドライバーと互換性がない場合にのみ、カーネル モード静止イメージ ドライバーを提供する必要があります。

**注**   Windows XP で、後で、ドライバーからバージョン情報を取得できます。 [ **WIA\_DIP\_WIA\_バージョン**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dip-wia-version)プロパティには、WIA バージョンが含まれていますと[ **WIA\_DIP\_ドライバー\_バージョン**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dip-driver-version)プロパティには、DLL バージョン ドライバーにはが含まれています。 WIA サービスを作成してこれらのプロパティの保持自動的に追加されます、WIA サービスによって、ドライバーが読み込まれるときにします。 Windows Me には、これらのプロパティは含まれません。

 

 

 




