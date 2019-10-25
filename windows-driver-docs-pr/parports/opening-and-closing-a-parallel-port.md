---
title: パラレル ポートの開始と終了
description: パラレル ポートの開始と終了
ms.assetid: 2183ffd9-8265-4848-b5d1-703643e0d0e6
keywords:
- パラレルポート WDK、開く
- パラレルポート WDK、終了
- パラレルポート WDK、共有
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64fb36c198e9e1777f48ed9b8bbbe11899f08e39
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844495"
---
# <a name="opening-and-closing-a-parallel-port"></a>パラレル ポートの開始と終了





クライアントは、パラレルポートを共有できます。 クライアントは、他の i/o 要求を使用したり、[パラレルポートコールバックルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を使用したりする前に、パラレルポートでファイルを開く必要があります。 クライアントがポートでファイルを閉じた後に、クライアントがパラレルポートとの通信を試行することはできません。

プラグアンドプレイ環境では、開いているファイルがないときは常にデバイスを削除または追加できます。 一般に、パラレルポートが追加されるたびに、プラグアンドプレイによって別の場所とリソースが割り当てられます。

 

 




