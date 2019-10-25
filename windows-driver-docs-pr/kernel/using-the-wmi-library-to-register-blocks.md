---
title: WMI ライブラリを使用したブロックの登録
description: WMI ライブラリを使用したブロックの登録
ms.assetid: 1f4b773d-ca24-47f5-87e8-84c98dad9267
keywords:
- WMI WDK カーネル、WMI への登録
- WMI データプロバイダーの登録
- データプロバイダー WDK WMI
- ドライバー登録 WDK WMI
- イベントブロック WDK WMI
- WDK WMI をブロックする
- IRP_MN_REGINFO
- IRP_MN_REGINFO_EX
- 登録 (ブロックを)
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd678e28751d6a5fa914ec02055f9ee95b1c3192
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838328"
---
# <a name="using-the-wmi-library-to-register-blocks"></a>WMI ライブラリを使用したブロックの登録





ドライバーは、WMI ライブラリを使用して、動的なインスタンス名を使用していないブロックを登録する場合、またはに基づいて静的インスタンス名を使用する場合に、reginfo および[**irp\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex) [ **\_REGINFO**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)\_EX によって\_処理されるようにすることができます。PDO またはドライバーで定義された基本名文字列。 この場合、ドライバーは次のようになります。

1.  ドライバーのデバイスオブジェクトへのポインター、 [**Wmb\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)構造体へのポインター、および IRP へのポインターを使用して、 [**wmi コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)を呼び出します。

    **Wm/b\_のコンテキスト**構造は、登録するブロックの数 (**guidcount**) を示し、GUID、インスタンスの数、および登録を指定する[**Wmiguidreginfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmiguidreginfo)構造 (**guidcount**) のリストを指します。対応するブロックに関連するフラグ。 また、ドライバーの必須および*省略可能な*、コールバックルーチンのエントリポイントも定義します。

2.  WMI がドライバーのドライブ名[*の指定ルーチンを*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_reginfo_callback)呼び出すと、ドライバーのレジストリパス、その MOF リソース名、すべてのブロックに関連する登録フラグ、および wmi がドライバーのデータのインスタンスに名前を指定するために使用する情報を指定します。ブロック。ドライバーの[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンに渡された物理デバイスオブジェクトへのポインター、または静的インスタンス名のベースとなる文字列。

ドライバーは、設定されているデータポイントを初期化する必要があります。**この呼び出しは、設定**されています。*このコールバック*ルーチンは、\_の**コンテキスト**構造にある、設定さ**れてい**ます。WMI がドライバーの \n 呼び出し*Queryreginfo*ルーチンを呼び出すまでは、 **WMの\_コンテキスト**構造になります。

 

 




