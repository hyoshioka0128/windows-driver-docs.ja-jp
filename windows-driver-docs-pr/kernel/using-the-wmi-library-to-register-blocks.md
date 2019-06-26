---
title: ブロックを登録するための WMI ライブラリの使用
description: ブロックを登録するための WMI ライブラリの使用
ms.assetid: 1f4b773d-ca24-47f5-87e8-84c98dad9267
keywords:
- WMI の WDK カーネルでは、WMI に登録します。
- WMI データ プロバイダーを登録します。
- WDK の WMI のデータ プロバイダー
- ドライバー WDK WMI の登録
- イベントは、WDK の WMI をブロックします。
- WDK の WMI をブロックします。
- IRP_MN_REGINFO
- IRP_MN_REGINFO_EX
- ブロックを登録します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71293d493677b459c48d7e7027301e0b66d2af43
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358174"
---
# <a name="using-the-wmi-library-to-register-blocks"></a>ブロックを登録するための WMI ライブラリの使用





ドライバーは、WMI ライブラリを使用して処理するために[ **IRP\_MN\_REGINFO** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)と[ **IRP\_MN\_REGINFO\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex)要求のかどうか、動的なインスタンスの名前を使用しないまたは PDO またはドライバーの定義の基本名の文字列に基づいて静的インスタンス名を使用するブロックが登録されています。 この場合は、ドライバー。

1.  呼び出し[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)ドライバーのデバイス オブジェクトへのポインターにポインターを使用して、 [ **WMILIB\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/ns-wmilib-_wmilib_context)構造、および IRP へのポインター

    **WMILIB\_コンテキスト**構造体を登録するブロックの数を示します (**GuidCount**) およびポイントの一覧に[ **WMIGUIDREGINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/ns-wmilib-_wmiguidreginfo)構造 (**GuidList**) インスタンス、および対応するブロックに関連する登録フラグの数、GUID を指定します。 ドライバーの必須のエントリ ポイントも定義と省略可能な*DpWmiXxx*コールバック ルーチン。

2.  WMI がドライバーを呼び出すときに[ *DpWmiQueryReginfo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_query_reginfo_callback) 、日常的なドライバーを指定します、ドライバーのレジストリ パス、その MOF リソース名、登録フラグに関連するすべてのブロック、および情報WMI では、ドライバーのデータ ブロックは、次のいずれかの名前のインスタンスに物理デバイス オブジェクトへのポインター、ドライバーに渡される[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)ルーチンまたは基になる文字列静的なインスタンス名です。

ドライバーのエントリ ポイントを初期化する必要があります、 *DpWmiXxx*コールバック ルーチン、 **WMILIB\_コンテキスト**呼び出す前に構造**WmiSystemControl**、初期化を延期することができますが、 **GuidCount**と**GuidList**で、 **WMILIB\_コンテキスト**WMI、ドライバーのを呼び出すまで構造体*DpWmiQueryReginfo*ルーチン。

 

 




