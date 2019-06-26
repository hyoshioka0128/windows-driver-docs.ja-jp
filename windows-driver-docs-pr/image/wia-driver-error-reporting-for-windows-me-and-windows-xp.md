---
title: Windows Me と Windows XP の WIA ドライバー エラー レポート
description: Windows Me と Windows XP の WIA ドライバー エラー レポート
ms.assetid: 5f696e16-0c22-4d71-98d2-d642e721ac8c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd29096ffcaeeb6e60d8f7ff8452b827064f6fff
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383763"
---
# <a name="wia-driver-error-reporting-for-windows-me-and-windows-xp"></a>Windows Me と Windows XP の WIA ドライバー エラー レポート





WIA ミニドライバーでは、文字列形式の WIA アプリケーションを拡張エラー情報を報告する機能があります。 HRESULT エラー コードを受け取ったら、WIA アプリケーションを呼び出すことができます、 **IWiaItemExtras::GetExtendedErrorInfo**ユーザーが判読できる文字列の詳細を記述する (Microsoft Windows SDK のドキュメントで説明) メソッドエラー。 このメソッドによって報告された文字列は、複数の言語にローカライズする必要があります。

WIA ミニドライバーは、エラー報告を実行する次のメソッドを実装する必要があります。

[**IStiUSD::GetLastError** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-getlasterror) −、WIA サービスが最近失敗したアクションをデバイスに固有のエラー コードを取得するには、このメソッドを呼び出します。

[**IStiUSD::GetLastErrorInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-getlasterrorinfo) −、WIA サービスから返されたエラー コードに関する拡張情報を取得するには、このメソッドを呼び出し、 **IStiUSD::GetLastError**メソッドの呼び出し。

[**IWiaMiniDrv::drvGetDeviceErrorStr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetdeviceerrorstr) −、WIA サービスは、エラー後に続行する方法の詳細、または手順については、エンドユーザーにエラーを説明するすべての表示可能な文字列を取得するには、このメソッドを呼び出します。 **IWiaItemExtras::GetExtendedErrorInfo**メソッドは、このメソッドの取得エラー文字列を返します。

WIA サービスのいずれかのエラー情報を求める、 [IWiaMiniDrv COM インターフェイス](iwiaminidrv-com-interface.md)メソッドが失敗します。

 

 




