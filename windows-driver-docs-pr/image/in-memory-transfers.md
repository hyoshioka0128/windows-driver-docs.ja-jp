---
title: メモリ内転送
description: メモリ内転送
ms.assetid: 90238354-e47c-41c7-bb6b-6337f39f63f0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa7cffc6fc25fdee85b933db99132ec329b968c0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551791"
---
# <a name="in-memory-transfers"></a>メモリ内転送





**注**  メモリ内転送は、Windows Vista 以前のオペレーティング システム。

 

*メモリ内データ転送*WIA サービスが割り当てられているメモリ バッファーに WIA ミニドライバーからデータをイメージの転送。 常に、データ転送を開始する WIA アプリケーションでは、データ転送のバッファーのサイズを決定します。 このデータ転送のバッファーのサイズで、ミニドライバーを定義する値より小さくすることはできません、 [ **WIA\_IPA\_バッファー\_サイズ**](https://msdn.microsoft.com/library/windows/hardware/ff551527)プロパティ。

WIA アプリケーションが、バッファーのサイズを決定した後は、データ転送を開始、WIA サービスを要求します。 WIA サービスは、要求されたサイズ (前の段落で説明したように、制約) に従って、WIA ミニドライバーがデータ転送を開始し、指定されたバッファーにデータを配置することを要求のメモリ バッファーを割り当てます。 WIA ミニドライバーは、データをバッファーに設定し、要求元の WIA アプリケーション データを返す WIA サービスに返します。 転送するデータがなくなるまで、このプロセスが繰り返されます。

次の図は、イメージのメモリの転送を示します。

![イメージのメモリ転送を示す図](images/wia-imagedatamem.png)

 

 




