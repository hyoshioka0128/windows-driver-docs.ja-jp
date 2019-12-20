---
title: UMDF での I/O ターゲットの使用
description: UMDF での I/O ターゲットの使用
ms.assetid: 5633242c-ffab-4af5-9650-7449395deb6b
keywords:
- ユーザーモードドライバー WDK UMDF、i/o ターゲット
- UMDF WDK、i/o ターゲット
- ユーザーモードドライバーフレームワーク WDK、i/o ターゲット
- フレームワークベースのドライバー WDK UMDF、i/o ターゲット
- I/o ターゲット (WDK UMDF)
- WDK UMDF のターゲット
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7699261df8bed76846aa884878b61fc1ca99240
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210776"
---
# <a name="using-io-targets-in-umdf"></a>UMDF での I/O ターゲットの使用


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

ドライバーが i/o 要求を受信すると、ドライバーが要求を単独で処理できる可能性があります。または、他のドライバーのサポートが必要な場合もあります。 ドライバーでサポートが必要な場合は、要求を別のドライバーに転送するか、1つまたは複数の新しい要求を作成して別のドライバーに送信することができます。

UMDF ベースのドライバーは、i/o*ターゲット*を使用して、i/o 要求を別のドライバーに送信します。 各 i/o ターゲットは、i/o ターゲットオブジェクトによって表されます。 それぞれの i/o ターゲットオブジェクトは、主にキューです。 ドライバーが i/o ターゲットに要求を送信すると、フレームワークは、i/o ターゲットに要求を配信できるようになるまで、要求をキューに格納します。

このフレームワークは、一般的な i/o ターゲットと特殊化された i/o ターゲットの両方をサポートしています。

-   [一般的な i/o ターゲット](general-i-o-targets-in-umdf.md)は、すべての UMDF ドライバーで使用できますが、デバイス固有の特別なデータ形式はサポートされていません。

-   特殊化された i/o ターゲットを使用すると、UMDF ドライバーは特殊なターゲット固有のデータ書式設定を必要とする i/o 要求を送信できます。 現時点では、このフレームワークは[USB i/o ターゲット](usb-i-o-targets-in-umdf.md)をサポートしています。

フレームワークが、デバイスのデータ形式をサポートする特殊な i/o ターゲットを提供する場合、ドライバーは特殊な i/o ターゲットを使用する必要があります。 それ以外の場合、ドライバーは一般的な i/o ターゲットを使用する必要があります。

 

 





