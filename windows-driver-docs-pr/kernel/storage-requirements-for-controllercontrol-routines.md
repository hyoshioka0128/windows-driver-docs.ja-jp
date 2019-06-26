---
title: ControllerControl ルーチンの記憶域の要件
description: ControllerControl ルーチンの記憶域の要件
ms.assetid: 1ee69144-5f52-4d61-ad30-02e8fbe1f91e
keywords:
- コント ローラー オブジェクトの WDK カーネル、ControllerControl ルーチンを記述
- 書き込みの ControllerControl ルーチン
- ControllerControl ルーチンでは、ストレージ
- ストレージの WDK コント ローラーのオブジェクト
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a7a545b209d7e1717ca00123207e1991602ae3c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382986"
---
# <a name="storage-requirements-for-controllercontrol-routines"></a>ControllerControl ルーチンの記憶域の要件





ある場合、 *ControllerControl* 、日常的な非 WDM ドライバーはの常駐記憶域を提供する必要があります、 *ControllerObject*によって返されたポインター [ **IoCreateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatecontroller).

ドライバーは、デバイスの拡張機能またはドライバーによって割り当てられた非ページ プールのために必要な記憶域を提供できます。 通常、コント ローラーのオブジェクトを使用するドライバー、保存、 *ControllerObject*各コント ローラーによって表されるハードウェアによって制御される論理または物理デバイスを表すデバイス オブジェクトの拡張機能でデバイスのポインターオブジェクト。

ドライバーの作成者は、サイズとの内部構造を決定、 *ControllerObject*-&gt;**ControllerExtension**します。

できないと、名前を指定する、コント ローラー オブジェクトは、I/O 要求のターゲットにすることはできません。 表す、通常はハードウェアでは、一連の I/O 要求の実際の対象となっている同種のデバイスを制御します。

 

 




