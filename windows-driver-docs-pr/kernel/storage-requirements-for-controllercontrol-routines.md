---
title: ControllerControl ルーチンの記憶域の要件
description: ControllerControl ルーチンの記憶域の要件
ms.assetid: 1ee69144-5f52-4d61-ad30-02e8fbe1f91e
keywords:
- コントローラーオブジェクト WDK カーネル、コントローラー制御ルーチンの記述
- コントローラー制御ルーチン、書き込み
- コントローラーコントロールルーチン、ストレージ
- storage WDK コントローラーオブジェクト
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7eb446fb89b492040f49a6660d92ff274e6a824d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838403"
---
# <a name="storage-requirements-for-controllercontrol-routines"></a>ControllerControl ルーチンの記憶域の要件





*コントローラーに制御*ルーチンがある場合、WDM 以外のドライバーは、 [**IoCreateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatecontroller)によって返される*コントローラーオブジェクト*ポインターの常駐ストレージを提供する必要があります。

ドライバーは、デバイス拡張機能またはドライバーによって割り当てられた非ページプールで、必要な記憶域を提供できます。 通常、コントローラーオブジェクトを使用するドライバーは、コントローラーオブジェクトによって表されるハードウェアによって制御される物理デバイスまたは論理デバイスを表すデバイスの拡張機能*に、コントローラー*オブジェクトを格納します。

ドライバーライターは、*コントローラー*-&gt;**コントローラー拡張機能**のサイズと内部構造を決定します。

名前を指定できないコントローラーオブジェクトは、i/o 要求のターゲットにすることはできません。 このようなハードウェアは通常、i/o 要求の実際のターゲットである同種のデバイスのセットを制御します。

 

 




