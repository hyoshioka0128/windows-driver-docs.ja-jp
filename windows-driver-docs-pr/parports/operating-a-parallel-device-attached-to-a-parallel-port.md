---
title: パラレル ポートに接続されているパラレル デバイスの操作
description: パラレル ポートに接続されているパラレル デバイスの操作
ms.assetid: 5ad36162-efbe-4be8-954c-964ef12c539a
keywords:
- パラレル ポート WDK、並列のデバイスの操作
- 並列デバイス WDK
- ベンダーから提供された並列ドライバー WDK、並列のデバイスの操作
- デバイス クライアントの操作、WDK を並列します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d41d24910fbee71f95dabf2f99d096b80cf2644c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377497"
---
# <a name="operating-a-parallel-device-attached-to-a-parallel-port"></a>パラレル ポートに接続されているパラレル デバイスの操作





このセクションでは、並列のデバイスでは、関数のベンダーから提供されたドライバーの具体的には、クライアントがパラレル ポートに接続されている並列のデバイスをどのように動作する方法について説明します。

パラレル ポートのシステム提供のバス ドライバーでは、パラレル ポートに列挙されている並列デバイスごとに物理デバイス オブジェクト (PDO) を作成します。 次のトピックでは、クライアントがデバイスの PDO によって提供されるインターフェイスを使用して並列のデバイスをどのように動作する方法について説明します。

[起動と使用の並列のデバイス](opening-and-using-a-parallel-device.md)

[並列デバイスへの接続](connecting-to-a-parallel-device.md)

[並列デバイスに関する情報を取得します。](obtaining-information-about-a-parallel-device.md)

[ロックおよび並列のデバイスで使用するため、パラレル ポートのロックを解除](locking-and-unlocking-a-parallel-port-for-use-by-a-parallel-device.md)

[設定および並列のデバイスの通信モードを解除](setting-and-clearing-a-communication-mode-for-a-parallel-device.md)

[並列のデバイスに属性を設定](setting-attributes-on-a-parallel-device.md)

[並列のデバイスの読み取りと書き込み](reading-and-writing-a-parallel-device.md)

パラレル ポートに接続されている並列のデバイスのサポートの詳細についてを参照してください。

[ParallelPorts とデバイスの概要](introduction-to-parallel-ports-and-devices.md)

[システム提供のパラレル ドライバー](system-supplied-parallel-drivers.md)

[システム提供平行ドライバーへのクライアント インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff543926)

 

 




