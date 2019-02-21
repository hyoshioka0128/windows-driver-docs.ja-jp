---
title: Windows 10 用のユニバーサル カメラ ドライバー設計のガイド
description: Windows 10 用のカメラのドライバー インターフェイスはすべてのデバイスの集約し、ユニバーサル カメラ ドライバー モデルを使用します。
ms.assetid: CB5EEDF2-650D-4CD3-A5DE-DF0D6F10B394
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30be0220c48c29aff792afc99f7196dbba7ae793
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560274"
---
# <a name="universal-camera-driver-design-guide-for-windows-10"></a>Windows 10 用のユニバーサル カメラ ドライバー設計のガイド


Windows 10 用のカメラのドライバー インターフェイスはすべてのデバイスの集約し、ユニバーサル カメラ ドライバー モデルを使用します。

ユニバーサル カメラ ドライバー モデルには、新しい Ddi などが含まれています。

* [デジタル ビデオ安定化](ksproperty-cameracontrol-extended-videostabilization.md)
* [可変フレーム レート](ksproperty-cameracontrol-extended-vfr.md)
* [顔検出](ksproperty-cameracontrol-extended-facedetection.md)
* [ハイ ダイナミック レンジ (HDR) のビデオ](ksproperty-cameracontrol-extended-videohdr.md)
* [光の安定化](ksproperty-cameracontrol-extended-ois.md)
* [シーンの分析: HDR の写真、flash、超の低いライトを点滅なし](ksproperty-cameracontrol-extended-advancedphoto.md)
* [統計情報をキャプチャしますメタデータ フレームワーク/属性のヒストグラム。](ksproperty-cameracontrol-extended-histogram.md)
* [滑らかに拡大](ksproperty-cameracontrol-extended-zoom.md)
* [ハードウェアの最適化ヒント](ksproperty-cameracontrol-extended-optimizationhint.md)
* [カメラのプロファイル](ksproperty-cameracontrol-extended-profile.md)

## <a name="build-a-universal-camera-driver"></a>ユニバーサル カメラ ドライバーをビルドします。

ユニバーサルのカメラのドライバーが上に構築された、AVStream ミニドライバー、 [Windows Driver Model](https://msdn.microsoft.com/library/windows/hardware/ff565698) (WDM)。

詳細については、次のセクションを参照してください、 [Windows 10 用のユニバーサル カメラ ドライバー モデルのリファレンス](windows-10-technical-preview-camera-drivers-reference.md):

* [新しいカメラ ドライバーの制御](camera-driver-controls.md)
* [新しいカメラ ドライバーの列挙体](camera-driver-enumerations.md)
* [新しいカメラ ドライバーの機能](camera-driver-functions.md)
* [新しいカメラ ドライバー構造体](camera-driver-structures.md)

AVStream ミニドライバーの構築に関する詳細については、次のトピックを参照してください。

* [AVStream の概要](avstream-overview.md)
* [AVStream、ミニドライバーを作成します。](writing-an-avstream-minidriver.md)



