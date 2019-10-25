---
title: WMI 登録フラグ
description: WMI 登録フラグ
ms.assetid: 001d4840-0ed4-464d-8379-7bbd0afce28c
keywords:
- 動的インスタンス名 WDK WMI
- 静的インスタンス名 WDK WMI
- 登録フラグ WDK WMI
- WDK WMI にフラグをする
- WMI WDK カーネル、WMI への登録
- WMI データプロバイダーの登録
- データプロバイダー WDK WMI
- ドライバー登録 WDK WMI
- イベントブロック WDK WMI
- WDK WMI をブロックする
- 登録 (ブロックを)
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e8fe309f38ab40c68a2b98f573e9feb59b0e284
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835653"
---
# <a name="wmi-registration-flags"></a>WMI 登録フラグ





ドライバーは、ブロックが静的[**または動的**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmiregguidw)なインスタンス名を使用しているかどうかを示します。また、ブロックを登録するために WMI に渡す[**Wmiguidreginfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmiguidreginfo)構造体またはのように、このブロックの他の特性を指定します。

ドライバーは、次のいずれかのフラグを設定することによって、ブロックが静的インスタンス名を使用することを示します。

-   WMI REG\_フラグ\_インスタンス\_リストは、ドライバーが静的リスト内のすべてのインスタンス名を提供することを示します。

    ドライバーがこのフラグを設定できるのは、このフラグを設定できるのは、 [**Wmi コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)を呼び出さずに、irp\_によって[ **\_Reginfo**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)または[**IRP\_\_、reginfo\_EX**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex)要求を処理することによってブロックが登録されている場合のみです。 ドライバーは、**ブロックの** **InstanceNameList**によって示されるバイトオフセットにインスタンス名文字列を書き込みます。

-   WMI REG\_フラグ\_インスタンス\_のベース名文字列から静的インスタンス名を生成するように WMI に指示します。

    Irp\_によって処理されるドライバーが **\_reginfo**または irp\_によって処理される **\_REGINFO\_EX**要求によって、**ブロックの** **BaseNameOffset**によって示されるオフセットにベース名文字列が書き込まれます。データ.

    **[Wmi システムコントロール]** を呼び出すドライバーは[ **、その**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_reginfo_callback)*インスタンスのインスタンス*名を指定します。

-   WMI REG\_フラグ\_インスタンス\_PDO は、ドライバーの PDO のデバイスインスタンス ID から静的インスタンス名を生成するように WMI に指示します。

    Irp\_によって処理されるドライバーが **\_reginfo**または irp\_\_によって処理される場合は、 **REGINFO\_EX**要求によって、ブロックの**Wmi reginfo**構造の**pdo**メンバーに pdo へのポインターが書き込まれます。 要求が**IRP\_\_REGINFO\_EX**である場合、ドライバーは、 [**obreferenceobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject)ルーチンを呼び出すことによって渡された各 PDO の参照カウントを増やす必要があります。 (システムは、後で各 PDO を逆参照します)。

    呼び出し[*元の*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_reginfo_callback)ドライバーは、その**システムコントロール**の*pdo*パラメーターにある pdo へのポインターを書き込みます。

ブロックで動的インスタンス名が使用されていることを示すには、ドライバーは、次のフラグを設定しないようにする必要があります。\_フラグ\_インスタンス\_リスト、の場合は、WMI REG\_フラグ\_インスタンス\_PDO,、または WMI REG\_フラグ\_インスタンス\_ベースです。

ドライバーは、データブロックが収集にかかるコストが高いことを示しています。これを行うには、\_フラグ\_コストを設定します。 これにより、wmi クライアントが最初にデータブロックを開いたときに[ **\_コレクション要求を有効に**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-collection)し、最後の wmi クライアントが終了したときに[**irp\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-disable-collection)\_\_収集要求を無効にするように、wmi に\_対して実行するように wmi に指示します。ブロック。 このようなブロックのデータを収集する必要があるのは、 **\_COLLECTION 要求を有効にする\_IRP\_** を受信するまでの間です。

ドライバーは、イベントブロックを示しています。これは、\_イベント\_\_フラグを設定することによって\_GUID のみになります。 これは、ブロックをイベントとして有効または無効にすることができ、クエリや設定を行うことができないことを示します。

ドライバーは、WMI に対して、以前に登録されたブロックを削除するように指示します。\_GUID\_削除するには、\_フラグを設定します。 このフラグは、登録情報を更新するための要求に応答する場合にのみ有効です ([ **\_reginfo**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)または irp\_によって、レジストリ情報[ **\_EX\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex)の更新を含む)。 詳細については、「 [WMI の登録情報を更新](updating-wmi-registration-information.md)する」を参照してください。

 

 




