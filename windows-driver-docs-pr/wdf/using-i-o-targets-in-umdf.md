---
title: UMDF で I/O ターゲットを使用します。
description: UMDF で I/O ターゲットを使用します。
ms.assetid: 5633242c-ffab-4af5-9650-7449395deb6b
keywords:
- ユーザー モード ドライバー WDK UMDF、I/O のターゲット
- UMDF WDK、I/O のターゲット
- ユーザー モード ドライバー フレームワーク WDK、I/O のターゲット
- フレームワーク ベースのドライバー WDK UMDF、I/O のターゲット
- I/O ターゲット WDK UMDF
- WDK UMDF のターゲット
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd8ac3b30b27d7c568dcc8cb5395bcfbab6aa028
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556930"
---
# <a name="using-io-targets-in-umdf"></a>UMDF で I/O ターゲットを使用します。


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ドライバーは、I/O 要求を受け取るときに、ドライバーは、単独で要求を処理できる場合があります。 またはその他のドライバーのサポートを必要があります。 ドライバーは、アシスタンスを必要とする場合は、別のドライバーに要求を転送できます。 または 1 つまたは複数の新しい要求を作成して別のドライバーに送信します。

UMDF ベースのドライバーを使用して、 *I/O ターゲット*を別のドライバーの I/O 要求を送信します。 I/O の各ターゲットは、I/O のターゲット オブジェクトで表されます。 各 I/O ターゲット オブジェクトは、主にキューです。 ドライバーは、I/O のターゲットに要求を送信するときに、フレームワークは I/O ターゲットを要求を提供できますまでキューに要求を格納します。

フレームワークには、一般的な I/O ターゲットと特殊な I/O ターゲットの両方がサポートされています。

-   [一般的な I/O ターゲット](general-i-o-targets-in-umdf.md)UMDF ドライバーをすべてで使用できるは、すべての特殊なデバイスに固有のデータ形式をサポートしていません。

-   特殊な I/O ターゲットは、書式設定、特別なターゲット固有のデータを必要とする I/O 要求を送信する UMDF ドライバーを有効にします。 フレームワークのサポートは、現時点では、 [USB I/O ターゲット](usb-i-o-targets-in-umdf.md)します。

フレームワークは、デバイスのデータ形式をサポートする特殊な I/O ターゲットを提供する場合、ドライバーは、特殊な I/O ターゲットを使用してください。 それ以外の場合、ドライバーは、一般的な I/O ターゲットを使用する必要があります。

 

 





