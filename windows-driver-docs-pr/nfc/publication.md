---
title: 発行 NFP メッセージ
description: 発行 NFP メッセージ
ms.assetid: 45BE3620-ADF4-413D-90B3-586FCEB5F606
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6955f0d4a63a68633c0f321a7af371e47a7a0133
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386517"
---
# <a name="publishing-nfp-messages"></a>発行 NFP メッセージ


パブリケーションは、ドライバー内で一意のオープン ハンドルとして表されます。 アクティブな発行は、型とデータ バッファーの両方が必要です。 ファイル名を"Pubs"名前空間で開くことで、型が設定されています。 データ バッファーを送信することによって設定[ **IOCTL\_NFP\_設定\_ペイロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfpdev/ni-nfpdev-ioctl_nfp_set_payload)します。

実行しようとした伝送でのコールバックを指定を通じて、完了した[ **IOCTL\_NFP\_取得\_次\_送信\_メッセージ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfpdev/ni-nfpdev-ioctl_nfp_get_next_transmitted_message).

使用してパブリケーションが一時的に無効にできますが、 [ **IOCTL\_NFP\_を無効にする**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfpdev/ni-nfpdev-ioctl_nfp_disable)します。

パブリケーションを使用して再度有効にすることができます、 [ **IOCTL\_NFP\_を有効にする**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfpdev/ni-nfpdev-ioctl_nfp_enable)します。

##  <a name="handles"></a>ハンドル数


メッセージを発行する必要があるクライアントはまず、ドライバーへの新しいハンドルを開きます。 以前のパブリケーション、サブスクリプション、およびからのハンドルを再利用することはできません。 必要がなくなったらは、適切に動作するクライアントによって閉じられます。

クライアントがファイル ハンドルを開く、"Pubs/&lt;プロトコル&gt;.&lt;サブタイプ&gt;"デバイス依存の名前空間。 完全な例を次に示します。

``` syntax
\\?\root#ContosoProx#0000#{FB3842CD-9E2A-4F83-8FCC-4B0761139AE9}\Pubs\Windows.windows.com/SD
<---------------Device Interface Symbolic Link-----------------> <------File Name---------->
    <--------------------><------------------------------------> <--> <-----> <------------>
          DeviceID          NearFieldProximity Interface Class     *  Protocol   SubType
```

ハンドルを開いた後、クライアント設定する必要がありますし、公開するメッセージのペイロード、 [ **IOCTL\_NFP\_設定\_ペイロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfpdev/ni-nfpdev-ioctl_nfp_set_payload)します。

指定したファイル名 (パブリケーションの種類) を読み取るための機能はありません。

### <a name="file-name"></a>ファイル名

ドライバーの*CreateFile*ハンドラー、デバイス インターフェイス*SymbolicLink*取り除かは、デバイスの相対ファイル名のみが残ります。 このファイル名を null で終わる大文字 UTF 16LE 文字列バッファーの文書 (またはサブスクリプション) の種類を示すとなります。 このバッファーの最大サイズには、NULL ターミネータを含めた 502 の文字です。 ドライバーは、次の 3 つの構成要素にこのパスを解析する必要があります。"Pubs\\"、プロトコル、およびサブタイプします。

### <a name="required-actions"></a>必要な操作

