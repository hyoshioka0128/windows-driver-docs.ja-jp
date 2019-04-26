---
title: WMI IRP を処理するための WmiSystemControl の呼び出し
description: WMI IRP を処理するための WmiSystemControl の呼び出し
ms.assetid: a2fa53e2-6468-4c3c-8b41-9a97305abc43
keywords:
- WMI の WDK カーネルでは、要求
- WDK の WMI の要求
- Irp WDK WMI
- WmiSystemControl
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e02df29ea68f5f8ad56cbd0153185e10c252dd19
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338606"
---
# <a name="calling-wmisystemcontrol-to-handle-wmi-irps"></a>WMI IRP を処理するための WmiSystemControl の呼び出し





WMI のライブラリ ルーチンがこのような各要求を処理する代わりに、ドライバーを呼び出すためにの WMI 要求の処理を簡略化[ **WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)します。 **WmiSystemControl**呼び出し、ドライバーは初期化された渡します[ **WMILIB\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff565813)ドライバーのを指すエントリを含む構造体[WMI ライブラリ コールバック ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff566357)(*DpWmiXxx*ルーチン) と、ドライバーのデータ ブロックおよびブロックのイベントに関する情報。

WMI ライブラリは動的なインスタンス名または静的インスタンス名の一覧を渡すためのメカニズムを提供しないために、ドライバーは、PDO または 1 つのベース名の文字列に基づく静的インスタンスの名前を唯一のデータ ブロックに関連した要求を処理するために WMI ライブラリを使用できます。 静的および動的なインスタンス名の詳細については、次を参照してください。 [WMI インスタンスの名前の定義](defining-wmi-instance-names.md)します。 WMI ライブラリを使用して、このようなブロックの要求を処理して、ブロックを他の要求の処理からドライバーにこだわるの[ *DispatchSystemControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。 詳細については、次を参照してください。 [DispatchSystemControl ルーチンで WMI Irp の処理](processing-wmi-irps-in-a-dispatchsystemcontrol-routine.md)します。

呼び出して WMI Irp を処理するために**WmiSystemControl**、ドライバーが必要な特定を実装する必要があります*DpWmiXxx*コールバック ルーチンでは、追加の実装と省略可能な*DpWmiXxx*コールバック ルーチン。

-   [*DpWmiQueryReginfo*](https://msdn.microsoft.com/library/windows/hardware/ff544097)—(Required) データおよびイベントに関する情報を提供は、ドライバーによって登録されているをブロックします。 WMI 呼び出し、ドライバーの*DpWmiQueryReginfo*プロセスに日常的な[ **IRP\_MN\_REGINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551731)または[ **IRP\_MN\_REGINFO\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff551734)要求。 詳細については、次を参照してください。[ブロックの登録に WMI ライブラリを使用して](using-the-wmi-library-to-register-blocks.md)します。

-   [*DpWmiQueryDataBlock*](https://msdn.microsoft.com/library/windows/hardware/ff544096)—(Required) が 1 つのインスタンスまたはデータ ブロックのすべてのインスタンスのいずれかを返します。 WMI 呼び出し、ドライバーの*DpWmiQueryDataBlock*プロセスに日常的な[ **IRP\_MN\_クエリ\_単一\_インスタンス**](https://msdn.microsoft.com/library/windows/hardware/ff551718)または[ **IRP\_MN\_クエリ\_すべて\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff551650)要求。

-   [*DpWmiSetDataBlock*](https://msdn.microsoft.com/library/windows/hardware/ff544104)—(Optional) データ ブロックの 1 つのインスタンス内のすべてのデータ項目を変更します。 WMI 呼び出し、ドライバーの*DpWmiSetDataBlock*プロセスに日常的な[ **IRP\_MN\_変更\_単一\_インスタンス**](https://msdn.microsoft.com/library/windows/hardware/ff550831)要求。

-   [*DpWmiSetDataItem*](https://msdn.microsoft.com/library/windows/hardware/ff544108)—(Optional) データ ブロックのインスタンス内の 1 つのデータ項目を変更します。 WMI 呼び出し、ドライバーの*DpWmiSetDataItem*プロセスに日常的な[ **IRP\_MN\_変更\_単一\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff550836)要求。

-   [*DpWmiFunctionControl*](https://msdn.microsoft.com/library/windows/hardware/ff544094)—(Optional) 有効にしを収集する高価なとして登録されているブロックのイベント通知とデータの収集を無効にします。 WMI 呼び出し、ドライバーの*DpWmiFunctionControl*プロセスに日常的な[ **IRP\_MN\_を有効にする\_コレクション**](https://msdn.microsoft.com/library/windows/hardware/ff550857)、 [**IRP\_MN\_を無効にする\_コレクション**](https://msdn.microsoft.com/library/windows/hardware/ff550848)、 [ **IRP\_MN\_を有効にする\_イベント**](https://msdn.microsoft.com/library/windows/hardware/ff550859)、または[ **IRP\_MN\_を無効にする\_イベント**](https://msdn.microsoft.com/library/windows/hardware/ff550851)要求。

-   [*DpWmiExecuteMethod*](https://msdn.microsoft.com/library/windows/hardware/ff544090)—(Optional) データ ブロックに関連付けられているメソッドを実行します。 WMI 呼び出し、ドライバーの*DpWmiExecuteMethod*プロセスに日常的な[ **IRP\_MN\_EXECUTE\_メソッド**](https://msdn.microsoft.com/library/windows/hardware/ff550868)要求。

ドライバーの*DpWmiXxx*ルーチンがドライバー ライターによって選択された任意の名前があることができます。

呼び出しの前に[ **WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)、ドライバーを初期化する必要があります、 [ **WMILIB\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff565813)エントリを含む構造体指すその*DpWmiXxx*ルーチンとそのデータ ブロックとブロックのイベントに関する情報。

ドライバーは、WMI 要求を受信するとします。

1. ドライバー呼び出し**WmiSystemControl**へのポインターの初期化に**WMILIB\_コンテキスト**構造、そのデバイス オブジェクトへのポインターおよび IRP へのポインター。

2. WMI IRP パラメーターを検証およびドライバーの呼び出し*DpWmiXxx*要求を処理するルーチン。 ドライバー エントリ ポイント設定されていない場合、 **WMILIB\_コンテキスト**、省略可能な*DpWmiXxx* 、日常的な WMI 完了 IRP が既定値と状態。

3. その*DpWmiXxx*ルーチン、ドライバー、要求を処理し、呼び出し元が指定のバッファーに出力を書き込みます。 たとえば、運転免許[ *DpWmiQueryDataBlock* ](https://msdn.microsoft.com/library/windows/hardware/ff544096)ルーチンは、要求されたインスタンスは指定されたブロックをバッファーに書き込むとします。

4. すべての*DpWmiXxx*以外ルーチン[ *DpWmiQueryReginfo*](https://msdn.microsoft.com/library/windows/hardware/ff544097)、ドライバー呼び出し[ **WmiCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff565798)要求、または返します状態を完了する\_PENDING と任意の IRP の完了を延期します。

5. WMI は、必要に応じて後処理を実行します。、、適切な出力をパッケージ化**れた WNODE\_* XXX*** 構造体、およびデータ コンシューマーに出力と状態を渡します。

 

 




