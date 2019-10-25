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
ms.openlocfilehash: 0d6015f4d0a6c63754b1dabbe2b5256ba01700ab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835771"
---
# <a name="wakefromd0-wakefromd1-wakefromd2-and-wakefromd3"></a>WakeFromD0、WakeFromD1、WakeFromD2、WakeFromD3





これらの各[**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)の構造体のメンバーは、デバイスが指定された状態になったときに着信する外部シグナルに応答してデバイスを目覚めさせることができるかどうかを示します。

4つのデバイスの電源状態 (D0、D1、D2、D3) をすべてサポートしているデバイスでは、状態が D0 および D1 の場合にのみ機能しますが、 **WakeFromD0**と**WakeFromD1**のビットは設定され、 **WakeFromD2**と**WakeFromD3**のビットはクリアされます。

 

 




