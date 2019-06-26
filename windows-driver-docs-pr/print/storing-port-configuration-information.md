---
title: ポート構成情報の格納
description: ポート構成情報の格納
ms.assetid: b1c83729-d7d2-4920-9402-4e00baa12633
keywords:
- ポート管理の構成情報を格納する、WDK の印刷
- レジストリ WDK の印刷
- WDK モニターの印刷スプーラー レジストリ情報を印刷します。
- 印刷のポートの構成情報を格納します。
- スプーラ レジストリ情報の WDK 印刷モニター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e14f62814e13891e68d566891196e800bebb8225
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363972"
---
# <a name="storing-port-configuration-information"></a>ポート構成情報の格納





Windows 2000 およびそれ以降の印刷スプーラーはできるクラスター化または非クラスター化サーバー環境にどちらかで動作します。 スプーラがサーバー クラスターで動作している、ときに、クラスター レジストリに印刷モニターの構成情報を格納する必要があります。 その一方で、スプーラーが動作して、1 つの非クラスター化サーバー システムの場合、サーバーのローカル レジストリに印刷モニターの構成情報を格納する必要があります。

印刷スプーラーは印刷モニターによって使用されるレジストリ関数のセットを定義します。 これらの関数は、印刷のモニターは、サーバーがクラスター化されているかを判断する必要はありませんので、適切なレジストリに構成データを指示します。 印刷モニター使用しないで、Win32 のレジストリ API や、クラスター レジストリ API は直接すべての構成データは、格納する必要があり、スプーラーのレジストリの機能を使用してアクセスします。 印刷のモニターにこれらの関数のアドレスが指定される、 [ **MONITORREG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/ns-winsplp-_monitorreg)スプーラーがモニターを呼び出すときに[ **InitializePrintMonitor2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-initializeprintmonitor2)関数。

サーバー クラスターでは、スプーラーの複数のインスタンスが共存できます。 具体的には、各クラスター ノードが、独自のインスタンスを所有し、クラスター自体の追加のインスタンスが存在します。 スプーラ レジストリ関数の入力パラメーターの 1 つは、スプーラー ハンドルです。 このハンドルは、モニターのによって受信**InitializePrintMonitor2**関数し、モニターが開いているスプーラー インスタンス (ノードまたはクラスター) を識別します。 スプーラ ハンドルを使用して、スプーラー レジストリ関数は、スプーラー インスタンスごとにサブキーを維持します。

 

 




