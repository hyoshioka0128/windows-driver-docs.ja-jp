---
title: エラー報告
description: エラー報告
ms.assetid: 6f8c08f4-2809-4f49-9332-bbee85399404
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f782872739b6cab558436a70a3a66512a82fca78
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370055"
---
# <a name="error-reporting"></a>エラー報告





すべてのメソッド、 [IWiaMiniDrv インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)COM HRESULT 値を返します。 メソッドが成功すると、ミニドライバー返します S\_OK とクリア デバイス エラーの値、 *plDevErrVal*パラメーターが指します。 ミニドライバーが標準 COM エラー コードを返すメソッドが失敗した場合、設定と\* *plDevErrVal*デバイス固有のエラー コードを使用します。 WIA サービスを呼び出すことができます、 [ **IWiaMiniDrv::drvGetDeviceErrorStr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetdeviceerrorstr)によって示される値に関連付けられているエラー メッセージ文字列を取得するメソッド*plDevErrVal*します。 COM エラー値の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

 

 




