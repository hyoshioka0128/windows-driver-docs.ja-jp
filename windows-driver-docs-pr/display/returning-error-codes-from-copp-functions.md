---
title: COPP 関数から返されるエラー コード
description: COPP 関数から返されるエラー コード
ms.assetid: a42fba73-59b2-4106-ba2b-9e96cd8524c8
keywords:
- 保護 WDK COPP、エラー コードをコピーします。
- ビデオのコピー防止 WDK COPP、エラー コード
- COPP WDK DirectX va なので、エラー コード
- ビデオの WDK COPP、エラー コードの保護
- エラー コードの WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f3ccfeb986853dff58b2c9fe4b526412aef069f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365623"
---
# <a name="returning-error-codes-from-copp-functions"></a>COPP 関数から返されるエラー コード


**このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。**

[COPP DDI](sample-functions-for-copp.md)エラー コードの次の種類を返すことができます。

-   定義されているエラー コード、 *winerror.h*ヘッダー ファイルとは、すべての Windows アプリケーションに共通します。 これらの Windows エラー コードが始まり、E\_プレフィックス。

-   定義されているエラー コード、 *ddraw.h*ヘッダー ファイルとは、DirectDraw に固有です。 DirectDraw これらのエラー コードが始まり、DDERR\_プレフィックス。

エラー コードは、COPP DDI に固有ではありません。

COPP DDI を実装する場合に、次の Windows エラー コードの使用量を制限する必要があります。

-   E\_予期しません。

    ディスプレイ ドライバーは、無効な状態です。 たとえば、 [ *COPPSequenceStart* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppsequencestart)する前に関数が呼び出された、 [ *COPPKeyExchange* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppkeyexchange)関数。

-   E\_INVALIDARG

    ドライバーに渡される入力パラメーターが無効です。

-   E\_ポインター

    有効なアドレスを指す必要があります、出力パラメーターは**NULL**します。

COPP DDI E を返すことができます\_、および失敗および DDERR\_一般的なエラー コードです。 ただし、エラーの原因が示さないため、その使用はお勧めします。

各 COPP 関数は「解説」の指定、DDERR\_ COPP 関数を報告するエラー コード。 返す他の任意の DDERR COPP DDI は要求されません\_エラー コード。

戻り値を使用する必要がある、ディスプレイ ドライバー、ビデオのミニポート ドライバーで COPP DDI からエラー情報を反映するときに、 [ **EngDeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeviceiocontrol)関数は、ため、Windowsカーネルに IOCTL から返されるエラー値を操作する**EngDeviceIoControl**します。 代わりに、エラー情報を渡す必要があります、 *lpInBuffer*パラメーターの**EngDeviceIoControl**します。 詳細については、次を参照してください。 [COPP DDI をディスプレイ ドライバーから呼び出す](calling-the-copp-ddi-from-the-display-driver.md)とコード例で[COPP ビデオのミニポート ドライバー テンプレート](copp-video-miniport-driver-template.md)と[COPP 操作の実行](performing-copp-operations-example.md)します。

 

 





