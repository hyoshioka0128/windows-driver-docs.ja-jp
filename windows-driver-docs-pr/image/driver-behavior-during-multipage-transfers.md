---
title: 複数ページ転送中のドライバーの動作
description: 複数ページ転送中のドライバーの動作
ms.assetid: ecf0428b-c11c-49ff-9aa3-322e55dbca07
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75806e0c93f4b7236db5d0d9124f7cad33fb7551
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840853"
---
# <a name="driver-behavior-during-multipage-transfers"></a>複数ページ転送中のドライバーの動作


ドライバーは、フォルダーの取得を直接サポートする必要はありません。 ドライバーでサポートされていない場合、WIA サービスは項目ツリーを再帰的にウォークし、 [**IWiaMiniDrv::D rvacquireitemdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)を呼び出します。これは、 [**wia\_IPA\_item\_FLAGS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-flags)プロパティで**wiaitemtypetransfer**ビットが設定されているすべての項目に対して行われます。

フォルダー取得をサポートするドライバーは、フォルダー項目の [ [**WIA\_ip\_転送\_機能**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-transfer-capabilities)] プロパティを公開する必要があります。 このプロパティはフラグプロパティであり、フォルダー取得機能が直接サポートされていることを示すために、\_子\_対応ビットを取得\_には、WIA\_転送する必要があります。 このサポートは、ドライバー自体がツリーをウォークして関連する項目を転送し、WIA サービスがフォルダーで**IWiaMiniDrv::D rvacquireitemdata**を呼び出すだけであることを意味します。 ドライバーでは、通常の転送要求とフォルダー取得要求を区別できます。これを行うには、WIA\_転送の*Lflags*パラメーターをテストして\_の子ビットを取得\_ます。

ドライバーがフォルダーの取得を直接サポートする主な理由の1つは効率です。 ドライバーは、各項目に対して、WIA サービスが転送を呼び出すよりも、複数の項目をはるかに効率的に転送できます。

この状況の好例として、マルチリージョンスキャン中が挙げられます。 スキャナーのフラットベッドで複数の領域 (個別の画像など) が検出されると、"フラットな" アイテムから子として表現される可能性があります。 この状況の例を次の図に示します。

![マルチリージョンスキャンの項目ツリーを示す図](images/itemtree-multiregionscan.png)

"フラットベッド" の各子項目で別の転送が呼び出された場合、ドライバーは3つの個別のスキャンを実行するため、時間がかかる可能性があります。 ただし、フォルダー取得が "フラットベッド" で要求された場合、ドライバーは1つのスキャンを実行し、それを分解して、3つの個別の領域を戻します (多くの場合、高速です)。

**注**  は、より高度なドライバーのみがフォルダーの取得を直接サポートすることをお勧めします。これは、ドライバーが項目ツリーをウォークし、適切な操作を行う必要があるためです。

 

 

 




