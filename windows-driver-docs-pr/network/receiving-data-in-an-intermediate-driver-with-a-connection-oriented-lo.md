---
title: 下のエッジ中間ドライバーのデータ受信を接続指向
description: 接続指向の下端と中間のドライバーのデータの受信
ms.assetid: c14b4e8a-cfa2-4771-83b2-aa20fda79d39
keywords:
- 中間ドライバー WDK ネットワー キング、受信操作
- NDIS は、ドライバー WDK を中間、受信操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7cf5b282e06a4c0fb512ff0debc58559f4aeac3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538770"
---
# <a name="receiving-data-in-an-intermediate-driver-with-a-connection-oriented-lower-edge"></a>接続指向の下端と中間のドライバーのデータの受信





NDIS を呼び出して、中間のドライバーの場合は、中間ドライバーは、接続指向のミニポート ドライバー上に重ねられる、 [ **ProtocolCoReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff570256)を受信したデータを示す関数。

基になる接続指向のミニポート ドライバーを呼び出すことでネットワーク データを示します[ **NdisMCoIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff563561)、1 つまたは複数のリンク リストを渡して[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。

接続指向の下端と中間のドライバーのデータの受信についての詳細については、[Connection-Oriented 操作](connection-oriented-operations.md)を参照してください。

 

 





