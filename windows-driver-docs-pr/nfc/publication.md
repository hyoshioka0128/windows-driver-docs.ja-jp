---
title: NFP メッセージの公開
description: NFP メッセージの公開
ms.assetid: 45BE3620-ADF4-413D-90B3-586FCEB5F606
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4eb0aa6abc565c48d4917a2a1556f88208df40e1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838097"
---
# <a name="publishing-nfp-messages"></a>NFP メッセージの公開


パブリケーションは、ドライバー内で開かれている一意のハンドルとして表されます。 アクティブなパブリケーションには、型とデータバッファーの両方が必要です。 型を設定するには、"Pubs" 名前空間のファイル名を開きます。 データバッファーは、 [**IOCTL\_NFP\_set\_ペイロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_set_payload)を送信することによって設定されます。

試行された送信のコールバックは、完了した[**IOCTL\_NFP\_、\_次\_送信\_メッセージを取得**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_get_next_transmitted_message)することによって与えられます。

パブリケーションは、 [**IOCTL\_NFP\_DISABLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_disable)を使用して一時的に無効にすることができます。

パブリケーションは、 [**IOCTL\_NFP\_ENABLE を**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_enable)使用して再度有効にすることができます。

##  <a name="handles"></a>ハンドル数


メッセージを公開するクライアントは、まずドライバーへの新しいハンドルを開きます。 以前のパブリケーションやサブスクリプションなどのハンドルを再利用することはできません。 これらが不要になった場合は、適切に動作するクライアントによって閉じられます。

クライアントは、"Pubs/&lt;プロトコル&gt;でファイルハンドルを開きます。&lt;サブタイプ&gt;"デバイス相対名前空間。 完全な例を次に示します。

``` syntax
\\?\root#ContosoProx#0000#{FB3842CD-9E2A-4F83-8FCC-4B0761139AE9}\Pubs\Windows.windows.com/SD
<---------------Device Interface Symbolic Link-----------------> <------File Name---------->
    <--------------------><------------------------------------> <--> <-----> <------------>
          DeviceID          NearFieldProximity Interface Class     *  Protocol   SubType
```

ハンドルを開いた後、クライアントは、 [**IOCTL\_NFP\_set\_ペイロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_set_payload)を使用して、公開されるメッセージのペイロードを設定する必要があります。

指定されたファイル名 (パブリケーションの種類) を読み取る機能がありません。

### <a name="file-name"></a>ファイル名

ドライバーの*CreateFile*ハンドラーでは、デバイスインターフェイス*SymbolicLink*は削除され、デバイスの相対ファイル名のみが保持されます。 このファイル名は、パブリケーション (またはサブスクリプション) の種類を示す null で終わる、大文字と小文字を区別する UTF 16LE 文字列バッファーです。 このバッファーの最大サイズは、NULL 終端文字を含む502文字です。 ドライバーは、このパスを "Pubs\\"、"protocol"、"subtype" の3つの構成要素に解析する必要があります。

### <a name="required-actions"></a>必要なアクション

