---
title: WMI 登録フラグ
description: WMI 登録フラグ
ms.assetid: 001d4840-0ed4-464d-8379-7bbd0afce28c
keywords:
- WDK の WMI の名前の動的インスタンス
- 静的なインスタンス名を WDK WMI
- 登録は、WDK の WMI をフラグします。
- WDK の WMI のフラグ
- WMI の WDK カーネルでは、WMI に登録します。
- WMI データ プロバイダーを登録します。
- WDK の WMI のデータ プロバイダー
- ドライバー WDK WMI の登録
- イベントは、WDK の WMI をブロックします。
- WDK の WMI をブロックします。
- ブロックを登録します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: eecddaf1a6e8afa134bea883f84581c3c54ebee4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369900"
---
# <a name="wmi-registration-flags"></a>WMI 登録フラグ





ドライバーは、ブロックは、静的なを使用するかどうかまたは動的なインスタンス名しフラグを設定して、ブロックの他の特性を指定することを示します、 [ **WMIGUIDREGINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/ns-wmilib-_wmiguidreginfo)または[ **WMIREGGUID** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-wmiregguidw)ブロックを登録する WMI に合格する構造体。

ドライバーでは、次のフラグのいずれかを設定して、ブロックが静的インスタンス名を使用することを示します。

-   WMIREG\_フラグ\_インスタンス\_一覧は、ドライバーがすべてのインスタンスの静的リスト内の名前を提供することを示します。

    処理によってブロック登録されている場合にのみ、ドライバーはこのフラグを設定できる、 [ **IRP\_MN\_REGINFO** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)または[ **IRP\_MN\_REGINFO\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex)呼び出しではなく、要求[ **WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)します。 ドライバー書き込みます、インスタンス名の文字列で示されるバイト オフセット位置に**InstanceNameList**ブロックの**WMIREGGUID**構造体。

-   WMIREG\_フラグ\_インスタンス\_BASENAME ドライバー定義した基本名文字列から静的なインスタンス名を生成する WMI に指示します。

    処理するドライバー、 **IRP\_MN\_REGINFO**または**IRP\_MN\_REGINFO\_EX**要求がある基本名文字列を書き込みます、示されたオフセット**BaseNameOffset**ブロックの**WMIREGGUID**構造体。

    呼び出すドライバー **WmiSystemControl**の基本名文字列を指定します、 *InstanceName*のパラメーターの[ **DpWmiQueryReginfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_query_reginfo_callback)ルーチン。

-   WMIREG\_フラグ\_インスタンス\_PDO ドライバーの PDO のデバイス インスタンス ID からの静的インスタンス名を生成する WMI に指示します。

    処理するドライバー、 **IRP\_MN\_REGINFO**または**IRP\_MN\_REGINFO\_EX**要求は、でPDOにポインターを書き込みます**Pdo**のブロックのメンバー **WMIREGGUID**構造体。 要求が場合**IRP\_MN\_REGINFO\_EX**、ドライバーは、呼び出すことによって渡される各 PDO の参照カウントを増やす必要があります、 [ **ObReferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obfreferenceobject)ルーチン。 (システムが逆参照各 PDO 後。)

    呼び出すドライバー **WmiSystemControl**で PDO にポインターを書き込みます、 *Pdo*のパラメーターの[ *DpWmiQueryReginfo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_query_reginfo_callback)ルーチン。

ブロックでの動的インスタンス名を使用することを示す、ドライバーする必要がありますを設定できませんの次のフラグ。WMIREG\_フラグ\_インスタンス\_リスト、WMIREG\_フラグ\_インスタンス\_PDO、または WMIREG\_フラグ\_インスタンス\_BASENAME します。

ドライバーは、データ ブロックが WMIREG を設定して、収集する高価であることを示します\_フラグ\_高コストです。 これに指示を送信する WMI、 [ **IRP\_MN\_を有効にする\_コレクション**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-collection)初めて WMI クライアントが開くデータ ブロックの要求と[ **IRP\_MN\_を無効にする\_コレクション**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-disable-collection)最後の WMI クライアントが、ブロックを閉じるときに要求します。 受信するまで、ドライバーは、このようなブロックのデータを収集しない必要があります、 **IRP\_MN\_を有効にする\_コレクション**要求。

ドライバーが WMIREG を設定して、イベント ブロックを示す\_フラグ\_イベント\_のみ\_GUID。 これは、ブロックができることを示します。 有効になっているまたはのみ、イベントとして無効になっているとできません照会または設定します。

ドライバーに指示 WMIREG を設定して、以前に登録されたブロックを削除する WMI\_フラグ\_削除\_GUID。 このフラグは、登録情報を更新する要求に対する応答でのみ有効です ([**IRP\_MN\_REGINFO** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)または[ **IRP\_MN\_REGINFO\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex) WMIUPDATE で)。 詳細については、次を参照してください。 [WMI 登録情報を更新する](updating-wmi-registration-information.md)します。

 

 




