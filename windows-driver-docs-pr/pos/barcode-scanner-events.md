---
title: バーコード スキャナーのイベント
description: Readfile 関数を使用して、デバイス ドライバーから Point of Service (POS) API レイヤーに渡されるイベントについて説明します。
ms.assetid: f0a7a525-8fea-4bce-a817-25c69cd47ddd
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5bdcc7015e81ec91a46e2481c2e7753b889c3ddf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358672"
---
# <a name="barcode-scanner-events"></a>バーコード スキャナーのイベント

このセクションに渡されるデバイス ドライバから Point of Service (POS) API レイヤーを使用してイベントを説明します[ReadFile](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)します。 このセクションでは、バーコード スキャナに固有のイベントについて説明します。

## <a name="in-this-section"></a>このセクションの内容

[BarcodeScannerDataReceived](barcodescannerdatareceived.md)  
スキャンが成功イベントの後に発生します。

[BarcodeScannerErrorOccurred](barcodescannererroroccurred.md)  
スキャンのエラーなど、エラーがある場合に発生します。

[BarcodeScannerImagePreviewReceived](barcodescannerimagepreviewreceived.md)  
デバイスがスキャンのビットマップ イメージを受け取ると発生します。

[BarcodeScannerTriggerPressed](barcodescannertriggerpressed.md)  
バーコード スキャナーのトリガが押されたときに発生します。

[BarcodeScannerTriggerReleased](barcodescannertriggerreleased.md)  
バーコード スキャナーのトリガーがリリースされたときに発生します。
