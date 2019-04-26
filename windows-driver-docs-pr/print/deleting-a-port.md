---
title: ポートの削除
description: ポートの削除
ms.assetid: 0d491368-e529-4f04-a323-678e31a862c3
keywords:
- ポート管理 WDK の印刷、ポートの削除
- 印刷ポートを削除します。
- 印刷ポートを削除します。
- DeletePort
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e42208e39f06de3ac4c56b92e3e6ae9b91949c8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355678"
---
# <a name="deleting-a-port"></a>ポートの削除





ポートの削除は、ポート モニター サーバー DLL のローカル ストレージとは、レジストリから、ポートのストアド名とユーザーが変更可能な構成情報を削除するので構成されます。

アプリケーションから印刷スプーラの**DeletePort** (Microsoft Windows SDK のドキュメントで説明)、関数、 **DeletePort**関数呼び出し、 [ **DeletePortUI** ](https://msdn.microsoft.com/library/windows/hardware/ff547432)ポート モニター、適切なポート モニターの UI の DLL に含まれる関数。

ポート モニター UI の DLL の**DeletePortUI**関数は、次の操作を実行する必要があります。

1.  印刷スプーラーを呼び出す**ようになりました**(Windows SDK のドキュメントで説明)、関数で、これにより、 [ **XcvOpenPort** ](https://msdn.microsoft.com/library/windows/hardware/ff564259)ポート監視のサーバー DLL 内の関数呼び出されます。

2.  印刷スプーラーを呼び出す[ **XcvData** ](https://msdn.microsoft.com/library/windows/hardware/ff564255)ポート監視サーバーのポートを削除する DLL を要求する関数の 1 つ以上の時間。 **XcvData**関数呼び出しのサーバー DLL の[ **XcvDataPort** ](https://msdn.microsoft.com/library/windows/hardware/ff564258)関数。

3.  印刷スプーラーを呼び出す**ClosePrinter** (Windows SDK のドキュメントで説明)、関数で、これにより、 [ **XcvClosePort** ](https://msdn.microsoft.com/library/windows/hardware/ff564254)ポート監視のサーバーでの関数呼び出される DLL です。

これらの操作の詳細については、の説明を参照してください。 [ **DeletePortUI**](https://msdn.microsoft.com/library/windows/hardware/ff547432)します。

 

 




