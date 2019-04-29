---
title: パラレル デバイスの読み取りと書き込み
description: パラレル デバイスの読み取りと書き込み
ms.assetid: f28506b1-fa87-4119-a57a-2b49573197d8
keywords:
- デバイスの読み取り、WDK を並列します。
- 並列デバイス WDK、書き込み
- 並列のデバイスの読み取り
- 並列デバイスへの書き込み
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ded95e2b136c630d9f69aba8303ca99ef7162800
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384976"
---
# <a name="reading-and-writing-a-parallel-device"></a>パラレル デバイスの読み取りと書き込み





クライアントを読み取ってを使用して並列のデバイスを書き込みます[ **IRP\_MJ\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff544164)と[ **IRP\_MJ\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff544175)要求。 カーネル モード ドライバーは、システム提供も使用できます[ **PPARALLEL\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff544537)と[ **PPARALLEL\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff544771)コールバック ルーチン。 システム提供の読み取り専用にポインターを取得し、コールバックを書き込み、カーネル モード ドライバーを使用して、 [ **IOCTL\_内部\_PARCLASS\_CONNECT** ](https://msdn.microsoft.com/library/windows/hardware/ff544040)要求返された、 [ **PARCLASS\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff544334)構造体。 **ParallelRead**と**ParallelWrite** 、PARCLASS のメンバー\_情報構造体は、コールバックへのポインター。

クライアントの使用は、読み取りおよび書き込み I/O の要求がある場合、パラレル ポート バス ドライバーは、並列のデバイスの作業キューに要求をキューします。 並列デバイスのクライアントは、パラレル ポートのシステム提供のバス ドライバーが自動的にロックおよびクライアントのポートのロックを解除するために、デバイスを読み書きする前にパラレル ポートのロックする必要はありません。

 

 




