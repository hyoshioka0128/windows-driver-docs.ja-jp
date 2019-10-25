---
title: WMI イベント トレース
description: WMI イベント トレース
ms.assetid: 72505a9a-830a-4529-ba73-31af0fedfeec
keywords:
- WMI WDK カーネル、イベント追跡
- イベント WDK WMI
- WDK WMI のトレース
- WMI WDK カーネル、WDM ドライバー
- WDM ドライバー WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c256fea79a7ac7ee28d7771654a72714edd065aa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835686"
---
# <a name="wmi-event-tracing"></a>WMI イベント トレース





このセクションでは、情報プロバイダーが情報提供者に情報を提供するために使用できる、WDM (Windows 2000 以降でサポートされています) の WMI 拡張機能について説明します。 ドライバーは、通常、ドライバーの構成とリソースの使用状況を判断するためにコンシューマーが使用する情報を提供します。 WDM の WMI 拡張機能に加え、ユーザーモード API は WMI イベント情報のプロバイダーまたはコンシューマーをサポートしています。詳細については、Windows SDK を参照してください。

イベントトレース logger では、最大32のインスタンスがサポートされます。 インスタンスの1つは、カーネルのトレース用に予約されています。 Logger は、高いイベント率のトレースをサポートしています。

トレースイベントは、他の WMI イベントと同じ方法で定義されます。 WMI イベントについては、MOF ファイルを参照してください。 WMI イベントの説明の詳細については、「 [Wmi データおよびイベントブロックの MOF 構文](mof-syntax-for-wmi-data-and-event-blocks.md)」を参照してください。

カーネルモードドライバーのログ情報を既存の WMI インフラストラクチャに統合するプロセス。 トレースイベントをログに記録するために、ドライバーは次のことを行います。

1.  [**Iowmiregistrationcontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)を呼び出して、WMI プロバイダーとして登録します。

2.  イベント[**は、ドライバー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmiregguidw)によって WMI に登録されたときに渡される、\_\_\_フラグを設定する**ことにより**、イベントをトレース可能としてマークします。

3.  トレースイベントのセットを全体的に有効または無効にするには、コントロールイベントとして1つのイベントを指定します。これを行うには、 **[\_** \_\_\_フラグ **] を設定**します。ドライバーは、イベントを WMI に登録します。

4.  WMI から要求を受信して、GUID がトレースコントロールの GUID と一致するイベントを有効にする場合、ドライバーはロガーへのハンドルを格納する必要があります。 この値は、イベントを書き込むときに必要になります。 このハンドルの使用方法の詳細については、手順 6. を参照してください。 Logger ハンドル値は、enable events 要求のパラメーターの一部である WMI バッファーの[**Wnode\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-_wnode_header)部分の**HistoricalContext**メンバーに含まれています。

5.  トレースイベントが WMI イベントコンシューマーに送信されるか、WMI イベントロガーのみを対象とするかを決定します。 これにより、[**イベント\_トレース\_ヘッダー**](https://msdn.microsoft.com/library/windows/hardware/ff544329)の構造の基になるメモリの場所が決まります。 このメモリは、最終的に[**IoWMIWriteEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiwriteevent)に渡されます。

    イベントがログイベントのみの場合、メモリは WMI によって削除されません。 この場合、ドライバーはスタック上のバッファーを渡すか、またはこの目的のために割り当てられたバッファーを再利用する必要があります。 パフォーマンス上の理由から、ドライバーは不要な呼び出しを最小限に抑えてメモリの割り当てまたは解放を行う必要があります。 この推奨事項に準拠していないと、ログファイルに含まれるタイミング情報の整合性が損なわれます。

    イベントが logger と WMI イベントコンシューマーの両方に送信される場合は、非ページプールからメモリを割り当てる必要があります。 この場合、イベントは logger に送信され、WMI に転送されて、イベントの通知を要求した WMI イベントコンシューマーに送信されます。 その後、 **IoWMIWriteEvent**の動作に応じて、WMI によってイベントのメモリが解放されます。

6.  [**イベント\_トレース\_ヘッダー**](https://msdn.microsoft.com/library/windows/hardware/ff544329)のメモリと、ドライバーイベントデータ (存在する場合) がセキュリティで保護されている場合は、次の情報を設定する必要があります。

    **Size**メンバーを Sizeof (**event\_trace\_header**) に設定し、**イベント\_トレース\_ヘッダー**の最後に追加される追加のドライバーイベントデータのサイズを加算します。

    **Flags**メンバーを wnode\_フラグ\_トレース\_GUID に設定して、イベントが logger に送信されるようにします。 イベントが WMI イベントコンシューマーにも送信される場合は、WNODE\_フラグ\_LOG\_WNODE に設定します。 Wnode\_フラグ\_ログ\_WNODE を設定した場合、WNODE\_フラグ\_トレース\_GUID に設定する必要はありません。 両方が設定されている場合は、WNODE\_フラグ\_トレースされ\_GUID が優先され、イベントは WMI イベントコンシューマーに送信されません。

    **Guid**または**guidptr**メンバーを設定します。 **Guidptr**を使用する場合は、 **Flags**メンバーで\_GUID\_PTR を使用\_、wnode\_フラグを設定します。

    必要に応じて、 **TimeStamp**の値を指定します。 ドライバーで**タイムスタンプ**値が指定されていない場合、logger はこれをに入力します。 ドライバーがタイムスタンプを設定しないようにするには、 **Flags**メンバーで\_タイムスタンプ\_使用するように wnode\_フラグを設定する必要があります。

    次のいずれかの**イベント\_トレース\_ヘッダー**メンバーを設定します。これは、ドライバーに意味があります:**クラス、型**、**クラスレベル**、および**バージョン**。

    最後に、**イベント\_トレース\_ヘッダー**を**wnode\_ヘッダー**にキャストし、 **wnode**の**HistoricalContext**値を、上記の手順4で保存した logger ハンドルに設定します。

7.  **イベント\_トレース\_ヘッダー**構造体へのポインターを使用して、 [**IoWMIWriteEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiwriteevent)を呼び出します。

ドライバーは、コントロール GUID に関連付けられているトレースイベントのログ記録を続行し、IRP\_によってイベントログを無効にし、 **\_イベント要求\_無効**にするようにします。

 

 




