---
title: WMI IRP を処理するための WmiSystemControl の呼び出し
description: WMI IRP を処理するための WmiSystemControl の呼び出し
ms.assetid: a2fa53e2-6468-4c3c-8b41-9a97305abc43
keywords:
- WMI WDK カーネル、要求
- WDK WMI を要求する
- Irp WDK WMI
- Wmi コントロール
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a67216bde594957962bea380bbe2863ff35f727a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828572"
---
# <a name="calling-wmisystemcontrol-to-handle-wmi-irps"></a>WMI IRP を処理するための WmiSystemControl の呼び出し





WMI ライブラリルーチンは、このような要求を処理するのではなく、WMI の要求の処理を簡略化[**します。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) Wmi**コントロール**の呼び出しで、ドライバーは、初期化された[**WMB\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)構造を渡します。この構造体には、ドライバーの[WMI ライブラリコールバックルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index) *("* データポイント" ルーチン) へのエントリポイントと、ドライバーのデータブロックとイベントブロック。

WMI ライブラリには、動的インスタンス名または静的インスタンス名の一覧を渡すメカニズムが用意されていないため、ドライバーは、PDO または1つのベース名文字列に基づく静的インスタンス名を持つデータブロックのみを含む要求を処理するために、WMI ライブラリを使用できます。 静的および動的なインスタンス名の詳細については、「 [WMI インスタンス名の定義](defining-wmi-instance-names.md)」を参照してください。 ドライバーが WMI ライブラリを使用してそのようなブロックの要求を処理したり、 [*DispatchSystemControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチン内の他のブロックの要求を処理したりするのを防ぐことはできません。 詳細については、「 [DispatchSystemControl ルーチンでの WMI irp の処理](processing-wmi-irps-in-a-dispatchsystemcontrol-routine.md)」を参照してください。

WMI Irp を処理するには、次のような特定の必須の**システム***コールバック*ルーチンを実装*する必要が*あります。

-   [ *(必須*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_reginfo_callback)) ドライバーによって登録されているデータおよびイベントブロックに関する情報を提供します。 WMI は*ドライバーの要求*を処理するために、ドライバーのすべての[ **\_Reginfo**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)または[**irp\_\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex)を処理するために、ドライバーの\_を呼び出します。 詳細については、「 [WMI ライブラリを使用したブロックの登録](using-the-wmi-library-to-register-blocks.md)」を参照してください。

-   [](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)/(必須) は、1つのインスタンスまたはデータブロックのすべてのインスタンスを返します。 WMI は、*ドライバーの*すべての\_データ要求\_クエリ\_、 [**1 つの\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance)または[**IRP\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-all-data)の\_クエリを処理するために、ドライバーの\_を呼び出します。\_

-   データブロックの1つのインスタンスのすべてのデータ項目を変更し[*ます (省略*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_set_datablock_callback)可能)。 WMI は、 [**1 つの\_インスタンス要求\_\_変更**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-instance)された IRP\_を処理するために、*ドライバーの設定*を呼び出します。

-   [インスタンス[ *]: (* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_set_dataitem_callback)省略可能) データブロックのインスタンス内の1つのデータ項目を変更します。 WMI は、ドライバーの設定された、 [**1 つの\_項目の要求\_\_変更**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-item)された IRP\_処理*するルーチンを*呼び出します。

-   [](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_function_control_callback)/(オプション) 収集にかかるコストとして登録されたブロックのイベント通知とデータ収集を有効または無効にします。 WMI は、Irp\_を処理するために、ドライバーの実行可能な*コントロール*ルーチンを呼び出します。これに[**より、\_COLLECTION**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-collection)、 [**irp\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-disable-collection)\_\_コレクションの無効化\_irp\_\_有効にすることができ[ **\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-events)、または[**IRP\_、\_イベントの要求を無効\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-disable-events) 。

-   [ *(オプション*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_execute_method_callback)) データブロックに関連付けられたメソッドを実行します。 WMI は、*ドライバーの*実行されたプロセスを呼び出して、 [ **\_メソッド要求を実行\_IRP\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-execute-method)を処理します。

ドライバーの設定では、ドライバーライターによって*任意の名前*を選択できます。

[**Wmi コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)を呼び出す前に、ドライバーは *、そのデータ*ブロックとイベントブロックに関する情報を含むエントリポイントを使用して、 [**wmb\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)構造体を初期化する必要があります。

ドライバーが WMI 要求を受け取ると、次のようになります。

1. ドライバーは、初期化された**Wmb\_コンテキスト**構造体へのポインター、デバイスオブジェクトへのポインター、および IRP へのポインターを使用して、 **wmi コントロール**を呼び出します。

2. WMI は、IRP パラメーターを検証し、要求を処理するドライバーの要求*元ルーチンを*呼び出します。 ドライバーが *、オプションの*設定可能なのに **\_コンテキスト**のエントリポイントを設定していない場合、WMI は既定値と状態を使用して IRP を完了します。

3. このルーチン*で*は、ドライバーが要求を処理し、呼び出し元が指定したバッファーに出力を書き込みます。 たとえば、[*ドライバーのインスタンス*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)は、指定されたブロックの要求されたインスタンスをバッファーに書き込みます。

4. WmiCompleteRequest を除くすべての実行されて*いるルーチンで*は、ドライバー[*は、要求*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_reginfo_callback)を完了するために[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmicompleterequest)を呼び出します。または、IRP の場合と同様に、完了を延期するステータス\_を返します。

5. WMI は必要な後処理を実行し、適切な**Wnode\_* XXX*** 構造の出力をパッケージ化して、出力と状態をデータコンシューマーに渡します。

 

 




