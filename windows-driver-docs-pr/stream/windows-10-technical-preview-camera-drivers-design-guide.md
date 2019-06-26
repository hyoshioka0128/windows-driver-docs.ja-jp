---
title: Windows 10 用のユニバーサル カメラ ドライバー設計のガイド
description: Windows 10 用のカメラのドライバー インターフェイスはすべてのデバイスの集約し、ユニバーサル カメラ ドライバー モデルを使用します。
ms.assetid: CB5EEDF2-650D-4CD3-A5DE-DF0D6F10B394
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5fc8ef50d7469cbe7ca6d9cf62424e88def4d18b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385355"
---
# <a name="universal-camera-driver-design-guide-for-windows-10"></a>Windows 10 用のユニバーサル カメラ ドライバー設計のガイド


Windows 10 用のカメラのドライバー インターフェイスはすべてのデバイスの集約し、ユニバーサル カメラ ドライバー モデルを使用します。

ユニバーサル カメラ ドライバー モデルには、新しい Ddi などが含まれています。

* [デジタル ビデオ手ブレ補正](ksproperty-cameracontrol-extended-videostabilization.md)
* [可変フレーム レート](ksproperty-cameracontrol-extended-vfr.md)
* [顔検出](ksproperty-cameracontrol-extended-facedetection.md)
* [ハイ ダイナミック レンジ (HDR) ビデオ](ksproperty-cameracontrol-extended-videohdr.md)
* [光学式手ブレ補正](ksproperty-cameracontrol-extended-ois.md)
* [シーン分析: HDR 写真、フラッシュ/フラッシュなし、超ローライト](ksproperty-cameracontrol-extended-advancedphoto.md)
* [統計情報のキャプチャ: メタデータ フレームワーク/属性、ヒストグラム](ksproperty-cameracontrol-extended-histogram.md)
* [スムーズ ズーム](ksproperty-cameracontrol-extended-zoom.md)
* [ハードウェア最適化のヒント](ksproperty-cameracontrol-extended-optimizationhint.md)
* [カメラ プロファイル](ksproperty-cameracontrol-extended-profile.md)

## <a name="build-a-universal-camera-driver"></a>ユニバーサル カメラ ドライバーをビルドします。

ユニバーサルのカメラのドライバーが上に構築された、AVStream ミニドライバー、 [Windows Driver Model](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model) (WDM)。

詳細については、次のセクションを参照してください、 [Windows 10 用のユニバーサル カメラ ドライバー モデルのリファレンス](windows-10-technical-preview-camera-drivers-reference.md):

* [新しいカメラ ドライバーの制御](camera-driver-controls.md)
* [新しいカメラ ドライバーの列挙体](camera-driver-enumerations.md)
* [新しいカメラ ドライバーの機能](camera-driver-functions.md)
* [新しいカメラ ドライバー構造体](camera-driver-structures.md)

AVStream ミニドライバーの構築に関する詳細については、次のトピックを参照してください。

* [AVStream の概要](avstream-overview.md)
* [AVStream、ミニドライバーを作成します。](writing-an-avstream-minidriver.md)



