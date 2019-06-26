---
title: 操作領域ハンドラーを登録/登録解除する
description: 操作領域ハンドラーを登録/登録解除する
ms.assetid: de40488d-7935-431c-b1f4-87f8aff1125b
keywords:
- ACPI デバイス WDK、領域の操作
- 操作のリージョン WDK ACPI
- 機能ドライバー WDK ACPI、領域の操作
- WDM 関数ドライバー WDK ACPI、領域の操作
- 操作のリージョンのハンドラーを登録します。
- 操作のリージョンのハンドラーの登録を解除
ms.date: 01/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: 108e05dc40b77557de56d72d9f390f78a2b7ba26
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355815"
---
# <a name="registering-and-deregistering-an-operation-region-handler"></a>操作領域ハンドラーを登録/登録解除する


ACPI 関数ドライバーは、呼び出すことによって操作リージョン ハンドラーを登録[ **RegisterOpRegionHandler** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/oprghdlr/nf-oprghdlr-registeropregionhandler)し、次の情報を提供します。

-   物理デバイス オブジェクト (PDO) 操作の領域を定義する ACPI デバイスを表します。

-   アクセス権の種類*生*または*調理します。*

    詳細については、次を参照してください[、操作の領域へのアクセス。](accessing-an-operation-region.md)

-   領域の種類。

    仕入先には、0 xff まで 0x80 からベンダ定義値を指定する必要があります。 (よりも小さい値 0x80 は ACPI 仕様によって定義され、内部使用のために予約されています。)

-   ドライバーの操作のリージョンのハンドラーへのポインター。

    ACPI ドライバーでは、ドライバーの操作のリージョンのハンドラーを呼び出すことによって、操作のリージョンにアクセスします。

-   ポインター、*操作リージョン コンテキスト*します。

    操作のリージョン コンテキストでは、デバイスに固有しは、関数のドライバーでのみ使用します。 ACPI ドライバー操作のリージョンのハンドラーを呼び出すと、ハンドラーに戻す操作の地域のコンテキストを渡します。 通常、機能のデバイス オブジェクト (FDO) のデバイスの拡張機能です。

**RegisterOpRegionHandler**機能ドライバーを使用して、ドライバー、ハンドラーの登録を解除するときにのみ、操作のリージョンのハンドラーを一意に識別する操作領域オブジェクトを返します。

通常、ドライバー ハンドラーを登録操作リージョン、ドライバーのプラグ アンド プレイ ディスパッチ ルーチンで FDO への応答の開始後に、 [ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)要求。 ドライバーは、ハンドラーの操作の地域のコンテキストを割り当てた後、ハンドラーを登録する必要があります。 ドライバーは、デバイスのベンダ定義のインターフェイスを作成する場合、ドライバーはハンドラーを登録した後にデバイス インターフェイスを有効する必要があります。

ACPI 関数ドライバーを呼び出して、操作のリージョンのハンドラーの登録を解除[ **DeRegisterOpRegionHandler** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/oprghdlr/nf-oprghdlr-deregisteropregionhandler)し、次の情報を提供します。

-   この PDO ACPI デバイス操作の領域を定義を表します。

-   ACPI のドライバーがドライバーには、操作のリージョンのハンドラーが登録されているときに返される操作領域オブジェクト。 このオブジェクトは、操作のリージョンのハンドラーを一意に識別します。

通常、ドライバー登録を解除します、ドライバーのプラグ アンド プレイ ディスパッチ ルーチンでリージョン操作ハンドラー FDO への応答を停止する前に、 [ **IRP\_MN\_停止\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)要求。 ハンドラーの操作の地域のコンテキストを解放する前に、ドライバーは、ハンドラーを登録解除する必要があります。 ドライバーは、デバイスのベンダ定義のインターフェイスを作成する場合、ドライバーは、ハンドラーの登録を解除する前にデバイス インターフェイスを無効する必要があります。

 




