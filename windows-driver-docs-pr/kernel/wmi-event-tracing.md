---
title: WMI イベント トレース
description: WMI イベント トレース
ms.assetid: 72505a9a-830a-4529-ba73-31af0fedfeec
keywords:
- WMI の WDK カーネルでは、イベントの追跡
- WDK の WMI イベント
- WDK の WMI のトレース
- WMI の WDK カーネル、WDM ドライバー
- WDM ドライバー WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f936552dc2d07c3728b4f7aaa2dbdfa7f09a0d36
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386385"
---
# <a name="wmi-event-tracing"></a>WMI イベント トレース





このセクションでは、情報プロバイダーとしてそのカーネル モード ドライバー (Windows 2000 以降をサポート) WDM に WMI の拡張機能をについて説明しますを使用してコンシューマーの情報に情報を提供します。 ドライバーは、通常、コンシューマーを使用して、ドライバーの構成とリソース使用量を決定する情報を提供します。 WDM する「WMI 拡張機能のほか、ユーザー モード API では、プロバイダーまたは WMI イベント情報のコンシューマーがサポートしています-詳細については、Windows SDK を参照してください。

イベント トレースのロガーは、最大 32 個のインスタンスをサポートします。 カーネルをトレースするため、インスタンスの 1 つは予約されています。 ロガーは、大量のイベント率のトレースをサポートします。

トレース イベントは、その他の WMI イベントと同じ方法で定義されます。 MOF ファイルは、WMI イベントを説明します。 WMI イベントの説明の詳細については、次を参照してください。 [WMI データとイベント ブロックの MOF 構文](mof-syntax-for-wmi-data-and-event-blocks.md)します。

既存の WMI インフラストラクチャには、カーネル モード ドライバーが情報を記録するプロセスを統合します。 トレース イベントをログにドライバーは、次を行います。

1.  呼び出すことによって、WMI プロバイダとして登録[ **IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)します。

2.  WMIREG を設定してイベントをトレース可能としてマークを付ける\_フラグ\_追跡\_の GUID、**フラグ**のメンバー、 [ **WMIREGGUID** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-wmiregguidw)ドライバーは、wmi イベントを登録するときに渡される構造体。

3.  WMIREG を設定して、全体的な有効化/無効化のトレース イベントの一連のコントロールのイベントとして 1 つのイベントを指定\_フラグ\_トレース\_コントロール\_の GUID、**フラグ**のメンバー、**WMIREGGUID**ドライバーは、wmi イベントを登録するときに渡される構造体。

4.  GUID がトレース コントロールの GUID と一致するイベントを有効にする WMI からの要求を受信すると、ドライバーは、ロガーへのハンドルを格納する必要があります。 値は、イベントの書き込み時に必要になります。 このハンドルを使用する方法については、手順 6 を参照してください。 ロガーのハンドル値が含まれている、 **HistoricalContext**のメンバー、 [**れた WNODE\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-_wnode_header)パラメーターの一部である WMI バッファーの一部有効にするイベントの要求。

5.  トレース イベントが WMI イベントのコンシューマーに送信されますまたは WMI イベント ロガーをのみを対象としているかどうかを決定します。 場所を決定するこれは、メモリ、 [**イベント\_トレース\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff544329)構造体に由来する必要があります。 最終的に、このメモリに渡される[ **IoWMIWriteEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiwriteevent)します。

    イベントがログ イベントのみの場合、メモリは WMI では削除されません。 この場合、ドライバーは、バッファーにスタックに渡す必要がありますか、この目的のため、割り当てられたバッファーを再する必要があります。 パフォーマンス上の理由から、ドライバーが不要な割り当てやメモリを解放する呼び出しを最小限に抑える必要があります。 この勧告に準拠するためにエラーがログ ファイルに含まれるタイミング情報の整合性が低下します。

    イベントが、両方の logger にし、WMI イベントのコンシューマーに送信する場合、非ページ プールからメモリを割り当てる必要があります。 ここではイベント ロガーに送信され、するイベントの通知を要求した WMI イベントのコンシューマーに送信する WMI に転送されます。 動作に従って WMI によってイベントのメモリが解放し、 **IoWMIWriteEvent**します。

6.  後のメモリ、 [**イベント\_トレース\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff544329)ドライバー イベント データ、存在する場合、含まれているとは、次の情報を設定する必要があります。

    設定、**サイズ**sizeof するメンバー (**イベント\_トレース\_ヘッダー**) の最後に追加される追加のドライバー イベント データのサイズと**イベント\_トレース\_ヘッダー**します。

    設定、**フラグ**れた WNODE メンバー\_フラグ\_追跡\_イベントをログに送信する GUID。 イベントが WMI イベントのコンシューマーもに送信する場合、設定、れた WNODE\_フラグ\_ログ\_れた WNODE します。 注意してください、れた WNODE を設定する必要はありません\_フラグ\_追跡\_れた WNODE を設定する場合は、GUID\_フラグ\_ログ\_れた WNODE します。 どちらも設定されている場合、れた WNODE\_フラグ\_追跡\_GUID が優先され、イベントは、WMI イベントのコンシューマーには送信されません。

    設定、 **Guid**または**GuidPtr**メンバー。 使用して場合**GuidPtr**、れた WNODE 設定\_フラグ\_使用\_GUID\_で PTR、**フラグ**メンバー。

    必要に応じての値を指定**タイムスタンプ**します。 ドライバーが指定されていない場合、**タイムスタンプ**値、ロガーはこれを入力します。 ドライバーは、タイムスタンプを設定するロガーをしないかどうかは、れた WNODE を設定する必要がある\_フラグ\_使用\_のタイムスタンプ、**フラグ**メンバー。

    次のいずれかの設定**イベント\_トレース\_ヘッダー**ドライバーに意味を持つメンバー。**Class.Type**、 **Class.Level**、および**Class.Version**します。

    最後にキャスト、**イベント\_トレース\_ヘッダー**を**れた WNODE\_ヘッダー**設定と、 **HistoricalContext** の値**れた Wnode**で保存されているロガーのハンドルを手順 4 上。

7.  呼び出す[ **IoWMIWriteEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiwriteevent)へのポインターが、**イベント\_トレース\_ヘッダー**構造体。

ドライバーはドライバーを使用したイベント ログを無効にする通知を受信するまでは、コントロールの GUID に関連付けられているトレース イベントのログ記録を続行する必要があります、 **IRP\_MN\_を無効にする\_イベント**要求。

 

 




