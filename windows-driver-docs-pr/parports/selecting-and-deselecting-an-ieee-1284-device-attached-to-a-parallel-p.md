---
title: パラレル ポートに接続されている IEEE 1284 デバイスの選択と選択解除
description: パラレル ポートに接続されている IEEE 1284 デバイスの選択と選択解除
ms.assetid: 1a3ac1b1-9180-4b71-8740-70c6fbe9a885
keywords:
- IEEE 1284 WDK
- パラレル ポート WDK、IEEE 1284 デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2258c60201d3a224206dcc969fdea10851ef119
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365372"
---
# <a name="selecting-and-deselecting-an-ieee-1284-device-attached-to-a-parallel-port"></a>パラレル ポートに接続されている IEEE 1284 デバイスの選択と選択解除





クライアントは、選択し、次の内部デバイス制御要求を使用してパラレル ポートに接続されている、IEEE 1284.3 デバイスの選択を解除します。

[**IOCTL\_内部\_選択\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff544052)

[**IOCTL\_内部\_解除\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff543987)

カーネル モード ドライバーは、システム提供も使用できます[デバイス コールバック ルーチンを並列](https://msdn.microsoft.com/library/windows/hardware/ff544275)を使用して取得される、 [ **IOCTL\_内部\_取得\_並列\_PNP\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff543997)要求。 この要求を返します、 [**並列\_PNP\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff544299)システム提供のコールバックに次のポインターを含む構造体。

-   **TrySelectDevice**メンバーへのポインターを[ *PPARALLEL\_を再試行してください\_選択\_日常的な*](https://msdn.microsoft.com/library/windows/hardware/ff544767)コールバックで、選択を解除します。IEEE 1284.3 デイジー チェーン デバイスまたはパラレル ポートに接続されている IEEE 1284 チェーンの最後のデバイス。

-   **DeselectDevice**メンバーへのポインターを[ *PPARALLEL\_解除\_ルーチン*](https://msdn.microsoft.com/library/windows/hardware/ff544504)コールバックを IEEE 1284.3 デイジー チェーンを選択します。デバイスまたはパラレル ポートに接続されている IEEE 1284 チェーンの最後のデバイス。

の要求が最も低いパラレル ポートが別のクライアントが割り当てられている場合、パラレル ポートのシステムによって提供される関数のドライバーがクライアントの選択の要求をキューにあるため、クライアントによって処理します。 パラレル ポート関数ドライバーには、要求がキューから後、は、IEEE 1284.3 デバイスを選択して、ポートを割り当てることを試行します。 クライアントは、タイムアウトの許容遅延またはその他デバイス固有の条件のため、いつでも選択の要求をキャンセルできます。

**注**  クライアントのみを使用する場合、 [ **PPARALLEL\_を再試行してください\_選択\_日常的な**](https://msdn.microsoft.com/library/windows/hardware/ff544767)並列を選択しようとするコールバックデバイス、およびその他のクライアントをパラレル ポートの競合しているシステムによって提供される関数のドライバーをパラレル ポート可能性があることはありません、ポートに割り当てるクライアント。 成功を確実には、クライアントを使用する必要があります、 [ **IOCTL\_内部\_選択\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff544052)要求。 (パラレル ポート関数ドライバーのキュー、およびその後プロセス、ポートの要求の割り当てし、デバイスが選択するデバイスで要求が受信した順序で要求を選択します)。

 

パラレル ポート機能のドライバーを選択すると、クライアントに対して IEEE 1284.3 デバイスをクライアントが、ポートと、選択した IEEE 1284.3 デバイスへの排他アクセスします。 クライアントが呼び出す必要があります、 [ **PPARALLEL\_解除\_ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff544504)ポートを解放して、IEEE 1284.3 デバイスの選択を解除するコールバック。 クライアントが、ポートを解放した後、パラレル ポート関数ドライバーが存在する場合は、保留中の要求をキューからし、要求を処理します。

Microsoft Windows 2000 は、ポートごとに 4 つデイジー チェーン接続デバイスをサポートしています。ただし、ポートごとに最大で 2 つのデイジー チェーン接続デバイスの使用をお勧めします。 Windows XP では、1 ポートあたり最大で 2 つデイジー チェーンのデバイスをサポートします。

 

 




