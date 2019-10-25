---
title: IEEE 1394 ノードの構成 ROM の内容を取得する
description: Windows 7 には、カーネルモードドライバーフレームワーク (KMDF) を使用して実装される新しい IEEE 1394 バスドライバーである 1394ohci .sys が含まれています。
ms.assetid: AC327938-A813-4665-8E2E-43BEE11D4AA9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 360e994f3ccada3d305a7869cf8bf23106bd5216
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841528"
---
# <a name="retrieving-the-contents-of-a-ieee-1394-nodes-configuration-rom"></a>IEEE 1394 ノードの構成 ROM の内容を取得する


Windows 7 には、カーネルモードドライバーフレームワーク (KMDF) を使用して実装される新しい IEEE 1394 バスドライバーである 1394ohci .sys が含まれています。 1394ohci バスドライバーは、ポート/ミニポート構成--1394ohci. sys および ochi1394 のレガシ IEEE バスドライバーを置き換えます。 レガシ1394バスドライバーとの下位互換性があります。 新しい1394バスドライバーとレガシバスドライバーの動作の既知の違いについては、「 [Windows 7 の IEEE 1394 バスドライバー](https://docs.microsoft.com/windows-hardware/drivers/ieee/IEEE-1394-Bus-Driver-in-Windows-7)」を参照してください。

このトピックでは、1394ohci のドライバーが、後でデバイスの列挙に使用されるノードの構成 ROM の内容を取得する方法について詳しく説明します。 Windows 7 では、デバイスの検出のためにノードの構成 ROM の内容を処理する操作は変更されていません。 ノードの構成 ROM の内容の処理方法の詳細については、「 [1394 構成 rom の変更](https://docs.microsoft.com/windows-hardware/drivers/ieee/modifying-the-1394-configuration-rom)」を参照してください。

1394ohci は、非同期の読み取りトランザクションをノードに送信することで、1394バスのリセット後にノードの構成 ROM の内容を取得します。 ノードに送信される非同期読み取りトランザクションの数を減らして、ノードの構成 ROM の内容を取得しようとします。

このトピックには、次のセクションが含まれています。

-   [構成 ROM ヘッダーを取得しています](#retrieving-the-configuration-rom-header)
-   [新しい構成 ROM](#new-configuration-rom)
-   [以前に取得した構成 ROM](#previously-retrieved-configuration-rom)
-   [関連トピック](#related-topics)

## <a name="retrieving-the-configuration-rom-header"></a>構成 ROM ヘッダーを取得しています


ノードの構成 ROM の内容を取得するために、クライアントドライバーは、 **u. GetLocalHostInformation**を指定することによって、 [ **\_ローカル\_ホストの\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff537644)要求を IEEE 1394 ドライバースタックに取得\_要求を送信します。 nlevel to\_ホスト\_構成\_ROM を取得します。 要求が完了すると、バスドライバーは[**GET\_ローカル\_ホスト\_INFO5**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_get_local_host_info5)構造体のノードの構成 ROM ヘッダーを取得します。 構成 ROM ヘッダーは、ノードの構成 ROM の最初の5つの quadlets にあります。 このヘッダーには、IEEE 1394a 仕様で定義されているように、バス情報ブロックの内容が含まれています。

1394ohci ドライバーは、単一の非同期ブロック読み取りトランザクションで構成 ROM ヘッダーを取得しようとします。 ただし、特定の1394デバイスがこのトランザクションに正しく応答しない可能性があります。 この場合、新しい1394バスドライバーは、5つの非同期 quadlet 読み取りトランザクションを使用して、構成 ROM ヘッダーを取得します。

ノードとの通信速度は、ノードの構成 ROM ヘッダーを取得するときに決定されます。 1394ohci は、サポートされる最速の速度でノードに非同期の読み取りトランザクションを送信し、ローカルノードとターゲットノードの間で低速のノードを考慮します。 非同期の読み取りトランザクションが、サポートされている最速の速度で正常に完了しない場合、1394ohci のバスドライバーは、より低速で別の非同期読み取りトランザクションをノードに送信します。 1394ohci を実行すると、非同期の読み取りトランザクションは、トランザクションが正常に完了するまで、低速で高速にノードに送信されます。 非同期トランザクションが特定の速度で完了すると、別の1394バスリセットが発生するまで、ノードとのすべての追加通信にその速度が使用されます。 非同期の読み取りトランザクションが、可能な限り遅い速度で完了しない場合、1394ohci のバスドライバーはノードの構成 ROM の内容を取得しません。

構成 ROM のヘッダーを取得した後、1394ohci は、ノードの構成 ROM の内容が以前に取得されたかどうかを確認します。 その場合は、キャッシュされたバージョンを再利用できます。 それ以外の場合は、ノードの構成 ROM の残りの内容を取得する必要があります。

## <a name="new-configuration-rom"></a>新しい構成 ROM


1394ohci のドライバーによって、ノードの構成 ROM の内容が以前に取得されていないと判断された場合は、ノードの構成 ROM の残りの内容を取得します。

1394ohci のドライバーは、configuration ROM ヘッダーの bus 情報ブロックの**max\_rom**値を使用して、構成の残りの内容を取得するためにノードに送信する非同期読み取りトランザクションのサイズを決定します。Bios. **\_rom の最大**値に関係なく、非同期の読み取りトランザクションが失敗した場合、新しい1394バスドライバーは非同期の quadlet 読み取りトランザクションを使用して、ノードの構成 rom の残りのコンテンツを取得します。

## <a name="previously-retrieved-configuration-rom"></a>以前に取得した構成 ROM


1394ohci のドライバーは、ノードの configuration ROM ヘッダーの内容を取得した後で、そのドライバーが以前に取得した構成 ROM の内容のうち、キャッシュされたコピーの1つのヘッダーと一致するかどうかを判断します。 一致する構成 ROM ヘッダーが見つかった場合は、キャッシュされた構成 ROM の内容を再利用します。

1394ohci のドライバーは、次の手順を使用して、ノードの構成 ROM の内容のキャッシュされたコピーを再利用できるかどうかを判断します。

1.  バスドライバーは、ノード **\_ベンダ\_id**、**チップ\_id hi**、**チップ\_id lo**値がノードの configuration ROM ヘッダーのバス情報ブロック内にあるかどうかを判断します。構成 ROM コンテンツのドライバーのキャッシュされたコピーの1つ。
2.  手順 1. で一致するものが見つかった場合、バスドライバーは、バス情報ブロックの世代値も一致するかどうかを判断します。 生成値が変更されていない場合 (または、変更されないことを示す1に設定されている場合)、バスドライバーは、構成 ROM のキャッシュされたコンテンツを再利用します。

構成 ROM の値の説明については、前述の IEEE 1394 仕様の手順を参照してください。 1394ohci ドライバーが、一致するキャッシュされた構成 ROM ヘッダーを見つけられなかった場合、または**世代**の値が変更されたためにノードの構成 rom の内容を再読み込みする必要がある場合は、前の手順に従って、の内容を取得します。新しい構成 ROM。

## <a name="related-topics"></a>関連トピック
[IEEE 1394 ドライバー スタック](https://docs.microsoft.com/windows-hardware/drivers/ieee/the-ieee-1394-driver-stack)  
[1394 構成 ROM の修正](https://docs.microsoft.com/windows-hardware/drivers/ieee/modifying-the-1394-configuration-rom)  
[ **\_構成\_ROM を取得\_要求**](https://msdn.microsoft.com/library/windows/hardware/gg266404)  



