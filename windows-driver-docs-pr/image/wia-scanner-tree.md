---
title: WIA スキャナー ツリー
description: WIA スキャナー ツリー
ms.assetid: bd1452b9-1926-4dd6-b94c-e44f07573266
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e5afaabe43e254352bd8690c34377a77e23f126
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355168"
---
# <a name="wia-scanner-tree"></a>WIA スキャナー ツリー





次の図は、スキャナーとそれによって生成されるイメージを示します。

![スキャナーとそれによって生成されるイメージを示す図](images/art-scanner.png)

次の図は、Windows Vista での Windows XP または Microsoft Windows Me スキャナー、またはスキャナーを示していますドキュメント フィーダー、両面印刷ユニットまたはフィルム スキャナーが、そのスキャナーによってがないかどうかを提供します。

WIA では、スキャナー、および次の図のように、項目のツリーとして前の図に示すようにイメージを表します。

![wia が、スキャナー、および項目のツリーとしてイメージを表す方法を示す図](images/art-4.png)

スキャナーで、ルート項目は、一般的なデバイス プロパティ (カメラおよびスキャナーの両方に共通するプロパティ) とスキャナーに固有のデバイス プロパティで構成されます。 同様に、各子項目は、カメラおよびスキャナー項目の両方に共通するプロパティとスキャナーの項目に固有のプロパティで構成されます。

WIA サービスを介して、アプリケーションは、スキャナー項目から、次を要求できます。

-   スキャナーの機能のクエリを実行します。

-   スキャナーのデバイス プロパティを設定します。

-   データ転送を要求します。

ルート アイテムのすぐ下の Windows XP と Windows Me では、典型的なスキャナー オブジェクトは、デバイスのデータ収集機能を表すスキャナー項目、1 つの項目が。 アプリケーションは、スキャナーの項目のプロパティを設定して、スキャンを設定します。 アプリケーションは、項目から、WIA サービスによって、データを要求したときに、スキャンが実行されます。

Windows Me、Windows XP でアプリケーションは通常は自動ドキュメント フィーダー (ADFs) を持つ 2 つの項目 - ルート項目と 1 つの子で表されるなどのフラット ベッド スキャナーを想定します。 すべてのデータ転送は、子項目から実行されます。 ドライバー、プライベートの使用のためには、他の項目を作成することもでき、これらの項目を転送に対応できます。 (これを行うへの呼び出しで項目の型のフラグの WiaItemTypeTransfer ビットを設定[ **wiasCreateChildAppItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiascreatechildappitem)します。 この定数は、「Microsoft Windows SDK のドキュメントです。)ただし、アプリケーションは一般に、これらのプライベート項目について知るにはないと、それらを操作する方法がわからない。 ADF 機能の公開されているし、WIA を追加することにより、Windows XP、または Windows Me で ADF にスキャナーの\_DPS\_ドキュメント\_処理\_*XXX*プロパティをスキャナーのルートにスキャナーの子ではなく、項目を項目します。 これらのプロパティの詳細については、次を参照してください。 [WIA プロパティ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-properties)します。 Windows Vista では、ADF を使用した、スキャナーの詳細については、次を参照してください。 [WIA フィーダー スキャナー](wia-feeder-scanners.md)します。

ドライバーは報告されているデバイスが、フラット ベッドと ADF、および Windows XP、または Windows Me で双方向のスキャンを行うことができるかどうか、 [ **WIA\_DPS\_ドキュメント\_処理\_機能**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-capabilities)プロパティとして (フィード |フラット |DUP)。 確認しますの有効な値[ **WIA\_DPS\_ドキュメント\_処理\_選択**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-select)が正しく設定されています。 すべてのドキュメントを単一のスキャン ジョブでスキャンされる項目のツリー内の 1 つの子項目で存在することに注意してください。 Windows Vista で、スキャナー、ADF を使用し、両面印刷ユニットについては、次を参照してください。 [WIA フィーダー スキャナー](wia-feeder-scanners.md)します。

たとえば、アプリケーションは、ADF から 3 つのページの双方向のスキャンを実行しようとします。 これを実現するアプリケーションは、WIA を設定\_DPS\_ドキュメント\_処理\_にプロパティを選択します (フィーダー |双方向)、および設定は、 [ **WIA\_DPS\_ページ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-pages)プロパティを 3。 WIA を設定する必要がありますが、アプリケーションは、最初のページの先頭をスキャンする場合、\_DPS\_ドキュメント\_処理\_にプロパティを選択します (フィーダー |双方向 |前部\_最初)。 これは、アプリケーションがデータ転送元の要求が子項目に移動します。 ミニドライバーは、ADF ページ 1、2 ページとしてそのページのページ 3 として ADF では、2 番目のページの先頭と最初のページの先頭をレポートします。

デバイスは、ADF にある場合、ADF プロパティをサポートする必要があることに注意してください。

 

 