-   ドライバーは、プロトコルのコンポーネントを解析する必要があります (1 つ目の前に '.')。 状態が認識されない任意のプロトコルを完了する必要があります\_オブジェクト\_パス\_いない\_が見つかりました
-   ドライバーがステータスの IOCTL を完了する必要があります、文字列が NULL で終わるバッファーの長さでない場合、\_無効な\_パラメーター。
-   ドライバーがステータスの IOCTL を完了する必要があります、プロトコルがサブタイプを必要とし、文字列バッファーのサブタイプのコンポーネントが 1 未満です (1) 文字または 250 文字より長くする場合\_無効な\_パラメーター。
-   文字列バッファーのプロトコルのコンポーネントが 250 文字より長い場合は、ドライバーがステータスの IOCTL を完了する必要があります\_無効な\_パラメーター。
-   ドライバーは、文字列の末尾として最初に NULL を解釈する必要があります。
-   ドライバーは、パブリケーションの種類"ペアリング: Bluetooth"を認識できます。 ドライバーは、互換性を維持するためにこの型を認識する可能性があります。 (コロンを使用ではなく、期間の使用に注意してください)。
-   ドライバーは、"WindowsUri"の種類を認識する必要があります。
-   ドライバーでは、サブスクリプションだけ"DeviceArrived"の種類を認識する必要があります。
-   ドライバーでは、サブスクリプションだけ"DeviceDeparted"の種類を認識する必要があります。
-   ドライバーでは、サブスクリプションだけ"WindowsMime"の種類を認識する必要があります。
-   ドライバーは"WindowsMime"を認識する必要があります。 入力します。
-   かどうかは、プロトコルは、サブスクリプションの場合のみ認識される必要があり、IOCTL を指定します"Pubs\\"、ドライバーは、IOCTL 状態を完了する必要があります\_オブジェクト\_パス\_いない\_が見つかりました。
-   かどうかは、プロトコルは、パブリケーションの場合のみ認識される必要があり、IOCTL を指定します"サブ\\"、ドライバーは、IOCTL 状態を完了する必要があります\_オブジェクト\_パス\_いない\_が見つかりました。
-   同じ型に 2 つの開いているハンドルは、2 つの個別のエンティティを表す必要があります。
-   一部のプロトコル (名前空間) は予約されています。 このドキュメントで明示的に指定しない限り、MUST NOT ドライバーがで始まるすべてのプロトコルを認識します。
    -   "Windows"
    -   「デバイス」
    -   「ペアリング」
    -   "NDEF"
    -   "NFC"
    -   "Iso14443Dep"
    -   "Iso14443TypeA"
    -   "Iso14443TypeB"
    -   "Iso15693Vicinity"
    -   "MifareClassic"
    -   "MifareUltralight"
    -   "FeliCa"

## <a name="unpublish"></a>発行の取り消し


クライアントは、公開されたメッセージを不要になったが場合に、パブリケーションのハンドルを閉じます。 これは、メッセージを送信できなく必要があることを示します。 クライアント プロセスが終了した場合、システムは、クライアントに代わってすべての開いているファイル ハンドルを閉じます。

### <a name="required-actions"></a>必要な操作

-   ハンドルを閉じる際に (IRP\_MJ\_閉じる)、ドライバー。
    -   このパブリケーションの進行中の転送に関するバッファー以外のパブリケーション (データ型とメッセージの両方) で使用されるすべてのメモリを解放する必要があります。
    -   デバイスが、今後近接になった場合、メッセージを転送しませんする必要があります。
    -   パブリケーションの実行中の転送を中断する必要があります。
-   ドライバーは IRP を無視することが\_MJ\_クリーンアップします。

ドライバーでは、クライアントは、メッセージを 2 回発行で場合があるクライアントは、デバイスが近接の場合に、メッセージが 2 回送信される必要があるため、想定してください。

### <a name="required-actions"></a>必要な操作

ドライバーは、そのまま使用し、同じクライアントによって発行された場合でも、重複する公開されたメッセージを送信する必要があります。

### <a name="required-actions"></a>必要な操作


ドライバーする必要がありますすべてのメッセージの削除 (およびそれらのリソースを解放)、クライアントが、置換を送信していない場合は、「受信」キューから[ **IOCTL\_NFP\_取得\_次\_サブスクライブ済み\_メッセージ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfpdev/ni-nfpdev-ioctl_nfp_get_next_subscribed_message)以前 IOCTL 完了の 10 ~ 20 秒以内です。

## <a name="unresponsive-or-misbehaving-clients"></a>クライアントが応答していないか、不適切な動作


クライアントは、必要な送信が失敗した場合[ **IOCTL\_NFP\_取得\_次\_送信\_メッセージ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfpdev/ni-nfpdev-ioctl_nfp_get_next_transmitted_message) 10 個のピリオドの要求20 秒に\[10 ~ 20 秒\]ドライバーが、クライアントがなくなったことを想定してください。 通常の状況では、クライアントは、1 秒の範囲内での要求を更新する必要があります\[1 s\]します。 このような場合、ドライバーは"CompleteEventImmediately"カウンターを 0 に設定する必要があり、クライアントがウェイク アップし、必要な IRP を送信するまで、カウンターをインクリメントしない必要があります。

### <a name="required-actions"></a>必要な操作

ドライバーは、"CompleteEventImmediately"をカウンターを 0 に設定する必要があり、クライアントが、置換を送信していない場合は、カウンターをインクリメントする必要がありますいない[ **IOCTL\_NFP\_取得\_次\_送信済み\_メッセージ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfpdev/ni-nfpdev-ioctl_nfp_get_next_transmitted_message)以前 IOCTL 完了の 10 ~ 20 秒以内です。

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[フィールドの近接 DDI 参照の近く](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  

