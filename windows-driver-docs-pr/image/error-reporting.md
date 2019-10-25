---
title: エラー報告
description: エラー報告
ms.assetid: 6f8c08f4-2809-4f49-9332-bbee85399404
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3caafafaa775e3296f90008924514e4bf7004819
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840844"
---
# <a name="error-reporting"></a>エラー報告





[IWiaMiniDrv インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)のすべてのメソッドは、COM HRESULT 値を返します。 メソッドが成功した場合、ミニドライバーは S\_OK を返し、 *Pldeverrval*パラメーターが指すデバイスエラー値をクリアします。 メソッドが失敗した場合、ミニドライバーは標準の COM エラーコードを返し、\**Pldeverrval*をデバイス固有のエラーコードとして設定します。 WIA サービスは[**IWiaMiniDrv::D rvgetdeviceerrorstr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetdeviceerrorstr)メソッドを呼び出して、 *Pldeverrval*が指す値に関連付けられたエラーメッセージ文字列を取得できます。 COM エラー値の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

 

 




