---
title: NFP デバイス インターフェイス
description: クライアント アプリケーションは、定義された一連の開いているハンドルに送信される I/O 制御コードを使用して近接デバイスと通信します。
ms.assetid: ED63FDCF-3253-4976-8571-82F4824923C5
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 582630ac2dd4ff0f5be93f3f1d77b3c38e4c30d9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377546"
---
# <a name="nfp-device-interface"></a>NFP デバイス インターフェイス


クライアント アプリケーションは、定義された一連の開いているハンドルに送信される I/O 制御コードを使用して近接デバイスと通信します。

## <a name="publication-and-subscription-handles"></a>パブリケーションおよびサブスクリプションの処理


各パブリケーションおよびサブスクリプションごとには、ドライバーへのオープン ハンドルとして表されます。 そのため、パブリケーションの M と N のサブスクリプションは、ドライバーに M と N の開いているハンドルと同等です。 Windows I/O マネージャー プロセスで妥当なハンドル数の制限が適用されます。

## <a name="generic-null-file-name-handles"></a>NULL の汎用のファイル名のハンドル


ドライバーを非パブリケーションおよびサブスクリプション以外の要求を送信するため、汎用のファイル ハンドルが開かれます。 この種類のハンドルを承諾する必要があります。 クライアントはメッセージの最大サイズと、ドライバーの転送速度を判断するのにこのハンドルを使用します。

## <a name="ioctl-support"></a>IOCTL サポート


近接デバイス ドライバー インターフェイスをサポートしている Ioctl は Nfpdev.h で定義されます。 制御コードは、次の属性で定義されます。

-   メソッド\_バッファーに格納されました。
-   ファイル\_ANY\_アクセス
-   ファイル\_デバイス\_NFP

各パブリケーションおよびサブスクリプションごとには、独自のドライバーに開いているハンドルとして示されています。 そのため、パブリケーションの M と N のサブスクリプションは、ドライバーに M と N の開いているハンドルと同等です。 Windows I/O マネージャー プロセスで妥当なハンドル数の制限が適用されます。

IOCTL コードが Nfpdev.h ヘッダー内に定義されています。

デバイスのセキュリティ記述子は OS やデバイス クラスの既定値として残しておきます。

## <a name="reserved-and-vendor-ioctl-codes"></a>予約されており、IOCTL 仕入先のコード


次の表では、予約されており、ベンダの特定のコントロールのコード範囲について説明します。

| 種類            | 範囲の開始                               | 範囲の終了                                 |
|-----------------|-------------------------------------------|-------------------------------------------|
| 予約済み        | `CTL_CODE(FILE_DEVICE_NFP, 0x0000, *, *)` | `CTL_CODE(FILE_DEVICE_NFP, 0x00FF, *, *)` |
| ベンダー固有 | `CTL_CODE(FILE_DEVICE_NFP, 0x0100, *, *)` | `CTL_CODE(FILE_DEVICE_NFP, 0x01FF, *, *)` |

 

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[フィールドの近接 DDI 参照の近く](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  

