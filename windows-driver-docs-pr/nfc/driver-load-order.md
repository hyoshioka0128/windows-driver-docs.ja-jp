---
title: NFC ドライバーの読み込み順序
description: ACPI が NFCC を表すデバイスノードを作成すると、PnP は NFC クライアントドライバーで指定された .inf と照合され、そのデバイスノード用にインストールされます。
ms.assetid: 8094B525-A4A1-42D2-8D1F-4B32D77418E3
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6912d3f22c9a2fb30913f681d318b7b68655ef34
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843421"
---
# <a name="nfc-driver-load-order"></a>NFC ドライバーの読み込み順序


ACPI が NFCC を表すデバイスノードを作成すると、PnP は NFC クライアントドライバーで指定された .inf と照合され、そのデバイスノード用にインストールされます。 NFC クライアントドライバーは、AddDevice ルーチンの実行中に、クラス拡張を初期化します。これにより、Microsoft が提供する NFC クラス拡張 (NfcCx .dll) を読み込み、それ自体が NFC クラスの最上位部分に実装する必要がある i/o キューの処理をセットアップすることができます。拡張機能ドライバー。 次の図は、ドライバーの読み込みメカニズムを示しています。

![ドライバーの読み込み順序](images/driverloadsequence1.png)

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC クラス拡張 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

