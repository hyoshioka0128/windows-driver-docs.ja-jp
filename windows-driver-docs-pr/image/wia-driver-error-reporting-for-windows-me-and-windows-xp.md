---
title: Windows Me と Windows XP の WIA ドライバー エラー レポート
description: Windows Me と Windows XP の WIA ドライバー エラー レポート
ms.assetid: 5f696e16-0c22-4d71-98d2-d642e721ac8c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcbd156d288429edc6a5c5b69d8b7e31b3fb381f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840708"
---
# <a name="wia-driver-error-reporting-for-windows-me-and-windows-xp"></a>Windows Me と Windows XP の WIA ドライバー エラー レポート

WIA ミニドライバーには、拡張されたエラー情報を文字列形式で WIA アプリケーションに報告する機能があります。 HRESULT エラーコードを受信すると、WIA アプリケーションは**Iwiaitemextras:: GetExtendedErrorInfo**メソッド (Microsoft Windows SDK のドキュメントで説明) を呼び出して、エラーの詳細を説明する、ユーザーが判読できる文字列を取得できます。 このメソッドによって報告される文字列は、複数の言語にローカライズする必要があります。

WIA ミニドライバーは、エラー報告を実行するために次のメソッドを実装する必要があります。

[**Ib usd:: GetLastError**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getlasterror) − WIA サービスは、このメソッドを呼び出して、最近失敗した操作のデバイス固有のエラーコードを取得します。

[**Ib usd:: GetLastErrorInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getlasterrorinfo) − WIA サービスは、このメソッドを呼び出して、 **i、Usd:: GetLastError**メソッドの呼び出しから返されたエラーコードに関する拡張情報を取得します。

[**IWiaMiniDrv::D rvgetdeviceerrorstr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetdeviceerrorstr) − WIA サービスは、このメソッドを呼び出して、エラーの詳細を説明するすべての参照可能な文字列を取得します。または、エラーの後に進む方法をエンドユーザーに指示します。 **Iwiaitemextras:: GetExtendedErrorInfo**メソッドは、このメソッドが取得したエラー文字列を返します。

[IWIAMINIDRV COM インターフェイス](iwiaminidrv-com-interface.md)メソッドのいずれかが失敗した場合、WIA サービスはエラー情報を要求します。
