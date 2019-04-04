---
title: 中間ドライバー ネットワーク データ管理
description: 中間ドライバー ネットワーク データ管理
ms.assetid: 12f708b9-32f2-470c-bc4d-7c1b0c1012b1
keywords:
- 中間ドライバー WDK ネットワーク、ネットワーク データの管理
- NDIS 中間ドライバー WDK、ネットワーク データの管理
- ネットワーク データ管理 WDK NDIS 中間
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbe36a437adb9db84fcc7dff9656baef6aa2113c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579478"
---
# <a name="intermediate-driver-network-data-management"></a>中間ドライバー ネットワーク データ管理





中間のドライバーを受け取る[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)ネットワーク経由で送信するためのより高度なドライバーから MDLs が 1 つまたは複数の構造に関連付けられています。 中間のドライバーは、基になるドライバーを使用してデータを呼び出すことによって渡すことができます[ **NdisSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff564535)ドライバーはコネクションレスの下端または呼び出すことによって[ **NdisCoSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff561728)場合、ドライバーは接続指向の下端。 代わりに、中間のドライバーによってアクションを実行できますいずれかを変更チェーン バッファー順序、または他の通信の基準とした受信データのタイミングの内容。

このようなドライバーが着信ネットへチェーンされているバッファーを再、中間のドライバーの目的に応じて\_バッファー\_リストの構造体。 たとえば、中間のドライバーは、次の状況でネットワーク データをは。

-   中間のドライバーより大きなデータ バッファーを上位のプロトコル ドライバーから基になるメディア上で 1 つのバッファーで送信することよりもを受信します。 その結果、中間のドライバーでは、小さなバッファーに、受信データを分割する必要があります。

-   中間のドライバーでは、長さまたは基になるドライバーに圧縮または各転送する前にデータを暗号化によってデータを送信するネットワークの内容を変更します。

データ管理のネットワークを作成する方法の詳細については、[プロトコル ドライバー バッファー管理](protocol-driver-buffer-management.md)を参照してください。

NDIS 複製およびフラグメントにインターフェイスを提供する[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体。 複製と構造体をフラグメント化の詳細については、[派生 NET\_バッファー\_リスト構造](derived-net-buffer-list-structures.md)を参照してください。

NET\_バッファー\_ドライバーの初期化時、または、必要に応じて、リストの構造体を割り当てることができる、 [ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)関数。 中間ドライバー開発者は、割り当てることができます、必要に応じて、パフォーマンス上の理由から、構造体の数の初期化時にように[ **ProtocolReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff570267)が事前に割り当てられます上位レベルのドライバーを示すための受信データをコピー先のリソース、および[ *MiniportSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559440)で使用できるように[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造 (と可能性があるバッファー) を渡す受信は、[次へ] の下位のドライバーにネットワーク データを送信します。

中間のドライバーを呼び出すことができる場合、中間のドライバーは新しいバッファーまたはバッファーにデータを送信または受信したデータをコピーし、最後のバッファーの実際のデータの長さが割り当てられたバッファーの長さより小さい、 **NdisAdjustMdlLength**バッファー データの実際の長さを調整します。

コネクションレスの下端と中間のドライバーがから基になるミニポート アダプターからの着信データを常に受信その[ **ProtocolReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff570267)関数。

接続指向の下端と中間のドライバーがから基になるミニポート アダプターからの着信データを常に受信その[ **ProtocolCoReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff570256)関数。

 

 





