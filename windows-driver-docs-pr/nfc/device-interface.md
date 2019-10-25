---
title: NFP デバイスインターフェイス
description: クライアントアプリケーションは、開いているハンドルに送信される一連の i/o 制御コードを使用して近接デバイスと通信します。
ms.assetid: ED63FDCF-3253-4976-8571-82F4824923C5
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a764b889eb57c3be72d78c5a0365b1110a0978df
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842539"
---
# <a name="nfp-device-interface"></a>NFP デバイスインターフェイス


クライアントアプリケーションは、開いているハンドルに送信される一連の i/o 制御コードを使用して近接デバイスと通信します。

## <a name="publication-and-subscription-handles"></a>パブリケーションとサブスクリプションのハンドル


各パブリケーションと各サブスクリプションは、ドライバーを開くハンドルとして表されます。 そのため、M パブリケーションと N サブスクリプションは、ドライバーに対して M + N 個の開いているハンドルに相当します。 Windows i/o マネージャーでは、プロセスに対する適切なハンドル数制限が適用されます。

## <a name="generic-null-file-name-handles"></a>汎用 NULL ファイル名ハンドル


パブリケーション以外の要求をドライバーに送信するために、汎用ファイルハンドルが開かれています。 この種類のハンドルは受け入れられる必要があります。 クライアントはこのハンドルを使用して、最大メッセージサイズとドライバーの転送速度を決定します。

## <a name="ioctl-support"></a>IOCTL のサポート


近接性デバイスドライバーインターフェイスをサポートする Ioctl は、「」で定義されています。 制御コードは、次の属性で定義されます。

-   メソッド\_バッファーされる
-   ファイル\_\_アクセス
-   ファイル\_デバイス\_NFP

各パブリケーションと各サブスクリプションは、ドライバーへのオープンハンドルとして示されています。 そのため、M パブリケーションと N サブスクリプションは、ドライバーに対して M + N 個の開いているハンドルに相当します。 Windows i/o マネージャーでは、プロセスに対する適切なハンドル数制限が適用されます。

IOCTL コードは、のヘッダーに定義されています。

デバイスのセキュリティ記述子は、OS またはデバイスクラスの既定値のままになります。

## <a name="reserved-and-vendor-ioctl-codes"></a>予約済みおよび仕入先 IOCTL コード


次の表では、予約済みおよびベンダ固有の制御コード範囲について説明します。

| タスクバーの検索ボックスに            | 範囲の開始                               | 範囲の終了                                 |
|-----------------|-------------------------------------------|-------------------------------------------|
| 予約済み        | `CTL_CODE(FILE_DEVICE_NFP, 0x0000, *, *)` | `CTL_CODE(FILE_DEVICE_NFP, 0x00FF, *, *)` |
| ベンダー固有 | `CTL_CODE(FILE_DEVICE_NFP, 0x0100, *, *)` | `CTL_CODE(FILE_DEVICE_NFP, 0x01FF, *, *)` |

 

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[近距離無線近接 DDI リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

