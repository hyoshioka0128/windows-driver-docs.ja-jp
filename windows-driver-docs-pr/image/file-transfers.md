---
title: ファイル転送
description: ファイル転送
ms.assetid: 1c776dc5-982a-4652-bc03-f334fda30055
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a94ccac4efd642ccddcf07baf11f3c0f0a98b2e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385553"
---
# <a name="file-transfers"></a>ファイル転送





**注**  ファイル転送は、Windows Vista 以前のオペレーティング システム。

 

A*ファイル データの転送*WIA ミニドライバーから WIA サービスを作成したファイルにイメージ データの転送。 データ転送を開始する WIA アプリケーションは、ファイル転送を実行する準備ができたことを WIA サービスを示します。

WIA サービスは、ファイルを作成し、WIA ミニドライバーをファイルにデータを転送するように指示します。 WIA ミニドライバーは、転送されるデータを要求することによって、デバイスを接続します。 ミニドライバーでは、ため、低レベル バス ドライバー スタックは、バッファーに取得したデータを格納することが、独自のメモリが必要です。 WIA ミニドライバーは、バッファー内のデータを受け取る、使用して、 [ **wiasWriteBufToFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritebuftofile) WIA サービス ライブラリ関数は、メモリ バッファーに渡すことです。 WIA サービス ライブラリは、WIA サービスとして作成し、次の図は、のファイルに、WIA ミニドライバーのメモリ バッファーの内容を書き込みます。

![wia ドライバー ファイルのデータ転送を示す図](images/wia-imagedatafile.png)

使用して、 **wiasWriteBufToFile**サービス ライブラリ関数のほとんどのファイル転送。 使用して、 [ **wiasWritePageBufToFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiaswritepagebuftofile)ライブラリ関数を WIA を必要とするドライバーが複数ページの TIFF ファイルの書き込みにサービスに対してのみのサービスを提供します。 マルチページの TIFF ファイルを記述するときに、独自の TIFF ヘッダーを使用するドライバーを使用する必要があります**wiasWriteBufToFile**します。

 

 




