---
title: カメラ用の UWP デバイス アプリ
description: このセクションでは、カメラ用の UWP デバイス アプリを紹介します。
ms.assetid: 6CF13679-BCF3-443C-A864-4BBC54B8DA1C
ms.date: 09/14/2018
ms.localizationpriority: medium
ms.openlocfilehash: 06c9376950a595c6a9cc1a8cde59870cf4cb7bc8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369340"
---
# <a name="uwp-device-apps-for-cameras"></a>カメラ用の UWP デバイス アプリ


このセクションでは、カメラ用の UWP デバイス アプリを紹介します。 デバイス アプリでは、カスタマイズされたカメラの設定および特殊なカメラの効果をカメラの特殊な機能を強調表示できます。

## <a name="in-this-section"></a>このセクションの内容


| トピック | 説明 |
| ----- | ----------- |
| [カメラのオプションをカスタマイズする方法](how-to-customize-camera-options.md) | Windows 8.1、UWP デバイス アプリはデバイスの製造元が一部のカメラ アプリでカメラの他のオプションを表示するポップアップのカスタマイズを使用できます。 このトピックでは、<strong>より多くのオプション</strong>フライアウトを表示する、CameraCatureUI API をし、表示方法、C#のバージョン、[カメラ用の UWP デバイス アプリ](https://go.microsoft.com/fwlink/p/?LinkID=227865)サンプルでは、既定のフライアウトで、カスタムのフライアウトです。 |
| [カメラ driver MFT の作成](creating-a-camera-driver-mft.md) | Windows 8.1 では、UWP デバイス アプリは、カメラ driver MFT (メディア ファンデーション変換) でのカメラのビデオ ストリームのカスタム設定と特殊効果を適用するデバイスの製造元を使用できます。 このトピックでは、ドライバーの仕様を紹介しを使用して、 [Driver MFT](https://go.microsoft.com/fwlink/p/?LinkID=251566)サンプルを作成する方法について説明します。<br><br> **重要:** このトピックでは非推奨とされました。 参照してください、[デバイス MFT 設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/stream/dmft-design)のガイダンスを更新します。
| [複数ピン カメラ ドライバー仕様に関する考慮事項](driver-mfts-on-multi-pin-cameras.md) | 一部のカメラは、プレビュー、キャプチャ、および静止画の別々 の pin を指定します。 これらの複数ピン カメラでは、開発者に固有の課題が伴います。 このトピックでは、複数ピン カメラのカメラ driver MFT を開発する際に考慮すべきいくつかの点について説明します。 |
| [内蔵カメラの位置を特定します。](identifying-the-location-of-internal-cameras.md) | このトピックでは、Windows 8.1 でのシステムで内蔵カメラのサポートについての情報を提供します。 これには、UWP アプリで正しく動作するために、組み込みのカメラの物理的な場所を特定する方法について説明します。 UWP デバイス アプリを使用して、カメラが動作するように、モデル ID を設定する方法も説明します。 |


## <a name="windows81-samples"></a>Windows 8.1 のサンプル


-   [カメラ用の UWP デバイス アプリ](https://go.microsoft.com/fwlink/p/?LinkID=227865)サンプル driver MFT によって実装される効果を制御する UWP デバイス アプリを提供します。

-   [Driver MFT](https://go.microsoft.com/fwlink/p/?LinkID=251566)サンプルは、カメラの UWP デバイス アプリで使用するための driver MFT を提供します。 Driver MFT は、ビデオをキャプチャするときに、特定のカメラで使用 Media Foundation 変換です。 Driver MFT は、最初に、カメラからキャプチャされたビデオ ストリームに適用される MFT である、MFT0 とも呼ばれます。 この MFT は、写真やカメラからビデオをキャプチャするときにビデオ特殊効果、またはその他の処理を提供することができます。 カメラのドライバー パッケージと共に配布できます。

-   [カメラ キャプチャ UI](https://go.microsoft.com/fwlink/p/?linkid=228589)サンプルを使用する方法を示して、 [Windows.Media.Capture.CameraCaptureUI](https://docs.microsoft.com/uwp/api/Windows.Media.Capture.CameraCaptureUI) API で、写真やビデオをキャプチャするため、全画面表示の UI が表示されます。 カメラ キャプチャ UI では、写真からビデオ、写真の時間遅延をタイマー、およびカメラの設定を調整するためのカメラ オプション コントロールへの切り替えのコントロールを提供します。

    このサンプルは、呼び出しを使用することができます、[カメラ用の UWP デバイス アプリ](https://go.microsoft.com/fwlink/p/?LinkID=227865)サンプル。

-   [カメラ オプション UI](https://go.microsoft.com/fwlink/p/?linkid=228588)サンプル UWP デバイス アプリでカメラ オプションを使用する方法を示します。
