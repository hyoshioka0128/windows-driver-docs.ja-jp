---
title: ファイル転送
description: ファイル転送
ms.assetid: 1c776dc5-982a-4652-bc03-f334fda30055
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 550c2d7868956268a3306f541ca5e9552b1ba61d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840838"
---
# <a name="file-transfers"></a>ファイル転送





**注**   ファイル転送は、Windows Vista より前のオペレーティングシステム用です。

 

*ファイルデータ転送*とは、wia ミニドライバーから、wia サービスによって作成されたファイルに画像データを転送することです。 データ転送を開始する WIA アプリケーションは、ファイル転送を実行する準備ができていることを、WIA サービスに示します。

次に、WIA サービスがファイルを作成し、ファイルにデータを転送するように WIA ミニドライバーに指示します。 WIA ミニドライバーは、転送されるデータを要求することによってデバイスに接続します。 ミニドライバーには独自のメモリが必要なので、低いレベルのバスドライバースタックでは、取得したデータをバッファーに配置できます。 WIA ミニドライバーは、バッファー内のデータを受信すると、 [**wiasWriteBufToFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritebuftofile) WIA サービスライブラリ関数を使用して、メモリバッファーを渡します。 次の図に示すように、wia サービスライブラリは、wia サービスによって作成されたファイルに、wia ミニドライバーのメモリバッファーの内容を書き込みます。

![wia ドライバーファイルのデータ転送を示す図](images/wia-imagedatafile.png)

ほとんどのファイル転送には、 **wiasWriteBufToFile** service library 関数を使用します。 [**WiasWritePageBufToFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiaswritepagebuftofile) service library 関数は、WIA サービスが複数ページの TIFF ファイルの書き込みを必要とするドライバーに対してのみ使用します。 複数ページにわたる TIFF ファイルを書き込むときに独自の TIFF ヘッダーを使用するドライバーは、 **wiasWriteBufToFile**を使用する必要があります。

 

 