-   ドライバーは、プロトコルコンポーネント (最初の '. ' の前) を解析する必要があります。 認識されていないプロトコルは、ステータス\_オブジェクト\_パスで完了する必要があり\_\_見つかりません
-   文字列がバッファーの長さ内で NULL で終了しない場合、ドライバーは、状態\_無効な\_パラメーターを持つ IOCTL を完了する必要があります。
-   プロトコルにサブタイプが必要で、文字列バッファーのサブタイプコンポーネントが 1 (1) 文字未満または250文字を超える場合、ドライバーは状態\_無効\_パラメーターを持つ IOCTL を完了する必要があります。
-   文字列バッファーのプロトコルコンポーネントが250文字を超えている場合、ドライバーは、状態\_無効\_パラメーターを持つ IOCTL を完了する必要があります。
-   ドライバーは、最初の NULL を文字列の末尾として解釈する必要があります。
-   ドライバーは、パブリケーションの "ペアリング: Bluetooth" の種類を認識する場合があります。 ドライバーは、互換性を維持するために、この種類を認識することがあります。 (ピリオドを使用するのではなく、コロンを使用することに注意してください)。
-   ドライバーは、"WindowsUri" 型を認識している必要があります。
-   ドライバーは、サブスクリプションの "DeviceArrived" の種類のみを認識している必要があります。
-   ドライバーでは、サブスクリプションの "デバイスが使用されていません" の種類を認識している必要があります。
-   ドライバーでは、サブスクリプションの "WindowsMime" の種類のみを認識している必要があります。
-   ドライバーは "WindowsMime" を認識している必要があります。 各種.
-   プロトコルがサブスクリプションに対してのみ認識され、IOCTL が "Pubs\\" を指定している場合、ドライバーは、状態\_オブジェクト\_パス\_が見つから\_なかったことを示す IOCTL を完了する必要があります。
-   プロトコルがパブリケーションに対してのみ認識され、IOCTL が "Sub\\" を指定している場合、ドライバーは、状態\_オブジェクト\_パス\_が見つからない\_ことを示す IOCTL を完了する必要があります。
-   同じ型の2つの開いているハンドルは、2つの異なるエンティティを表す必要があります。
-   一部のプロトコル (名前空間) は予約されています。 このドキュメントで明示的に指定されていない限り、ドライバーは次の文字で始まるプロトコルを認識できません。
    -   ウィンドウ
    -   ドライブ
    -   組み合わせる
    -   "NDEF"
    -   NFC
    -   "Iso14443Dep"
    -   "Iso14443TypeA"
    -   "Iso14443TypeB"
    -   "Iso15693Vicinity"
    -   "MifareClassic"
    -   "MifareUltralight"
    -   "FeliCa"

## <a name="unpublish"></a>解除


クライアントがメッセージを公開する必要がなくなった場合は、パブリケーションハンドルを閉じます。 これは、メッセージが送信されなくなることを示します。 クライアントプロセスが終了すると、クライアントの代わりに開いているすべてのファイルハンドルが閉じられます。

### <a name="required-actions"></a>必要なアクション

-   ハンドルが閉じられると (IRP\_MJ\_CLOSE)、ドライバーは次のようになります。
    -   は、パブリケーションで使用されているすべてのメモリ (型とメッセージデータの両方) を再利用する必要があります。ただし、このパブリケーションを継続的に送信するためのバッファーは除きます。
    -   将来、デバイスが近接になった場合は、メッセージを送信しないようにしてください。
    -   パブリケーションの進行中の転送を中断することはできません。
-   ドライバーは、IRP\_MJ\_クリーンアップを無視する場合があります。

クライアントがメッセージを2回公開する場合、ドライバーは、デバイスが近接しているときにメッセージが2回送信されることを前提としています。

### <a name="required-actions"></a>必要なアクション

同じクライアントによって発行された場合でも、ドライバーは重複する公開メッセージを受け入れて送信する必要があります。

### <a name="required-actions"></a>必要なアクション


クライアントが置換された 10-20 [ **\_\_\_\_\_IOCTL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_get_next_subscribed_message)を送信しなかった場合、ドライバーは "Received" キューからすべてのメッセージ (およびそれらのリソースの回収) を削除する必要がありますIOCTL の完了。

## <a name="unresponsive-or-misbehaving-clients"></a>クライアントの応答不能または誤動作


クライアントが必要な IOCTL\_NFP の送信に失敗した場合は、10 ~ 20 秒\_10-20sec \[10 ~ 20 秒の期間にわたって[ **\_次\_送信\]メッセージ要求\_取得**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_get_next_transmitted_message)します。 通常の状況では、クライアントは1秒 \[1s\]内の要求を適切に更新する必要があります。 この場合、ドライバーは "CompleteEventImmediately" カウンターを0に設定し、クライアントがウェイクアップして必要な IRP を送信するまでカウンターを増やさないようにする必要があります。

### <a name="required-actions"></a>必要なアクション

ドライバーは、"CompleteEventImmediately" カウンターを0に設定する必要があります。また、クライアントが置換された\_IOCTL を送信していない場合は、10-20 秒以内に[ **\_次\_送信\_メッセージ\_取得**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_get_next_transmitted_message)するようにしてください。以前の IOCTL 完了の。

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[近距離無線近接 DDI リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

