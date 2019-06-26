---
title: IEEE 1394 ノードの構成 ROM の内容を取得します。
description: Windows 7 には、1394ohci.sys、カーネル モード ドライバー フレームワーク (KMDF) を使用して実装されている、新しい IEEE 1394 バス ドライバーが含まれています。
ms.assetid: AC327938-A813-4665-8E2E-43BEE11D4AA9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae3ba4fa1c68e168954f0b3b2d6bd4754aacbfc4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381036"
---
# <a name="retrieving-the-contents-of-a-ieee-1394-nodes-configuration-rom"></a>IEEE 1394 ノードの構成 ROM の内容を取得します。


Windows 7 には、1394ohci.sys、カーネル モード ドライバー フレームワーク (KMDF) を使用して実装されている、新しい IEEE 1394 バス ドライバーが含まれています。 1394ohci.sys バス ドライバーでは、従来の IEEE バス ドライバー ポート/ミニポート構成--1394bus.sys と ochi1394.sys に置き換えられます。 従来の 1394 バス ドライバーとの互換性になります。 いくつか新しいと従来の 1394 バス ドライバーの動作で既知の違いについては、次を参照してください。 [Windows 7 での IEEE 1394 バス ドライバー](https://docs.microsoft.com/windows-hardware/drivers/ieee/IEEE-1394-Bus-Driver-in-Windows-7)します。

このトピックでは、1394ohci.sys バス ドライバーを後でデバイスの列挙に使用するノードの構成、ROM の内容を取得する方法の詳細を提供します。 Windows 7 は、デバイスの検出のノードの構成を ROM の内容の処理は変更されていません。 ノードの構成 ROM の内容を処理する方法の詳細については、次を参照してください。 [1394 構成 ROM を変更する](https://docs.microsoft.com/windows-hardware/drivers/ieee/modifying-the-1394-configuration-rom)します。

1394ohci.sys バス ドライバーは、1394 バスの非同期送信することによってリセットには、ノードへのトランザクションが読み取られた後に、ノードの構成 ROM の内容を取得します。 ノードの構成 ROM. の内容を取得するノードに送信される非同期の読み取りトランザクションの数を削減しよう

このトピックには、次のセクションが含まれています。

-   [構成の ROM ヘッダーを取得します。](#retrieving-the-configuration-rom-header)
-   [新しい構成 ROM](#new-configuration-rom)
-   [ROM の構成を取得しました。](#previously-retrieved-configuration-rom)
-   [関連トピック](#related-topics)

## <a name="retrieving-the-configuration-rom-header"></a>構成の ROM ヘッダーを取得します。


ノードの構成 ROM の内容を取得するには、クライアント ドライバーの送信、 [**要求\_取得\_ローカル\_ホスト\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff537644)への要求、IEEE 1394 のドライバー スタックを指定して、 **u.GetLocalHostInformation.nLevel** GET に\_ホスト\_CONFIG\_ROM. バス ドライバーが内のノードの構成 ROM ヘッダーを取得する要求を完了すると、 [**取得\_ローカル\_ホスト\_info 5** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/1394/ns-1394-_get_local_host_info5)構造体。 構成 ROM のヘッダーがノードの構成 ROM. の最初の 5 つ quadlets に このヘッダーには、IEEE 1394 a 仕様で定義されている、バス情報ブロックの内容が含まれています。

1394ohci.sys バス ドライバーは、トランザクションの読み取り、1 つの非同期ブロックで構成 ROM ヘッダーを取得しようとします。 ただし、1394 の特定のデバイスが応答しませんこのトランザクションに正しく。 このような状況では、新しい 1394 バス ドライバーは、構成の ROM ヘッダーを取得するのに 5 つの非同期 quadlet 読み取りトランザクションを使用します。

ノードとの通信の速度は、ノードの構成の ROM ヘッダーの取得中に決定されます。 1394ohci.sys バス ドライバーでは、サポートされている最速の速度でノードに非同期の読み取りトランザクションを送信し、ローカル ノードとターゲット ノードの間の低速のノードを考慮します。 非同期の読み取りトランザクションが完了しない場合が正常に速度が、最速サポートされている、1394ohci.sys バス ドライバーでは、他の非同期の読み取りトランザクション速度を遅くノードに送信します。 1394ohci.sys バス ドライバーは、トランザクションが正常に完了するまでに時間がかかり、低速のスピードでノードに非同期の読み取りトランザクションを送信し続けます。 非同期トランザクションの速度に使用される特定の速度で完了した後は、1394 の別のバスのリセットされるまでノードを持つすべての追加の通信が発生します。 非同期の読み取りトランザクションが完了しない場合の転送速度が最も遅いこと、1394ohci.sys バス ドライバーがノードの構成 ROM. の内容を取得できません。

構成 ROM ヘッダーが取得された後 1394ohci.sys バス ドライバーは、ノードの構成 ROM の内容を以前に取得されたかどうかを確認します。 そうである場合は、キャッシュされたバージョンを再利用できます。 ノードの構成 ROM. の残りの内容を取得する必要がありますそれ以外の場合、

## <a name="new-configuration-rom"></a>新しい構成 ROM


場合 1394ohci.sys バス ドライバーでは、ROM は以前は取得されませんでした、そのノードの構成の内容に処理されて、そのノードの構成 ROM. の残りの内容を取得するかを決定します。

1394ohci.sys バス ドライバーを使用して、 **max\_rom**非同期のサイズを決定する構成 ROM ヘッダーのバス情報ブロックの値の読み取り、残りを取得するノードに送信するトランザクションROM. 構成の内容 非同期読み取りトランザクションが失敗した場合などに関係なく、 **max\_rom**値-新しい 1394 バス ドライバーでは、読み取りトランザクションの非同期作成されますを使用して、ノードの構成 ROM. の残りの内容を取得するには

## <a name="previously-retrieved-configuration-rom"></a>ROM の構成を取得しました。


1394ohci.sys バス ドライバーは、ノードの構成の ROM ヘッダーの内容を取得した後は、以前取得した、ドライバー構成 ROM の内容のキャッシュされたコピーのいずれかのヘッダーがヘッダーに一致するかどうかを決定します。 It には、一致する構成 ROM ヘッダーが検出されると、再利用キャッシュされた構成 ROM の内容をそのします。

1394ohci.sys バス ドライバーでは、ノードの構成 ROM の内容のキャッシュされたコピーを再利用できるかどうかを判断するのに、次の手順を使用します。

1.  バス ドライバーを決定するかどうか、**ノード\_ベンダー\_id**、**チップ\_id こんにちは**、および**チップ\_id lo**ノードの ROM 構成ヘッダーのバス情報ブロックの値では、これらの同じ構成 ROM の内容のドライバーのキャッシュされたコピーのいずれかのヘッダー値と一致します。
2.  一致が見つかった場合、手順 1 バス ドライバー、バス情報ブロックの generation 値にも一致するかどうかを判断します。 生成値が変化していない (または、ことを示す 1 に設定されている場合、変更できません)、バス ドライバーを再利用 ROM. 構成のキャッシュされたコンテンツ

IEEE 1394 仕様では、前の手順では、ROM の値で構成の説明を見つけることができます。 1394ohci.sys バス ドライバーが、一致する構成 ROM ヘッダーをキャッシュに失敗した場合、またはため、ノードの構成 ROM の内容を読み込んで必要がありますが、**生成**値を変更し、前の手順に従います新しい構成 ROM. の内容を取得します。

## <a name="related-topics"></a>関連トピック
[IEEE 1394 ドライバー スタック](https://docs.microsoft.com/windows-hardware/drivers/ieee/the-ieee-1394-driver-stack)  
[1394 構成 ROM の修正](https://docs.microsoft.com/windows-hardware/drivers/ieee/modifying-the-1394-configuration-rom)  
[**要求\_取得\_CONFIG\_ROM**](https://msdn.microsoft.com/library/windows/hardware/gg266404)  



