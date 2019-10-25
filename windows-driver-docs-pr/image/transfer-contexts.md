---
title: コンテキストの転送
description: コンテキストの転送
ms.assetid: b4eadccd-afb6-4cb5-bf52-704f64d45e40
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: adc47c980071a2a5c909e5b75cda87e82d731f9c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840736"
---
# <a name="transfer-contexts"></a>コンテキストの転送





転送コンテキストは、ミニドライバーからアプリケーションへのデータ転送を記述する情報のコレクションです。 転送に関する情報は、 [**MINIDRV\_transfer\_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_minidrv_transfer_context)構造体に格納されます。 転送コンテキストには、転送されるイメージに関する情報 (サイズ、解像度、色深度 (ピクセルあたりのバイト数)、圧縮の種類、およびイメージ形式) を含むメンバーが含まれます。 WIA サービスは、 [**IWiaMiniDrv::D rvacquireitemdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)メソッドを呼び出す前に、関連する wia 項目のプロパティからこれらの値を取得します。 次に、値が MINIDRV に格納され、\_コンテキスト構造\_転送され、簡単にアクセスできるようにドライバーに渡されます。 このプロセスにより、ドライバーが WIA サービスライブラリルーチンを使用して、アプリケーション項目コンテキスト (つまり、WIA サービスコンテキスト) からこれらの値を読み取る必要がなくなります。

転送コンテキストには、転送の種類に関する情報 (ファイルデータ転送であるか、メモリコールバック転送であるかなど) も含まれます。 ファイルデータ転送の場合、1つのメンバーには、書き込まれるファイルへのハンドルが格納されます。 ミニドライバーはこのハンドルに触れないことをお勧めします。 WIA サービスは、転送が行われる前にハンドルを開き、転送が完了すると閉じます。 メモリコールバックデータ転送 (およびアプリケーションがミニドライバーから更新を受け取るファイルデータ転送の場合) では、メンバーにはミニドライバーのコールバックルーチンのアドレスが含まれます。

その他のメンバーには、転送で使用されるすべてのバッファーの合計サイズ、ミニドライバーまたは WIA サービスによって割り当てられたかどうかなどの情報が含まれます。 この構造体のメンバーの完全な一覧については、「 [**MINIDRV\_TRANSFER\_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_minidrv_transfer_context) 」を参照してください。

ミニドライバーは、 [**wiasGetImageInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetimageinformation)関数と共に、イメージ自体を記述する転送コンテキスト項目の多く (ピクセル単位の幅や行数など) を設定します。 WIA サービスでは、データ転送に関する多くの転送コンテキスト項目が設定されます。たとえば、ファイルハンドル (該当する場合) は転送の種類です。

 

 




