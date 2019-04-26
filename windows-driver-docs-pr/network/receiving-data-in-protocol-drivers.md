---
title: プロトコル ドライバーのデータの受信
description: プロトコル ドライバーのデータの受信
ms.assetid: 758c6a86-6704-410b-ba13-bf589b1e330f
keywords:
- 受信側のデータの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd6d71ac8c24e7ea5d063cb70d0525a31a13202e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342922"
---
# <a name="receiving-data-in-protocol-drivers"></a>プロトコル ドライバーのデータの受信





次の図は、基本的な受信操作で、プロトコル ドライバー、NDIS、およびドライバー スタック内の基になるドライバーが含まれます。

![基本的なを示す図は、プロトコル ドライバー、ndis、およびドライバー スタック内の基になるドライバーの操作を受信します。](images/protocolreceive.png)

NDIS 呼び出しプロトコル ドライバーの[ *ProtocolReceiveNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff570267)を処理する関数が基になるドライバーからインジケーターを受信します。 NDIS 呼び出し*ProtocolReceiveNetBufferLists*受信を示す値の関数を呼び出して、基になるドライバーから (たとえば、 [ **NdisMIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff563598)) を受信したネットワーク データまたはループバック データを示します。

場合、 **NDIS\_受信\_フラグ\_リソース**フラグ、 *ReceiveFlags*パラメーターの[ *ProtocolReceiveNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff570267)プロトコル ドライバーの所有権を保持するが設定されている、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体にそれを呼び出すまで、 [ **NdisReturnNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff564534)関数。 NDIS が設定されている場合、 **NDIS\_受信\_フラグ\_リソース**フラグは、プロトコルのドライバーを保持できません、 **NET\_バッファー\_一覧**構造と関連付けられているリソース。 セット**NDIS\_受信\_フラグ\_リソース**フラグは、基になるドライバーが不足していることを示しますでリソースを受信します。 ここで、 *ProtocolReceiveNetBufferLists*関数がプロトコルに割り当てられた記憶域に受信したデータをコピーし、可能な限り早くを返す必要があります。

**注**  NDIS は、基になるドライバーを示すフラグを変更できます。 たとえば、ミニポート ドライバーの設定、 **NDIS\_受信\_フラグ\_リソース**フラグ、 *ReceiveFlags*のパラメーター、 [ **NdisMIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff563598)関数、NDIS は指定されたデータをコピーしてへのコピーを渡す[ *ProtocolReceiveNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff570267)で、**NDIS\_受信\_フラグ\_リソース**フラグをクリアします。

 

**注**  場合、 **NDIS\_受信\_フラグ\_リソース**フラグが設定されており、プロトコル ドライバーには、元のセットを保持する必要があります[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)リンク リスト内の構造体。 たとえば、このフラグが設定されている場合、ドライバー可能性があります、構造を処理、返しますが、元のリンクされたリストを復元する必要があります前に、一度に 1 つ、スタックにそれらを示します。

 

プロトコルのドライバーの呼び出し、 [ **NdisReturnNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff564534)関数の一覧の所有権を解放する[ **NET\_バッファー\_]ボックスの一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)構造体の場合は、関連付けられていると共に、 [ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造体、およびネットワークのデータ。

 

 





