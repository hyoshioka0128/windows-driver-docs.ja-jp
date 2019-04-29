---
title: WakeFromD0、WakeFromD1、WakeFromD2、WakeFromD3
description: WakeFromD0、WakeFromD1、WakeFromD2、WakeFromD3
ms.assetid: f01aaceb-babf-42da-bc4b-1a846c84a313
keywords:
- WakeFromD0
- WakeFromD1
- WakeFromD2
- WakeFromD3
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c4b5d45df5e3e6e150c449464b51698fc07584f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391442"
---
# <a name="wakefromd0-wakefromd1-wakefromd2-and-wakefromd3"></a>WakeFromD0、WakeFromD1、WakeFromD2、WakeFromD3





これらの各[**デバイス\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)構造体のメンバーは、デバイスことができます、デバイスが指定された状態を受信する外部のシグナルへの応答がスリープ解除するかどうかを示します。

すべての 4 つのデバイスの電源をサポートするデバイスのことができます (D0、D1、D2、D3) の状態を再開状態 D0 および D1 からのみ、 **WakeFromD0**と**WakeFromD1**ビットが設定されている、 **WakeFromD2**と**WakeFromD3**のビットがクリアされます。

 

 




