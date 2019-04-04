---
title: WinDbg で例外とイベントの構成
description: 特定の方法で指定された例外とイベントに対応するための WinDbg を構成することができます。 例外ごとに、中断状態と処理の状態を設定できます。
ms.assetid: B91DD7B6-5206-4BA6-8B49-8ECCA2FA730B
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10c50d9012bda84a5a02afacfccb8b6c2cfda45b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532246"
---
# <a name="configuring-exceptions-and-events-in-windbg"></a>WinDbg で例外とイベントの構成


特定の方法で指定された例外とイベントに対応するための WinDbg を構成することができます。 例外ごとに、中断状態と処理の状態を設定できます。 各イベントに対して、中断状態を設定できます。

中断状態を構成するには、次のいずれかの方法します。

-   選択**イベント フィルター**から、**デバッグ** メニューの イベントの一覧から使用する をクリックして、**イベント フィルター**クリックしてダイアログ ボックスで、**有効**、**無効**、**出力**、または**無視**します。

-   使用して、 [ **SXE**](sx--sxd--sxe--sxi--sxn--sxr--sx---set-exceptions-.md)、 **SXD**、 **SXN**、または**SXI**コマンド。

処理のステータスを構成するには、次のいずれかの方法します。

-   選択**イベント フィルター**から、**デバッグ** メニューの イベントの一覧から使用する をクリックして、**イベント フィルター**クリックしてダイアログ ボックスで、**処理済み**または**処理されない**します。

-   使用して、 [ **SXE**](sx--sxd--sxe--sxi--sxn--sxr--sx---set-exceptions-.md)、 **SXD**、 **SXN**、または**SXI**コマンド。

例外とイベントの詳細については、[を制御する例外とイベント](controlling-exceptions-and-events.md)を参照してください。

 

 





